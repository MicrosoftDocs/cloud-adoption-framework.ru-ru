---
title: Включение служб управления сервером на виртуальной машине
description: Узнайте, как включить службы управления Azure Server на одной виртуальной машине, с помощью инфраструктуры внедрения в облако для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: internal
ms.openlocfilehash: ed0b6a1f4aeeda17568c3bd93ec6fa3b34d755c1
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101792250"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Включение служб управления сервером на одной виртуальной машине для оценки

Узнайте, как включить службы управления сервером на одной виртуальной машине для оценки.

> [!NOTE]
> Перед реализацией служб управления Azure на виртуальной машине создайте необходимую [рабочую область log Analytics и учетную запись службы автоматизации Azure](./prerequisites.md#create-a-workspace-and-automation-account) .

Вы можете легко подключить службы управления сервером Azure к отдельным виртуальным машинам в портал Azure. Вы можете ознакомиться с этими службами перед их внедрением. При выборе экземпляра виртуальной машины все решения в списке [средств управления и служб](./tools-services.md) отображаются в меню **операции** или **мониторинг** . Выберите решение и следуйте указаниям мастера, чтобы подключить его.

![Снимок экрана параметров виртуальной машины в портал Azure](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Связанные ресурсы

Дополнительные сведения о том, как подключить эти решения к отдельным виртуальным машинам, см. в следующих статьях:

- [Подключение решения Управление обновлениями и Отслеживание изменений и инвентаризации для виртуальной машины в Azure](/azure/automation/change-tracking/manage-inventory-vms)
- [Включение Azure Monitor для виртуальных машин.](/azure/azure-monitor/vm/vminsights-enable-portal)

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как использовать политику Azure для подключения виртуальных машин Azure в нужном масштабе.

> [!div class="nextstepaction"]
> [Настройка служб управления Azure для подписки](./onboard-at-scale.md)
