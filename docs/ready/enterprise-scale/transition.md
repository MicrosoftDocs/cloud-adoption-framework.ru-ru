---
title: Переход с существующих сред Azure на корпоративный масштаб
description: Подключение существующих сред к архитектуре корпоративного масштаба
author: JefferyMitchell
ms.author: brblanch
ms.date: 10/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank, csu
ms.openlocfilehash: ab93248b465053b7eba13ce490395d4388e51375
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101785790"
---
<!-- docutune:casing resourceType resourceTypes resourceId resourceIds -->

# <a name="transition-existing-azure-environments-to-enterprise-scale"></a>Переход с существующих сред Azure на корпоративный масштаб

Мы понимаем, что у большинства организаций может быть существующее место в Azure, одна или несколько подписок, а также существующая структура групп управления. В зависимости от первоначальных бизнес-требований и сценариев, возможно, были развернуты ресурсы Azure, такие как гибридное подключение (например, VPN типа "сеть — сеть" или ExpressRoute).

Эта статья поможет организациям перемещаться по нужному пути на основе существующей среды Azure, переходя на корпоративный масштаб. В этой статье также приводятся рекомендации по перемещению ресурсов в Azure (например, перенос подписки из одной существующей группы управления в другую), которая поможет оценить и спланировать перенос существующей среды Azure в целевые зоны корпоративного уровня.

## <a name="moving-resources-in-azure"></a>Перемещение ресурсов в Azure

Некоторые ресурсы в Azure можно переместить после создания, и существуют различные подходы, с которыми организации могут подчиняться пользователям разрешения RBAC в Azure на уровне "на" и "в разных областях". В следующей таблице показано, какие ресурсы можно перемещать, в какой области, а также о преимуществах и недостатках, связанных с каждым из них.

| Область | Назначение | Плюсы | Минусы |
|--|--|--|--|
| Ресурсы в группах ресурсов | Можно переместить в новую группу ресурсов в той же или другой подписке. | Позволяет изменить композицию ресурсов в группе ресурсов после развертывания | — Не поддерживается всеми Ресаурцетипес <br> -Некоторые Ресаурцетипес имеют определенные ограничения или требования <br> -Идентификаторы ресурсов обновляются и влияет на существующие операции мониторинга, оповещений и управления. <br> -Группы ресурсов блокируются в течение периода перемещения <br> — Требует оценки политик и операций до и после перемещения RBAC. |
| Подписки в клиенте | Можно переместить в различные группы управления | Нет влияния на существующие ресурсы в подписке, так как значения resourceId не будут изменены | Требуется оценка политик и операций, выполняемых до и после перемещения RBAC |

Чтобы понять, какую стратегию перемещения следует использовать, мы рассмотрим примеры обоих способов.

## <a name="subscription-move"></a>Перемещение подписки

Распространенными вариантами использования для перемещения подписок является организация подписок на группы управления или передача подписок в новый клиент Azure Active Directory. Перемещение подписки на корпоративный масштаб ориентировано на перемещение подписок в группы управления. Перемещение подписки на новый клиент в основном предназначено для [передачи владения выставлением счетов](/azure/cost-management-billing/manage/billing-subscription-transfer).

### <a name="azure-rbac-requirements"></a>Требования к Azure RBAC

Чтобы оценить подписку перед перемещением, важно, чтобы у пользователя был соответствующий экземпляр Azure RBAC, такой как владелец подписки (прямое назначение ролей), и он имеет разрешение на запись в целевую группу управления (встроенные роли, поддерживающие это, являются ролью владельца, ролью участника и ролью участника группы управления).

Если у пользователя есть разрешение "унаследованная роль владельца" для подписки из существующей группы управления, то подписку можно переместить только в группу управления, в которой пользователю была назначена роль владельца.

### <a name="policy"></a>Политика

К существующим подпискам могут применяться политики Azure либо напрямую, либо в группе управления, в которой они находятся. Важно оценить текущие политики и политики, которые могут существовать в новой иерархии группы управления или группы управления.

Граф ресурсов Azure можно использовать для выполнения инвентаризации существующих ресурсов и сравнения их конфигурации с политиками, существующими в назначении.

После перемещения подписок в группу управления с существующими политиками Azure RBAC и политик на месте рассмотрите следующие варианты.

- Все Azure RBAC, наследуемые для перемещенных подписок, могут пройти до 30 минут, прежде чем маркеры пользователей в кэше группы управления будут обновлены. Чтобы ускорить этот процесс, можно обновить маркер, выполнив выход, или запросить новый маркер.
- Любая политика, в которой область назначения включает перемещенные подписки, выполняет операции аудита только для существующих ресурсов. В частности:
  - Любой существующий ресурс в подписке, соответствующий условию `DeployIfNotExists` политики, будет отображаться как не соответствующий политике и не будет исправлен автоматически, но требует вмешательства пользователя для выполнения исправления вручную.
  - Любой существующий ресурс в подписке, подверженный условиям `Deny` политики, будет отображаться как не соответствующий политике и не будет отклонен. Пользователь должен вручную устранить этот результат, как нужно.
  - Любой существующий ресурс в подписке `Append` и воздействие на `Modify` политику будут отображаться как не соответствующие требованиям и требуется вмешательство пользователя для устранения проблемы.
  - Любой существующий ресурс в подписке `Audit` и воздействие на `AuditIfNotExist` политику будут отображаться как не соответствующие требованиям и требуется вмешательство пользователя для устранения проблемы.
- Все новые операции записи в ресурсы в перемещенной подписке подчиняются назначенным политикам в режиме реального времени как обычные.

## <a name="resource-move"></a>Перемещение ресурсов

Основным вариантом использования при перемещении ресурсов является необходимость консолидации ресурсов в одну группу ресурсов, если они совместно используют один жизненный цикл, или перемещение ресурсов в другую подписку из-за стоимости, владельца или требований к Azure RBAC.

При перемещении ресурса и исходная группа ресурсов, и Целевая группа ресурсов будут заблокированы (Эта блокировка не повлияет на ресурсы в группе ресурсов) во время операции перемещения, что означает, что нельзя добавлять, обновлять или удалять ресурсы в группах ресурсов. Операция перемещения ресурса не изменит расположение ресурсов.

### <a name="before-you-move-resources"></a>Перед перемещением ресурсов

Перед операцией перемещения необходимо убедиться, что [ресурсы в области поддерживаются](/azure/azure-resource-manager/management/move-support-resources) , а также оценить их требования и зависимости. Например, чтобы переместить одноранговую виртуальную сеть, сначала необходимо отключить пиринг виртуальных сетей, а затем снова включить пиринг после завершения операции перемещения. Чтобы отключить или повторно включить зависимость, необходимо заранее спланировать, чтобы понять влияние на любую существующую рабочую нагрузку, которая может быть подключена к виртуальным сетям.

### <a name="post-move-operation"></a>Операция после перемещения

При перемещении ресурсов в новую группу ресурсов в одной подписке все наследуемые Azure RBAC и политики из группы управления или области подписки будут по-прежнему применяться. Если вы перейдете к группе ресурсов в новой подписке, в которой может быть наложена подписка на другие политики Azure RBAC и назначение политик, то же самое руководство применяется к сценарию перемещения подписки для проверки соответствия ресурсов и контроля доступа.
