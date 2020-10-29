---
title: Включение служб управления сервером на виртуальной машине
description: Узнайте, как включить службы управления Azure Server на одной виртуальной машине, с помощью инфраструктуры внедрения в облако для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 1b8389e4869383be2ed03600e904a2f982d8a237
ms.sourcegitcommit: 826f2a3f0353bb711917e99d9a17f6198fb41ada
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "93024527"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Включение служб управления сервером на одной виртуальной машине для оценки

Узнайте, как включить службы управления сервером на одной виртуальной машине для оценки.

> [!NOTE]
> Перед реализацией служб управления Azure на виртуальной машине создайте необходимую [рабочую область log Analytics и учетную запись службы автоматизации Azure](./prerequisites.md#create-a-workspace-and-automation-account) .

Вы можете легко подключить службы управления сервером Azure к отдельным виртуальным машинам в портал Azure. Вы можете ознакомиться с этими службами перед их внедрением. При выборе экземпляра виртуальной машины все решения в списке [средств управления и служб](./tools-services.md) отображаются в меню **операции** или **мониторинг** . Выберите решение и следуйте указаниям мастера, чтобы подключить его.

![Снимок экрана параметров виртуальной машины в портал Azure](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Связанные ресурсы

Дополнительные сведения о том, как подключить эти решения к отдельным виртуальным машинам, см. в следующих статьях:

- [Подключение решений Управление обновлениями, Отслеживание изменений и инвентаризации из виртуальной машины Azure](/azure/automation/change-tracking/manage-inventory-vms)
- [Подключение мониторинга Azure для виртуальных машин](/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как использовать политику Azure для подключения виртуальных машин Azure в нужном масштабе.

> [!div class="nextstepaction"]
> [Настройка служб управления Azure для подписки](./onboard-at-scale.md)
