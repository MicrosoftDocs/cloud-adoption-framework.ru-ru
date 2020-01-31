---
title: Оптимизация и преобразование
description: Оптимизация и преобразование
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 5d9ec518069023a8db763a9fc21f7c4847053be6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807008"
---
# <a name="optimize-and-transform"></a>Оптимизация и преобразование

Теперь, когда вы перенесли службы в Azure, необходимо рассмотреть решение для возможных областей оптимизации. Это может включать в себя проверку проекта решения, изменение размера служб и анализ затрат.

На этом этапе можно также оптимизировать среду и выполнить ее преобразование. Например, вы могли выполнить миграцию с повторным размещением, и теперь, когда ваши службы работают в Azure, вы можете пересмотреть конфигурацию решений или использованные службы и, возможно, выполнить рефакторинг некоторых компонентов, чтобы модернизировать свое решение и повысить его функциональные возможности.

# <a name="right-size-assetstaboptimize"></a>[Выбор соответствующего размера ресурсов](#tab/optimize)

Размер всех служб Azure, которые поддерживают модель затрат на основе потребления, можно изменить с помощью портала Azure, интерфейса командной строки или PowerShell. Первым шагом для правильного определения размера службы является проверка ее метрик использования. Служба Azure Monitor предоставляет доступ к этим метрикам. Может потребоваться настроить сбор метрик для анализируемой службы и предоставить соответствующее время для сбора значимых данных на основе шаблонов рабочих нагрузок.

1. Перейдите в раздел **Монитор**.
1. Выберите **Метрики** и настройте диаграмму, чтобы отобразить метрики анализируемой службы.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/metrics]" submitText="Go to Monitor" :::

::: zone-end

Ниже приведены некоторые распространенные службы, размер которых можно изменить.

## <a name="resize-a-virtual-machine"></a>Изменение размера виртуальной машины

Миграция Azure выполняет анализ соответствия размера на этом этапе оценки перед переносом, и размер виртуальных машин, перенесенных с помощью этого инструмента, скорее всего, будет выбран в соответствии с предварительными требованиями к миграции.

Однако для виртуальных машин, созданных или перенесенных с помощью других методов, или в случаях, когда после миграции требуется скорректировать требования к виртуальной машине, может потребоваться уточнить размер виртуальной машины.

1. Перейдите в раздел **Виртуальная машина**.
1. Выберите необходимую виртуальную машину из списка.
1. Щелкните **Размер** и выберите желаемый новый размер из списка. Возможно, потребуется настроить фильтры, чтобы найти нужный размер.
1. Выберите **Изменить размер**.

Обратите внимание на то, что изменение размера рабочих виртуальных машин может привести к нарушению работы службы. Попробуйте применить правильный размер виртуальных машин перед тем, как перенести их в рабочую среду.


::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

- [Управление резервированиями для ресурсов Azure](https://docs.microsoft.com/azure/billing/billing-manage-reserved-vm-instance)
- [Изменение размера виртуальной машины Windows](https://docs.microsoft.com/azure/virtual-machines/windows/resize-vm)
- [Изменение размера виртуальной машины Linux с помощью интерфейса командной строки Azure](https://docs.microsoft.com/azure/virtual-machines/linux/change-vm-size)

Партнеры могут использовать Центр партнеров для просмотра сведений об использовании.

- [Выбор размера виртуальной машины Microsoft Azure для максимального использования резервирования](https://docs.microsoft.com/partner-center/azure-usage)

::: zone-end

## <a name="resize-a-storage-account"></a>Изменение размера учетной записи хранения

1. Перейдите в раздел **Учетные записи хранения**.
1. Выберите нужную учетную запись хранения.
1. Выберите **Настроить** и настройте свойства учетной записи хранения в соответствии с вашими требованиями.
1. Щелкните **Сохранить**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2FStorageAccounts]" submitText="Go to Storage Accounts" :::

::: zone-end

## <a name="resize-a-sql-database"></a>Изменение размера Базы данных SQL

1. Перейдите в раздел **Базы данных SQL** или **Серверы SQL Server**, а затем выберите сервер.
1. Выберите нужную базу данных.
1. Выберите **Настройка** и желаемый новый размер уровня служб.
1. Нажмите кнопку **Применить**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Sql%2Fservers%2Fdatabases]" submitText="Go to SQL Databases" :::

::: zone-end

# <a name="cost-managementtabmanagecost"></a>[Управление затратами](#tab/ManageCost)

Важно оперативно выполнять анализ и проверку затрат. Это дает возможность изменять размер ресурсов по мере необходимости, чтобы балансировать затраты и рабочую нагрузку.

Управление затратами Azure работает с Помощником по Azure, чтобы обеспечить рекомендации по оптимизации затрат. Помощник по Azure помогает повысить эффективность работы благодаря выявлению незадействованных или недостаточно используемых ресурсов.

1. Выберите **Управление затратами + выставление счетов"** .
1. Выберите **Рекомендации консультанта** и щелкните вкладку **Затраты**.
1. В полях **Воздействие** и **Потенциальная ежегодная экономия** просмотрите потенциальные преимущества.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" :::

::: zone-end

Можно также использовать **Помощник** и выбрать вкладку **Затраты**, чтобы найти рекомендации по снижению затрат.

> [!TIP]
> Для служб, которым не требуются непрерывная доступность, реализуйте решение для запуска, остановки или приостановки службы по необходимости, чтобы помочь в управлении затратами (например, для Виртуальных машин Azure или Хранилища данных SQL Azure).
>

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

- [Руководство. Рекомендации по оптимизации затрат](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations)
- [Предотвращение непредвиденных расходов с помощью функции выставления счетов и управления затратами в Azure](https://docs.microsoft.com/azure/billing/billing-getting-started)
- [Изучение и анализ затрат с помощью функции анализа затрат](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis)

::: zone-end
