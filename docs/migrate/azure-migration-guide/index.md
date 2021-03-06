---
title: Руководство по миграции в Azure
description: Cloud Adoption Framework для Azure поможет узнать, как эффективно перенести службы вашей организации в Azure.
author: matticusau
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.localizationpriority: high
ms.custom: think-tank, fasttrack-new, AQC
ms.openlocfilehash: 6b49b694f9db2b3f0b8d7e7a3dc4b9efd28d0849
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101785569"
---
# <a name="azure-migration-guide-overview"></a>Обзор руководств по миграции Azure

[Методика миграции Cloud Adoption Framework](../index.md) предоставляет читателям инструкции по итеративному переносу одной рабочей нагрузки или небольшого набора рабочих нагрузок в каждом выпуске. В ходе каждой итерации необходимо выполнить оценку, миграцию, оптимизацию и повышения уровня, чтобы подготовить рабочие нагрузки к выполнению в рабочей среде. Эти независимые от облака инструкции можно использовать при миграции в среду любого поставщика облачных служб.

В этом руководстве демонстрируется упрощенная версия перехода из локальной среды в **Azure**.

::: zone target="docs"

> [!TIP]
> Чтобы использовать интерактивный интерфейс, просмотрите это руководство на портале Azure. Перейдите в [Центр быстрого запуска Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) на портале Azure, выберите **руководство по миграции в Azure**, а затем выполните пошаговые инструкции.

::: zone-end

## <a name="migration-tools"></a>[Средства миграции](#tab/MigrationTools)

В этом руководстве описан рекомендуемый подход к первой миграции в Azure, включая методику и облачные средства, чаще всего используемые при миграции в Azure. Эти средства описаны на следующих страницах:

> [!div class="checklist"]
>
> - **Оценка технического соответствия каждой рабочей нагрузки.** Проверка технической возможности и готовности к миграции.
> - **Миграция служб**. Выполните фактическую миграцию, реплицировав локальные ресурсы в Azure.
> - **Управление затратами и выставлением счетов.** Составьте представление о средствах, необходимых для управления затратами в Azure.
> - **Оптимизация и повышение уровня.** Оптимизируйте соотношение затрат и производительности перед повышением уровня рабочей нагрузки для выполнения в рабочей среде.
> - **Получение помощи**. Информация о справке и поддержке, которые доступны в ходе миграции или при последующих действиях.

Предполагается, что целевая зона уже развернута в соответствии с [методикой подготовки Cloud Adoption Framework](../../ready/index.md).

## <a name="when-to-use-this-guide"></a>[Когда использовать это руководство](#tab/WhenToUseThisGuide)

Хотя средства, описанные в этом руководстве, поддерживают разные сценарии миграции, здесь мы уделяем внимание в первую очередь действиям с ограниченной областью и *минимальной сложностью*. Чтобы определить, подходит ли это руководство по миграции для вашего проекта, проверьте, соответствуют ли следующие условия вашему сценарию:

- Рабочие нагрузки для начальной миграции не являются критически важными и не содержат конфиденциальные данные.
- Вы переносите однородную среду.
- Для миграции требуется согласование только с несколькими подразделениями организациям.
- Вы не планируете автоматизировать процесс миграции.
- В миграции участвует небольшое количество серверов.
- Вы можете легко определить правила сопоставления зависимостей для переносимых компонентов.
- Для вашей отрасли применяются минимальные нормативные требования, связанные с миграцией.

<!-- docutune:casing "our Microsoft teams" -->

Если хоть одно из этих условий не соответствует вашему сценарию, см. [рекомендации по миграции в облако](../azure-best-practices/index.md). Мы рекомендуем также обратиться к специалистам корпорации Майкрософт или нашим партнерам за помощью, если вам требуется выполнить более сложную миграцию. Клиенты, взаимодействующие с корпорацией Майкрософт или сертифицированными партнерами, более успешно справляются с такими сценариями. Дополнительные сведения о получении поддержки предоставлены в этом руководстве.

::: zone target="docs"

Дополнительные сведения см. в разделе:

- [Рекомендации по миграции в облако](../azure-best-practices/index.md)

::: zone-end
