---
title: Включение служб управления на одной виртуальной машине для оценки
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Включение служб управления на одной виртуальной машине для оценки
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e9d5e17e87d79d8d1fdf7239298a973959103a37
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029310"
---
# <a name="enable-management-services-on-a-single-vm-for-evaluation"></a>Включение служб управления на одной виртуальной машине для оценки

Узнайте, как включить службы управления на одной виртуальной машине для оценки.

> [!NOTE]
> Перед подключением виртуальных машин к службам управления Azure создайте необходимую [рабочую область log Analytics и учетную запись службы автоматизации Azure](./prerequisites.md#create-a-workspace-and-automation-account) .

Подключение отдельных виртуальных машин к службам управления сервером Azure осуществляется просто в портал Azure. На портале вы можете ознакомиться с этими службами, прежде чем подключать их к вашим виртуальным машинам. При выборе экземпляра виртуальной машины все решения, описанные в списке [средств и служб управления](./tools-services.md) , отображаются в меню " **операции** " или " **мониторинг** ". Можно выбрать каждое решение и следовать указаниям мастера, чтобы подключить его.

![Снимок экрана параметров виртуальной машины в портал Azure](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Связанные ресурсы

Дополнительные сведения о адаптации отдельных виртуальных машин к каждому решению см. в следующих статьях:

- [Подключение решений Управление обновлениями, Отслеживание изменений и инвентаризации из виртуальной машины Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Подключение мониторинга Azure для виртуальной машины](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Следующие шаги

Узнайте, как использовать политику Azure для подключения виртуальных машин Azure в нужном масштабе.

> [!div class="nextstepaction"]
> [Настройка служб управления Azure для подписки](./onboard-at-scale.md)
