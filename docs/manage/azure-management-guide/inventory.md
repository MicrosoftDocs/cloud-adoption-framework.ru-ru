---
title: Инвентаризация и визуальный контроль в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Из этой статьи вы узнаете, как настроить визуальный контроль, мониторинг, создание отчетов и оповещения для среды управления Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 84efac562647d88235dbcecbb2078e632c1c0341
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565467"
---
# <a name="inventory-and-visibility-in-azure"></a>Инвентаризация и визуальный контроль в Azure

_Инвентаризация и визуальный контроль_ — это первая из трех дисциплин в базовом плане управления облаком.

![Базовый план управления облаком](../../_images/manage/management-baseline.png)

Эта дисциплина должна быть первой, так как при принятии решений об операциях важно собирать правильные рабочие данные. Команды специалистов управления облачными задачами должны понимать, какие ресурсы администрируются и насколько хорошо они работают. В этой статье рассматриваются различные средства, которые предоставляют как инвентаризацию, так и визуальный контроль состояния выполнения инвентаризации.

В следующей таблице приведены рекомендуемые минимальные средства для базового плана управления для любой среды корпоративного уровня.

|Process  |Средство  |Назначение  |
|---------|---------|---------|
|Мониторинг работоспособности служб Azure|Работоспособность служб Azure|Работоспособность, производительность и диагностика служб, работающих в Azure|
|Централизованное ведение журнала|Log Analytics|Централизованное ведение журнала для всех целей визуального контроля|
|Централизованный мониторинг|Azure Monitor|Централизованный мониторинг операционных данных и тенденций|
|Инвентаризация и отслеживание изменений виртуальных машин|Отслеживание изменений и инвентаризация Azure|Инвентаризация виртуальных машин и мониторинг изменений на уровне гостевой ОС|
|Работоспособность службы|Журнал действий Azure|Мониторинг изменений на уровне подписки|
|Мониторинг гостевой ОС|Azure Monitor для виртуальных машин|Мониторинг изменений и производительности виртуальных машин|
|Мониторинг сетей.|Наблюдатель за сетями Azure|Мониторинг сетевых изменений и производительности|
|Мониторинг DNS|Аналитика DNS|Безопасность, производительность и операции DNS|

::: zone target="docs"

## <a name="azure-service-health"></a>Работоспособность служб Azure

::: zone-end
::: zone target="chromeless"

## <a name="azure-service-healthtabazureservicehealth"></a>[Служба "Работоспособность служб Azure"](#tab/AzureServiceHealth)

::: zone-end

Работоспособность служб Azure предоставляет персонализированное представление состояния работоспособности ваших служб и регионов Azure. В нем публикуется информация об активных проблемах, которая поможет вам понять влияние этих проблем на ваши ресурсы. Информация регулярно обновляется, и в случае решения проблем вы получаете уведомление.

Кроме того, в решении "Работоспособность служб" публикуются объявления о событиях планового обслуживания, чтобы оповестить вас об изменениях, которые могут повлиять на доступность ваших ресурсов. Настройте оповещения для решения "Работоспособность служб", чтобы получать уведомления о проблемах служб, плановом обслуживании и других изменениях, которые могут повлиять на ваши службы и регионы Azure.

Служба "Работоспособность служб Azure" предоставляет такие сведения:

- **Состояние Azure:** глобальное представление со сведениями о работоспособности служб Azure.
- **Работоспособность служб:** персонализированное представление со сведениями о работоспособности ваших служб Azure.
- **Работоспособность ресурса:** подробное представление со сведениями о работоспособности отдельных ресурсов.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Чтобы настроить оповещение в службе "Работоспособность служб", сделайте следующее:

