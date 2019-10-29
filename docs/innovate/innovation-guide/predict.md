---
title: Руководство по инновациям Azure. Прогнозирование и влияние
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как прогнозировать использование Azure и влиять на него.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b2ed1b072d5226649e5248e350edfa3578978c4c
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769248"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Руководство по инновациям Azure. Прогнозирование и влияние

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Прогнозирование и влияние

::: zone-end

Ваша инновационная компания будет анализировать данные, поведение и потребности клиента. Изучение этих полезных сведений может помочь в прогнозировании потребностей клиентов, прежде чем они сами о них узнают. В этой статье приводится несколько подходов к предоставлению прогнозных решений. В следующих разделах в статье рассматриваются подходы к интеграции этих прогнозов в решение, чтобы повлиять на поведение клиентов.

Следующая таблица поможет вам найти оптимальное решение в зависимости от потребностей реализации.

|Service  |Предварительно созданные модели  |Создание и экспериментирование  |Обучение и создание с помощью Python|Необходимые навыки|
|---------|---------|---------|---------|---------|
|Cognitive Services|Yes|Нет|Нет|API и навыки разработчиков|
|Студия машинного обучения Azure|Yes|Да|Нет|Общее представление о прогнозных алгоритмах|
|Служба "Машинное обучение Azure"|Yes|Да|Yes|Специалист по анализу и обработке данных|

## <a name="azure-cognitive-servicestabcognitiveservices"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Самый быстрый и простой путь к созданию прогнозов — использование Azure Cognitive Services. Службы Cognitive Services позволяют делать прогнозы на основе существующих моделей, что не требует дополнительного обучения. Эти службы являются оптимальными, если отсутствует специалист по обработке и анализу данных для обучения прогнозной модели. Для некоторых служб обучение не требуется, в то время как для других требуется в минимальном объеме.

Список доступных служб и требуемый объем обучения см. в разделе [Service requirements for the data model](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model) (Требования к службам для модели данных).

### <a name="action"></a>Действие

Чтобы использовать API-интерфейс для Cognitive Services:

1. Перейдите к **Cognitive Services**.
2. Щелкните **Добавить +** , чтобы найти в Marketplace службу Cognitive Service.
3. Если известно имя нужной службы, можно ввести это имя в поле **Поиск в Marketplace**.
4. Кроме того, чтобы получить список Cognitive Services, щелкните ссылку **Подробности** рядом с заголовком Cognitive Services.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к Cognitive Services на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts).

::: zone-end

## <a name="azure-machine-learning-studiotabmachinelearningstudio"></a>[Студия машинного обучения Azure](#tab/MachineLearningStudio)

Если имеющиеся модели в Cognitive Services не совпадают с требуемым прогнозом, Студия машинного обучения Azure может предоставить способ создания нужных прогнозов, не требуя глубоких навыков по анализу данных.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Студию машинного обучения Azure можно использовать для создания модели и проведения экспериментов с этой моделью:

1. Перейдите к **Студии машинного обучения Azure**.
2. Щелкните **Create Machine Learning Studio Workspace** (Создать рабочую область Студии машинного обучения) и следуйте инструкциям на экране, чтобы создать рабочую область.
3. Новая рабочая область предоставляет интерфейс перетаскивания для создания модели и проведения экспериментов с ней в качестве альтернативы глубокому обучению.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к службе "Студия машинного обучения Azure" на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces).

::: zone-end

## <a name="azure-machine-learning-servicetabmachinelearningservice"></a>[Служба "Машинное обучение Azure"](#tab/MachineLearningService)

Служба "Машинное обучение Azure" предоставляет более системный подход на основе кода, необходимый для более глубокого обучения наборов данных клиентов. Используя такие языки, как Python, специалисты по обработке и анализу данных могут обучить, а затем создать алгоритм для прогнозирования потребностей клиентов.

### <a name="action"></a>Действие

Специалисты по обработке и анализу данных могут использовать службу "Машинное обучение Azure" для обучения и создания модели с использованием таких языков, как Python:

1. Перейдите к **Службе машинного обучения Azure**.
2. Щелкните **Create Machine Learning service workspaces** (Создать рабочую область Службы машинного обучения) и следуйте инструкциям на экране, чтобы создать рабочую область.
3. Новая рабочая область предоставляет специалистам по обработке и анализу данных подход на основе кода для обучения и создания моделей, которым требуется более сложная аналитика для точного прогнозирования потребностей клиентов.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces]" submitText="Go to Azure Machine Learning Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к службе "Студия машинного обучения Azure" на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces).

::: zone-end

## <a name="influence"></a>Влияние

Все описанные выше подходы приводят к созданию API, который предоставляет модель прогнозирования для приложений. Используйте в своем решении любой из этих подходов для передачи данных, полученных от клиента, в API прогнозирования. Затем рекомендуется интегрировать результаты в пользовательский интерфейс.

На следующих шагах будут сформированы шаблоны поведения клиента и выполнена попытка повлиять на реакцию клиента. Так как предлагаемые дальнейшие действия основаны на прогнозных алгоритмах, для прогнозирования потребностей клиентов и удовлетворения этих потребностей, часто до того, как клиент узнает о них, будут использоваться предыдущие клиенты и доступные данные.
