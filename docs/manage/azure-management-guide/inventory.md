---
title: Инвентаризация и визуальный контроль в Azure
description: Изучите различные средства, которые обеспечивают как инвентаризацию, так и визуальный контроль состояния выполнения инвентаризации для сбора операционных данных.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.localizationpriority: high
ms.custom: internal, fasttrack-edit, AQC
ms.openlocfilehash: 1df00dd75d5a19488271daae19979473dc95f0b3
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102114852"
---
# <a name="inventory-and-visibility-in-azure"></a>Инвентаризация и визуальный контроль в Azure

*Инвентаризация и визуальный контроль* — это первая из трех дисциплин в базовом плане управления облаком.

![Базовый план управления облаком](../../_images/manage/management-baseline.png)

Эта дисциплина должна быть первой, так как при принятии решений об операциях важно собирать правильные рабочие данные. Команды специалистов управления облачными задачами должны понимать, какие ресурсы администрируются и насколько хорошо они работают. В этой статье рассматриваются различные средства, которые предоставляют как инвентаризацию, так и визуальный контроль состояния выполнения инвентаризации.

В следующей таблице приведены рекомендуемые минимальные средства для базового плана управления для любой среды корпоративного уровня.

| Процесс | Инструмент | Назначение |
|---|---|---|
| Мониторинг работоспособности служб Azure | [Работоспособность служб Azure](/azure/service-health/service-health-overview) | Работоспособность, производительность и диагностика служб, работающих в Azure |
| Централизованное ведение журнала | [Служба Log Analytics](/azure/azure-monitor/logs/log-analytics-overview) | Централизованное ведение журнала для всех целей визуального контроля |
| Централизованный мониторинг | [Azure Monitor](/azure/azure-monitor/overview) | Централизованный мониторинг операционных данных и тенденций |
| Инвентаризация и отслеживание изменений виртуальных машин | [Отслеживание изменений и инвентаризация](/azure/automation/change-tracking/overview) | Инвентаризация виртуальных машин и мониторинг изменений на уровне гостевой ОС |
| Мониторинг подписок | [Журнал действий Azure](/azure/azure-monitor/essentials/activity-log) | Мониторинг изменений на уровне подписки |
| Мониторинг гостевой ОС | [Azure Monitor для виртуальных машин](/azure/azure-monitor/vm/vminsights-overview) | Мониторинг изменений и производительности виртуальных машин |
| Мониторинг сетей. | [Наблюдатель за сетями Azure](/azure/network-watcher/network-watcher-monitoring-overview) | Мониторинг сетевых изменений и производительности |
| Мониторинг DNS | [Аналитика DNS](/azure/azure-monitor/insights/dns-analytics) | Безопасность, производительность и операции DNS |

::: zone target="docs"

## <a name="azure-service-health"></a>Работоспособность служб Azure

::: zone-end
::: zone target="chromeless"

## <a name="azure-service-health"></a>[Служба "Работоспособность служб Azure"](#tab/AzureServiceHealth)

::: zone-end

Работоспособность служб Azure предоставляет персонализированное представление состояния работоспособности ваших служб и регионов Azure. В службе "Работоспособность служб Azure" публикуется информация об активных проблемах, которая поможет вам определить влияние этих проблем на ваши ресурсы. Информация регулярно обновляется, и в случае решения проблем вы получаете уведомление.

Кроме того, в решении "Работоспособность служб Azure" публикуются объявления о событиях планового обслуживания, чтобы оповестить вас об изменениях, которые могут повлиять на доступность ваших ресурсов. Настройте оповещения для решения "Работоспособность служб", чтобы получать уведомления о проблемах служб, плановом обслуживании и других изменениях, которые могут повлиять на ваши службы и регионы Azure.

Служба "Работоспособность служб Azure" предоставляет такие сведения:

- **Состояние Azure:** Глобальное представление со сведениями о работоспособности служб Azure.
- **Работоспособность служб:** Персонализированное представление со сведениями о работоспособности ваших служб Azure.
- **Работоспособность ресурса:** подробное представление со сведениями о работоспособности отдельных ресурсов.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Чтобы настроить оповещение в службе "Работоспособность служб", сделайте следующее:

1. перейдите в раздел **Работоспособность служб**.
2. Выберите **Оповещения о работоспособности**.
3. Создайте оповещение службы "Работоспособности служб".

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы настроить оповещения в службе "Работоспособность служб", перейдите на [портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

### <a name="learn-more"></a>Дополнительные сведения

Дополнительные сведения см. в статье [Документация по службе "Работоспособность служб Azure"](/azure/service-health/).

## <a name="log-analytics"></a>Log Analytics

::: zone-end
::: zone target="chromeless"

## <a name="log-analytics"></a>[Служба Log Analytics](#tab/Log-Analytics)

::: zone-end

[Рабочая область Log Analytics](/azure/azure-monitor/logs/quick-create-workspace) — это уникальная среда для хранения данных журналов Azure Monitor. Каждая рабочая область имеет собственный репозиторий данных и конфигурацию. Источники данных и решения настраиваются для хранения данных в определенных рабочих областях. Решениям для мониторинга Azure требуется подключение всех серверов к рабочей области, чтобы их данные журналов можно было хранить и получать к ним доступ.

::: zone target="chromeless"

### <a name="action"></a>Действие

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2FWorkspaces]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Дополнительные сведения

Дополнительные сведения см. в [документации по созданию рабочей области Log Analytics](/azure/azure-monitor/logs/quick-create-workspace).

## <a name="azure-monitor"></a>Azure Monitor

::: zone-end
::: zone target="chromeless"

## <a name="azure-monitor"></a>[Azure Monitor](#tab/Azure-Monitor)

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

- [Приложения](/azure/azure-monitor/app/app-insights-overview)
- [Контейнеры](/azure/azure-monitor/containers/container-insights-overview)
- [Виртуальные машины](/azure/azure-monitor/vm/service-map)
- [Сети](/azure/networking/network-monitoring-overview)

Дополнительные решения для мониторинга других ресурсов можно найти в Azure Marketplace.

Чтобы изучить данные Azure Monitor, перейдите на [портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

### <a name="learn-more"></a>Дополнительные сведения

Подробные сведения см. в [документации по Azure Monitor](/azure/azure-monitor/).

## <a name="onboard-solutions"></a>Подключение решений

::: zone-end
::: zone target="chromeless"

## <a name="onboard-solutions"></a>[Подключение решений](#tab/Configure-solutions)

::: zone-end

Чтобы включить решения, необходимо настроить рабочую область Log Analytics. Подключенные виртуальные машины Azure и локальные серверы получают решения из рабочих областей Log Analytics, к которым они подключены.

Существует два подхода для подключения:

- [использование отдельной виртуальной машины](../../manage/azure-server-management/onboard-single-vm.md);
- [использование всей подписки](../../manage/azure-server-management/onboard-at-scale.md).

В каждой статье описывается последовательность действий по подключению этих решений:

- Update Management solution (Решение для управления обновлениями)
- Решение "Отслеживание изменений и инвентаризация"
- Журнал действий Azure
- решение "Работоспособность агентов" для Azure Log Analytics;
- Оценка защиты от вредоносных программ
- Azure Monitor для виртуальных машин
- Центр безопасности Azure

Каждая из предыдущих шагов поможет настроить инвентаризацию и визуальный контроль.
