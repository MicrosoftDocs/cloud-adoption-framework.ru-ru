---
title: Включение служб управления сервером на одной виртуальной машине для оценки
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Включение служб управления сервером на одной виртуальной машине для оценки
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7ee8cab09fc5ad875240a10d7fe6f632d91432c9
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73751660"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Включение служб управления сервером на одной виртуальной машине для оценки

Узнайте, как включить службы управления сервером на одной виртуальной машине для оценки.

> [!NOTE]
> Перед реализацией служб управления Azure на виртуальной машине создайте необходимую [рабочую область log Analytics и учетную запись службы автоматизации Azure](./prerequisites.md#create-a-workspace-and-automation-account) .

Вы можете легко подключить службы управления сервером Azure к отдельным виртуальным машинам в портал Azure. Вы можете ознакомиться с этими службами перед их внедрением. При выборе экземпляра виртуальной машины все решения в списке [средств управления и служб](./tools-services.md) отображаются в меню **операции** или **мониторинг** . Выберите решение и следуйте указаниям мастера, чтобы подключить его.

![Снимок экрана параметров виртуальной машины в портал Azure](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Связанные ресурсы

Дополнительные сведения о том, как подключить эти решения к отдельным виртуальным машинам, см. в следующих статьях:

- [Подключение решений Управление обновлениями, Отслеживание изменений и инвентаризации из виртуальной машины Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Подключение мониторинга Azure для виртуальных машин](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как использовать политику Azure для подключения виртуальных машин Azure в нужном масштабе.

> [!div class="nextstepaction"]
> [Настройка служб управления Azure для подписки](./onboard-at-scale.md)