1. перейдите в раздел **Работоспособность служб**.
2. Выберите **Оповещения о работоспособности**.
3. Создайте оповещение о работоспособности служб.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы настроить оповещение в службе "Работоспособность служб", перейдите на [портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

### <a name="learn-more"></a>Подробнее

Подробные сведения см. в [документации по Работоспособности служб Azure](https://docs.microsoft.com/azure/service-health).

## <a name="log-analytics"></a>Log Analytics

::: zone-end
::: zone target="chromeless"

## <a name="log-analyticstablog-analytics"></a>[Служба Log Analytics](#tab/Log-Analytics)

::: zone-end

[Рабочая область Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) — это уникальная среда для хранения данных журналов Azure Monitor. Каждая рабочая область имеет собственный репозиторий данных и конфигурацию. Источники данных и решения настраиваются для хранения данных в определенных рабочих областях. Решениям для мониторинга Azure требуется подключение всех серверов к рабочей области, чтобы их данные журналов можно было хранить и получать к ним доступ.

::: zone target="chromeless"

### <a name="action"></a>Действие

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2Fworkspaces]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Подробнее

Дополнительные сведения см. в [документации по созданию рабочей области Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace).

## <a name="azure-monitor"></a>Azure Monitor

::: zone-end
::: zone target="chromeless"

## <a name="azure-monitortabazure-monitor"></a>[Azure Monitor](#tab/Azure-Monitor)

::: zone-end

Azure Monitor предоставляет единый унифицированный концентратор для всех данных мониторинга и диагностики в Azure. С его помощью вы можете получать данные о состоянии всех ресурсов. С помощью Azure Monitor можно находить и устранять проблемы и оптимизировать производительность. Вы также можете анализировать поведение клиентов.

- **Мониторинг и визуализация метрик.** Метрики — это числовые значения, доступные в ресурсах Azure, которые помогают проанализировать работоспособность систем. Вы можете настроить диаграммы для своих панелей мониторинга и создавать отчеты с помощью книг.

- **Запросы и анализ журналов.** Журналы включают журналы действий и журналы диагностики Azure. Вы можете собирать дополнительные журналы других решений мониторинга и управления со сведениями об облачных или локальных ресурсах. Log Analytics — это центральный репозиторий для агрегирования всех этих данных. Из него вы можете выполнять запросы, которые помогут определить причины проблем или позволят визуализировать данные.

- **Настройка оповещений и действий.** Оповещения позволяют узнать о критических неполадках. Корректирующие действия можно выполнять на основе триггеров по метрикам, журналам или проблемам с работоспособностью службы. Вы можете настроить различные уведомления и действия, а также отправлять данные в средства для управления ИТ-услугами.

::: zone target="chromeless"

### <a name="action"></a>Действие

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

 Обеспечьте мониторинг:

- [Приложения](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Контейнеры](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Виртуальные машины](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Сети](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Дополнительные решения для мониторинга других ресурсов можно найти в Azure Marketplace.

Чтобы изучить данные Azure Monitor, перейдите на [портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

### <a name="learn-more"></a>Подробнее

Подробные сведения см. в [документации по Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

## <a name="onboard-solutions"></a>Подключение решений

::: zone-end
::: zone target="chromeless"

## <a name="onboard-solutionstabconfigure-solutions"></a>[Подключение решений](#tab/Configure-solutions)

::: zone-end

Чтобы включить решения, необходимо настроить рабочую область Log Analytics. Подключенные виртуальные машины Azure и локальные серверы получают решения из рабочих областей Log Analytics, к которым они подключены.

Существует два подхода для подключения:

- [использование отдельной виртуальной машины](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm);
- [использование всей подписки](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale).

В каждой статье описывается последовательность действий по подключению этих решений:

- Управление обновлениями
- Отслеживание изменений и инвентаризация
- Журнал действий Azure
- решение "Работоспособность агентов" для Azure Log Analytics;
- Оценка защиты от вредоносных программ
- Azure Monitor для виртуальных машин
- Центр безопасности Azure

Каждая из предыдущих шагов поможет настроить инвентаризацию и визуальный контроль.
