---
title: Соответствие операций нормативным требованиям в Azure
description: Узнайте, как поддерживать стабильность бизнеса благодаря обеспечению операционного соответствия, уменьшая вероятность простоев или уязвимостей.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b747a6f0d50fbf2510dc3a5220f72d513e8d1cb3
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216713"
---
<!-- cSpell:ignore WSUS getting started -->

# <a name="operational-compliance-in-azure"></a>Соответствие операций нормативным требованиям в Azure

_Соответствие операций нормативным требованиям_ — это вторая дисциплина в любом базовом плане управления облаком.

![Базовый план управления облаком](../../_images/manage/management-baseline.png)

Повышение соответствия операций нормативным требованиям снижает вероятность сбоя, связанного с отклонением конфигурации, или уязвимостей, связанных с системами, для которых не выполняется правильное исправление.

В этой таблице приведены рекомендуемые минимальные средства для базового плана управления для любой среды корпоративного уровня.

| Процесс | Инструмент | Назначение |
|---|---|---|
| Управление исправлениями | Управление обновлениями | Управление обновлениями и их планирование |
| Принудительное применение политики | Политика Azure | Применение политик для обеспечения соответствия сред и гостевых машин |
| Настройка среды | Azure Blueprints | Автоматическое обеспечение соответствия для основных служб |
| Настройка ресурса | Настройка требуемого состояния (DSC) | Автоматическая настройка в гостевой ОС и некоторых аспектов среды |

::: zone target="docs"

## <a name="update-management"></a>Управление обновлениями

::: zone-end
::: zone target="chromeless"

## <a name="update-management"></a>[Управление обновлениями](#tab/UpdateManagement)

::: zone-end

Ниже перечислены конфигурации, которые используются компьютерами, управляемыми с помощью решения "Управление обновлениями", для выполнения развертываний оценок и обновлений:

- Microsoft Monitoring Agent (MMA) для Windows или Linux;
- платформа PowerShell Desired State Configuration для Linux;
- гибридные рабочие роли Runbook службы автоматизации Azure;
- службы Центра обновления Майкрософт или Windows Server Update Services (WSUS) для компьютеров с Windows.

