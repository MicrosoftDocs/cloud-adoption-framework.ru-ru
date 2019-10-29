---
title: Соответствие операций нормативным требованиям в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Обеспечение стабильности бизнес-процессов за счет повышения соответствия операций нормативным требованиям
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7073df6b697da49429d4086d9f8f3f113583e52d
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557097"
---
# <a name="operational-compliance-in-azure"></a>Соответствие операций нормативным требованиям в Azure

Соответствие операций нормативным требованиям — это вторая дисциплина в любом базовом плане управления облаком.

![Базовый план управления облаком](../../_images/manage/management-baseline.png)

Повышение соответствия операций нормативным требованиям снижает вероятность сбоя, связанного с отклонением конфигурации, или уязвимостей, связанных с системами, для которых не выполняется правильное исправление.

В следующей таблице приведены рекомендуемые минимальные средства для любого базового плана управления для любой среды корпоративного уровня.

|Process  |Средство  |Назначение  |
|---------|---------|---------|
|Управление исправлениями|Управление обновлениями|Управление обновлениями и их планирование|
|Принудительное применение политики|Политика Azure|Применение политик для обеспечения соответствия сред и гостевых машин|
|Среда: Конфигурация|Azure Blueprint|Автоматическое обеспечение соответствия для основных служб|

::: zone target="docs"

## <a name="update-management"></a>Управление обновлениями

::: zone-end
::: zone target="chromeless"

## <a name="update-managementtabupdatemanagement"></a>[Управление обновлениями](#tab/UpdateManagement)

::: zone-end

Ниже перечислены конфигурации, которые используются компьютерами, управляемыми с помощью решения "Управление обновлениями", для выполнения развертываний оценок и обновлений:

- Microsoft Monitoring Agent (MMA) для Windows или Linux;
- служба настройки требуемого состояния PowerShell;
- гибридные рабочие роли Runbook службы автоматизации;
- службы Центра обновления Майкрософт или Windows Server Update Services (WSUS) для компьютеров с Windows.

Дополнительные сведения см. в статье [Update Management solution in Azure](https://docs.microsoft.com/azure/automation/automation-update-management) (Решение для управления обновлениями в Azure).

> [!WARNING]
> Прежде чем использовать решение для управления обновлениями, необходимо подключить виртуальные машины или всю подписку к Log Analytics и службе автоматизации Azure.
> Есть два подхода к подключению. Прежде чем перейти к управлению обновлениями, следует выполнить действия для одного из этих подходов:
>
> - [использование отдельной виртуальной машины](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm);
> - [использование всей подписки](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale).

### <a name="manage-updates"></a>Управление обновлениями

Чтобы применить политику к группе ресурсов, сделайте следующее:

1. Щелкните [Служба автоматизации Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Выберите одну из перечисленных **учетных записей автоматизации**.
3. Найдите раздел **Управление конфигурацией** в области навигации портала.
4. Возможности инвентаризации, управления изменениями и настройки состояния могут использоваться для управления состоянием управляемых виртуальных машин и соответствием их операций нормативным требованиям.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Политика Azure

::: zone-end
::: zone target="chromeless"

## <a name="azure-policytabazurepolicy"></a>[Политика Azure](#tab/AzurePolicy)

::: zone-end

Политика Azure используется во всех процессах управления. Это также очень полезно в процессах управления облаком. В дополнение к аудиту и исправлению ресурсов Azure, служба "Политика Azure" поддерживает аудит параметров на виртуальной машине. Проверка выполняется с помощью расширения гостевой конфигурации и клиента. Расширение с помощью клиента проверяет такие параметры, как:

- конфигурация операционной системы;
- конфигурация или наличие приложения;
- Параметры среды

В настоящее время гостевая конфигурация политики Azure выполняет аудит только параметров внутри компьютера. Конфигурации не применяются.

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

### <a name="learn-more"></a>Подробнее

Дополнительные сведения см. на следующих ресурсах:

- [Политика Azure](https://docs.microsoft.com/azure/azure-policy)
- [Understand Azure Policy's Guest Configuration](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) (Общие сведения о гостевой конфигурации службы "Политика Azure").
- [Role-based по принудительному применению политик](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprints

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprints](#tab/AzureBlueprints)

::: zone-end

Служба Azure Blueprints позволяет облачным архитекторам и центральным ИТ-группам определять воспроизводимый набор ресурсов Azure, который реализует стандарты, шаблоны и требования организации и полностью соответствует им. С помощью Azure Blueprints группы разработчиков могут быстро создавать и настраивать новые среды, зная, что они создаются в соответствии с требованиями организации и с рядом встроенных компонентов, таких как сети, для ускорения разработки и поставки.

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
1. В разделе **Создание схемы** выберите **Создать**.
1. Отфильтруйте список схем, чтобы выбрать соответствующую схему.
1. Введите **имя** и выберите соответствующий **источник определения**.
1. Щелкните **Далее: Артефакты >>** и просмотрите артефакты, включенные в схему.
1. Щелкните **Сохранить черновик**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Перейдите в раздел [Схемы — Начало работы](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. В разделе **Создание схемы** выберите **Создать**.
1. Отфильтруйте список схем, чтобы выбрать соответствующую схему.
1. Введите **имя** и выберите соответствующий **источник определения**.
1. Щелкните **Далее: Артефакты >>** и просмотрите артефакты, включенные в схему.
1. Щелкните **Сохранить черновик**.

::: zone-end

### <a name="publish-a-blueprint"></a>Публикация схемы

Чтобы опубликовать артефакты схемы в подписке, сделайте следующее:

::: zone target="chromeless"

1. Перейдите в раздел **Схемы — Определения схем**.
1. Выберите схему, созданную ранее.
1. Проверьте определение схемы и щелкните **Опубликовать схему**.
1. Укажите **версию** (например, 1.0) и все **заметки об изменениях**, а затем выберите **Опубликовать**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Перейдите в раздел [Схемы — Определения схем](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Выберите схему, созданную ранее.
1. Проверьте определение схемы и щелкните **Опубликовать схему**.
1. Укажите **версию** (например, 1.0) и все **заметки об изменениях**, а затем выберите **Опубликовать**.

### <a name="learn-more"></a>Подробнее

Дополнительные сведения см. на следующих ресурсах:

- [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints)
- [Руководство по принятию решений касательно согласованности ресурсов](../../decision-guides/resource-consistency/index.md)
- [Примеры схем на основе стандартов](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
