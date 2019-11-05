---
title: Руководство по инновациям Azure. Упрощение доступа к данным
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как упростить доступ к данным с помощью Azure
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: fe7614d29ba6a6baba99cd447d65bc30e3396bec
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058532"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Руководство по инновациям Azure. Упрощение доступа к данным

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Упрощение доступа к данным

::: zone-end

Одним из первых шагов для упрощения доступа к данным является улучшение их обнаружения. Каталогизация и управление обменом данными позволяют предприятиям получить наибольшую отдачу от существующих информационных ресурсов. Благодаря каталогу данных пользователи, которые управляют данными, могут легко обнаруживать источники данных и понимать их. Каталог данных Azure обеспечивает управление внутри организации, в то время как Azure Data Share обеспечивает управление и совместное использование за пределами организации.

Среди других возможностей, которые клиенты и партнеры успешно используют для внедрения инноваций, — службы Azure, обеспечивающие обработку данных, например "Аналитика временных рядов Azure" и Stream Analytics.

# <a name="catalogtabcatalog"></a>[Каталог](#tab/Catalog)

## <a name="azure-data-catalog"></a>Каталог данных Azure

Каталог данных Azure решает проблемы, связанные с обнаружением потребителей данных, а также позволяет создателям данных обслуживать информационные ресурсы. Постройте мост между ИТ и бизнесом, чтобы каждый мог внести свой вклад. Вы можете хранить данные в нужном расположении и получать доступ к необходимым инструментам. Благодаря службе "Каталог данных Azure" вы можете контролировать разрешения на обнаружение зарегистрированных ресурсов с данными. Вы можете интегрировать данные с существующими средствами и процессами с помощью открытых REST API.

> [!div class="checklist"]
>
> - Зарегистрировать
> - Поиск и добавление заметок
> - Подключение и управление

::: zone target="docs"

**Откройте [документацию для службы "Каталог данных Azure"](https://docs.microsoft.com/azure/data-catalog)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Действие

В организации можно использовать только один экземпляр службы "Каталог данных Azure". Если каталог для организации уже создан, добавить дополнительные каталоги будет невозможно.

Чтобы создать экземпляр службы "Каталог данных Azure" для организации, выполните приведенные ниже действия.

1. Перейдите к **Каталогу данных Azure**.
2. Нажмите кнопку **Создать**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Share](#tab/Share) (Предоставить общий доступ)

## <a name="azure-data-share"></a>Azure Data Share

Достижение баланса между открытым обменом данными и контролем над тем, кому и к каким данным предоставляется общий доступ, является основным движущим фактором инноваций. Пытаясь упростить доступ к данным, организации могут легко столкнуться с огромными объемами данных, быстрым темпом изменения и продолжительным жизненным циклом таких данных. Azure Data Share гарантирует, что поставщик данных может контролировать способ обработки своих данных, определяя условия использования общего ресурса с данными. Потребитель данных должен принять эти условия, прежде чем сможет получить доступ к данным. Поставщики данных могут указать частоту, с которой их потребители данных будут получать обновления. Поставщик данных может отозвать доступ к новым обновлениям в любое время.

> [!div class="checklist"]
>
> - создать общий доступ к данным;
> - добавить наборы данных в общий доступ к данным;
> - включить расписание синхронизации для общего доступа к данным;
> - добавить получателей для общего доступа к данным.

::: zone target="docs"
**Откройте [документацию для службы Azure Data Share](https://docs.microsoft.com/azure/data-share)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Создание общего ресурса данных:

1. Откройте страницу с экземплярами службы **Azure Data Share**.
2. Нажмите **Создать общий ресурс данных**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Shares" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

Платформа [Открытые наборы данных Azure](https://docs.microsoft.com/azure/open-datasets/overview-what-are-open-datasets) позволяет улучшить анализ, включая данные о [праздниках](https://azure.microsoft.com/services/open-datasets/catalog/public-holidays) и [погоде](https://azure.microsoft.com/services/open-datasets/catalog/noaa-global-forecast-system), а также [пространственные изображения](https://azure.microsoft.com/services/open-datasets/catalog/hls) в модели.

Затем необходимо [упростить доступ к бизнес-процессам](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/democratize-business-processes) и [расширить возможности разработчиков-любителей](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/empower-citizen-developers).

# <a name="insightstabinsights"></a>[Аналитика](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Служба "Аналитика временных рядов Azure" предоставляет неограниченные возможности внедрения инноваций для данных. Она обеспечивает изучение потоков данных практически в режиме реального времени и многоуровневое хранение данных временных рядов в масштабе Интернета вещей. Она также предоставляет модели для контекстуализации необработанных данных телеметрии и получения аналитики на основе ресурсов. Вы можете обеспечить плавную и непрерывную интеграцию с другими решениями для обработки данных, выполнять анализ первопричин и обнаруживать аномалии, включая настраиваемые варианты приложений на платформе службы "Аналитика временных рядов".

> [!div class="checklist"]
>
> - Планирование среды службы "Аналитика временных рядов".
> - Визуализация данных в обозревателе.
> - Концепция срока хранения данных.
> - Разработка и совместное использование пользовательских представлений.

::: zone target="docs"

**Откройте [обзор службы "Аналитика временных рядов Azure"](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Действие

Чтобы создать среду службы "Аналитика временных рядов Azure":

1. Откройте **среды службы "Аналитика временных рядов Azure"** .
2. Нажмите **Создание среды Аналитики временных рядов**.
3. Укажите для этой среды источник событий: Центр Интернета вещей Azure или Центры событий.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
