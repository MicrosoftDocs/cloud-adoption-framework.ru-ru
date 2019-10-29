---
title: Руководство по инновациям Azure. Упрощение доступа к данным
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как упростить доступ к данным с помощью Azure.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 65c1ecd1d722286fb495af3069862131629c35d1
ms.sourcegitcommit: 0d14d89b9004a65a322724342cb5086ad2c77467
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72777086"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Руководство по инновациям Azure. Упрощение доступа к данным

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Упрощение доступа к данным

::: zone-end

Одним из первых шагов для упрощения доступа к данным является улучшение их обнаружения. Каталогизация и управление обменом данными позволяют предприятиям получить наибольшую отдачу от существующих информационных ресурсов. Благодаря каталогу данных источники данных легко обнаруживаются и являются понятными для пользователей, которые управляют данными. Каталог данных Azure обеспечивает управление внутри организации, в то время как Azure Data Share обеспечивает управление и совместное использование за пределами организации.

Службы Azure, которые обеспечивают обработку данных, например Azure Time Series Insights и Stream Analytics, — это другие возможности, которые клиенты и партнеры успешно используют для внедрения инноваций.

# <a name="catalogtabcatalog"></a>[Каталог](#tab/Catalog)

## <a name="azure-data-catalog"></a>Каталог данных Azure

Каталог данных Azure решает проблемы, связанные с обнаружением потребителей данных, а также позволяет создателям данных обслуживать информационные ресурсы. Постройте мост между ИТ и бизнесом, чтобы каждый мог внести свой вклад. Разместите ваши данные там, где вам удобно, и подключайтесь к ним с любого устройства. Управляйте списком пользователей, которые имеют доступ к зарегистрированным ресурсам данных. Интегрируйте данные с существующими средствами и процессами с помощью открытых REST API.

> [!div class="checklist"]
>
> - Зарегистрировать
> - Поиск и добавление заметок
> - Подключение и управление

::: zone target="docs"

**Перейдите к [Каталогу данных Azure](https://docs.microsoft.com/azure/data-catalog).**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Действие

В организации поддерживается только один Каталог данных Azure. Если каталог для организации уже создан, вы не сможете добавить дополнительные каталоги.

Чтобы создать Каталог данных Azure для организации, выполните следующие действия:

1. Перейдите к **Каталогу данных Azure**.
2. Нажмите кнопку **Создать** .

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Share](#tab/Share) (Предоставить общий доступ)

## <a name="azure-data-share"></a>Azure Data Share

Достижение баланса между открытым обменом данными и контролем над тем, к каким данным предоставляется общий доступ и кто его имеет, является основным движущим фактором инноваций. Несмотря на упрощение доступа к данным организации могут легко столкнуться с огромными объемами данных, быстрым темпом изменения и продолжительным жизненным циклом таких данных. С помощью Azure Data Share поставщик данных может контролировать способ обработки своих данных, определяя условия использования общего ресурса с данными. Потребитель данных должен принять эти условия, прежде чем сможет получить доступ к данным. Поставщики данных могут указать частоту, с которой их потребители данных будут получать обновления. Поставщик данных может отозвать доступ к новым обновлениям в любое время.

> [!div class="checklist"]
>
> - создать общий доступ к данным;
> - добавить наборы данных в общий доступ к данным;
> - включить расписание синхронизации для общего доступа к данным;
> - добавить получателей для общего доступа к данным.

::: zone target="docs"
**Перейдите к [Azure Data Share](https://docs.microsoft.com/azure/data-share).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Чтобы создать Azure Data Share, выполните следующие действия:

1. Перейдите к **Azure Data Share**.
2. Щелкните **Create Data Share** (Создать общий ресурс с данными).

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Share" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

Платформа [Открытые наборы данных Azure](https://docs.microsoft.com/azure/open-datasets/overview-what-are-open-datasets) позволяет улучшить анализ, включая данные о [праздниках](https://azure.microsoft.com/services/open-datasets/catalog/public-holidays), [погоде](https://azure.microsoft.com/services/open-datasets/catalog/noaa-global-forecast-system) и [пространственные изображения](https://azure.microsoft.com/services/open-datasets/catalog/hls) в модели.

Следующими шагами являются [упрощение доступа к бизнес-процессам](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/democratize-business-processes) и [расширение возможностей разработчиков-любителей](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/empower-citizen-developers).

# <a name="insightstabinsights"></a>[Аналитика](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Возможности инноваций в области работы с данными безграничны, так как они позволяют в режиме реального времени изучать потоки данных и многослойное хранилище данных и моделей временных рядов в масштабе Интернета вещей для контекстуализации необработанной телеметрии и получения аналитической информации на основе ресурсов. Вы можете обеспечить плавную и непрерывную интеграцию с другими решениями для обработки данных, выполнять анализ первопричин и обнаруживать аномалии, включая настраиваемые варианты приложений на платформе Аналитики временных рядов.

> [!div class="checklist"]
>
> - Планирование среды службы "Аналитика временных рядов".
> - Визуализация данных в обозревателе.
> - Концепция срока хранения данных.
> - Разработка и совместное использование пользовательских представлений.

::: zone target="docs"

**Перейдите к службе [Аналитика временных рядов Azure](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Действие

Чтобы создать среду службы "Аналитика временных рядов Azure":

1. Перейдите к службе **Аналитика временных рядов Azure**.
2. Щелкните **Создание среды Аналитики временных рядов**.
3. Укажите для этой среды источник событий: центр Интернета вещей или концентратор событий.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