Дополнительные сведения см. в статье [Update Management solution in Azure](https://docs.microsoft.com/azure/automation/automation-update-management) (Решение для управления обновлениями в Azure).

> [!WARNING]
> Прежде чем использовать решение "Управление обновлениями", необходимо подключить виртуальные машины или всю подписку к Log Analytics и службе автоматизации Azure.
>
> Существует два подхода для подключения:
>
> - [использование отдельной виртуальной машины](../../manage/azure-server-management/onboard-single-vm.md);
> - [использование всей подписки](../../manage/azure-server-management/onboard-at-scale.md).
>
> Прежде чем продолжить работу с решением "Управление обновлениями" выберите один из них.

### <a name="manage-updates"></a>Управление обновлениями

Чтобы применить политику к группе ресурсов, сделайте следующее:

1. Щелкните [Служба автоматизации Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Выберите **Учетные записи автоматизации** и одну из перечисленных учетных записей.
1. Перейдите в раздел **Управление конфигурацией**.
1. Возможности **инвентаризации**, **управления изменениями** и **настройки состояния** могут использоваться для управления состоянием управляемых виртуальных машин и соответствием их операций нормативным требованиям.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Политика Azure

::: zone-end
::: zone target="chromeless"

## <a name="azure-policy"></a>[Политика Azure](#tab/AzurePolicy)

::: zone-end

Политика Azure используется во всех процессах управления. Это также очень полезно в процессах управления облаком. Политика Azure может выполнять аудит ресурсов Azure и оптимизировать их, а также выполнять аудит параметров на компьютере. Проверка выполняется с помощью расширения гостевой конфигурации и клиента. Расширение с помощью клиента проверяет такие параметры, как:

- конфигурация операционной системы;
- конфигурация или наличие приложения;
- параметры среды.

Сейчас гостевая конфигурация политики Azure выполняет аудит только параметров внутри компьютера. Конфигурации не применяются.

::: zone target="chromeless"

### <a name="action"></a>Действие

Назначение встроенной политики для группы управления, подписки или группы ресурсов.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

### <a name="apply-a-policy"></a>Применение политики

Чтобы применить политику к группе ресурсов, сделайте следующее:

1. Перейдите в раздел [Политика Azure](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Щелкните **Assign a policy** (Назначить политику).

### <a name="learn-more"></a>Дополнительные сведения

Дополнительные сведения см. на следующих ресурсах:

- [Политика Azure](https://docs.microsoft.com/azure/azure-policy)
- [Understand Azure Policy's Guest Configuration](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) (Общие сведения о гостевой конфигурации службы "Политика Azure").
- [Role-based по принудительному применению политик](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprints

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprints"></a>[Azure Blueprints](#tab/AzureBlueprints)

::: zone-end

С помощью Azure Blueprints облачные архитекторы и центральные ИТ-группы могут определить повторяемый набор ресурсов Azure. В этих ресурсах реализуются и соблюдаются стандарты, шаблоны и требования организации.

С помощью Azure Blueprints группы разработчиков могут быстро создавать и подготавливать новые среды. Команды также могут надежно создавать решения в соответствии с требованиями организации. Это делается с помощью набора встроенных компонентов, таких как сеть, для ускорения разработки и предоставления решений.

Схемы — это декларативный способ оркестрации развертывания различных шаблонов ресурсов и других артефактов, таких как:

- Назначения ролей.
- Назначения политик.
- Шаблоны Azure Resource Manager.
- Группы ресурсов.

Применение схемы может обеспечить соблюдение соответствия операций нормативным требованиям в среде, если это еще не сделано командой управления облаком.

### <a name="create-a-blueprint"></a>Создание схемы

Чтобы создать схему, сделайте следующее:

::: zone target="chromeless"

1. Перейдите в раздел **Схемы — Начало работы**.
1. На панели **Создание схемы** выберите **Создать**.
1. Отфильтруйте список схем, чтобы выбрать соответствующую схему.
1. В поле **Имя схемы** введите имя схемы.
1. Выберите **Расположение определения** и нужное расположение.
1. Выберите **Далее: Артефакты >>** и просмотрите артефакты, включенные в схему.
1. Выберите **Сохранить черновик**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Перейдите в раздел [Схемы — Начало работы](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. На панели **Создание схемы** выберите **Создать**.
1. Отфильтруйте список схем, чтобы выбрать соответствующую схему.
1. В поле **Имя схемы** введите имя схемы.
1. Выберите **Расположение определения** и нужное расположение.
1. Выберите **Далее: Артефакты >>** и просмотрите артефакты, включенные в схему.
1. Выберите **Сохранить черновик**.

::: zone-end

### <a name="publish-a-blueprint"></a>Публикация схемы

Чтобы опубликовать артефакты схемы в подписке, сделайте следующее:

::: zone target="chromeless"

1. Перейдите в раздел **Схемы — Определения схем**.
1. Выберите схему, созданную ранее.
1. Проверьте определение схемы и щелкните **Опубликовать схему**.
1. В поле **Версия** введите версию, например 1.0.
1. В поле **Сведения об изменениях** введите свои заметки.
1. Нажмите кнопку **Опубликовать**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Перейдите в раздел [Схемы — Определения схем](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Выберите схему, созданную ранее.
1. Проверьте определение схемы и щелкните **Опубликовать схему**.
1. В поле **Версия** введите версию, например 1.0.
1. В поле **Сведения об изменениях** введите свои заметки.
1. Нажмите кнопку **Опубликовать**.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Дополнительные сведения

Дополнительные сведения см. на следующих ресурсах:

- [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints)
- [Role-based по принятию решений касательно согласованности ресурсов](../../decision-guides/resource-consistency/index.md)
- [Примеры схем на основе стандартов](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
