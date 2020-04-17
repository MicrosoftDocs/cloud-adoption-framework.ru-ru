---
title: Инновации в Azure. Прогнозирование и влияние
description: Узнайте о решениях Azure для прогнозирования потребностей клиентов и интеграции прогнозов в решение, что помогает влиять на поведение клиентов.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 166c938b510959427a30cecea1c97de35032d20e
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2020
ms.locfileid: "80427003"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Руководство по инновациям Azure. Прогнозирование и влияние

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Прогнозирование и влияние

::: zone-end

Ваша инновационная компания может анализировать данные, поведение и потребности клиента. Изучение этих полезных сведений поможет прогнозировать потребности клиентов, возможно даже до того, как они сами о них узнают. В этой статье приводится несколько подходов к предоставлению прогнозных решений. В последних разделах статьи рассматриваются подходы к интеграции этих прогнозов в решение с целью повлиять на поведение клиентов.

Представленная ниже таблица поможет вам найти оптимальное решение с учетом потребностей реализации.

|Служба  |Предварительно созданные модели  |Создание и экспериментирование  |Обучение и создание с помощью Python|Необходимые навыки|
|---------|---------|---------|---------|---------|
|Azure Cognitive Services|Да|нет|нет|API и навыки разработчиков|
|Студия машинного обучения Azure|Да|Да|нет|Общее представление о прогнозных алгоритмах|
|Служба машинного обучения|Да|Да|Да|специалист по анализу и обработке данных;|

## <a name="azure-cognitive-services"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Самый быстрый и простой способ прогнозирования потребностей клиентов — использование Azure Cognitive Services. Службы Cognitive Services позволяют делать прогнозы на основе существующих моделей, что не требует дополнительного обучения. Эти службы — оптимальный и эффективный вариант, если среди ваших сотрудников нет специалиста по анализу и обработке данных для обучения прогнозной модели. Для некоторых служб обучение не требуется, в то время как для других требуется в минимальном объеме.

Список доступных служб и необходимый объем обучения см. в разделе [Требования к службам для модели данных](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Действие

Чтобы использовать API-интерфейс Cognitive Services, выполните приведенные ниже действия.

1. На [портале Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.CognitiveServices%2FAccounts) откройте раздел **Cognitive Services**.
2. Нажмите кнопку **Добавить**, чтобы найти API-интерфейс Cognitive Services в Azure Marketplace.
3. Выполните одно из приведенных ниже действий.
   - Если вы знаете имя нужной службы, введите его в поле **Поиск в Marketplace**.
   - Чтобы получить список API-интерфейсов Cognitive Services, щелкните ссылку **Подробности** рядом с заголовком Cognitive Services.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к Cognitive Services на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

## <a name="azure-machine-learning-studio"></a>[Студия машинного обучения Azure](#tab/MachineLearningStudio)

Если имеющиеся модели в Cognitive Services не совпадают с необходимым прогнозом, Студия машинного обучения Azure может предоставить способ создания нужных прогнозов, не требующий глубоких навыков по анализу данных.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

С помощью Студии машинного обучения Azure Machine вы можете создать модель и экспериментировать с нею, выполнив приведенные ниже действия.

1. На [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces) откройте **Студию машинного обучения Azure**.
2. Нажмите **Создать рабочую область Студии машинного обучения** и следуйте инструкциям на экране, чтобы создать рабочую область.

   Новая рабочая область предоставляет интерфейс перетаскивания для создания модели и проведения экспериментов с ней в качестве альтернативы углубленному обучению.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к службе "Студия машинного обучения Azure" на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces).

::: zone-end

## <a name="azure-machine-learning-service"></a>[Служба "Машинное обучение Azure"](#tab/MachineLearningService)

Служба "Машинное обучение Azure" предоставляет более системный подход на основе кода, необходимый для более глубокого обучения наборов данных клиентов. Используя такие языки, как Python, специалисты по обработке и анализу данных могут обучить, а затем собрать алгоритм для прогнозирования потребностей клиентов.

### <a name="action"></a>Действие

Специалисты по анализу и обработке данных могут использовать службу "Машинное обучение Azure" для обучения и создания модели с использованием таких языков, как Python:

1. Перейдите к **Службе машинного обучения Azure**.
2. Нажмите **Создать рабочую область Службы машинного обучения** и следуйте инструкциям на экране, чтобы создать рабочую область.
3. Новая рабочая область предоставляет специалистам по обработке и анализу данных подход на основе кода для обучения и создания моделей, которым требуется более сложная аналитика для точного прогнозирования потребностей клиентов.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к службе "Студия машинного обучения Azure" на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="influence"></a>Влияние

Все описанные выше подходы приводят к созданию API, который предоставляет модель прогнозирования для приложений. Используйте в своем решении любой из этих подходов для передачи данных, полученных от клиента, в API прогнозирования. Затем рекомендуется интегрировать результаты в пользовательский интерфейс.

Рекомендуемые дальнейшие действия помогают повлиять на привычки клиентов и их реакцию. Так как предлагаемые дальнейшие действия основаны на прогнозных алгоритмах, для прогнозирования потребностей клиентов и их удовлетворения (часто до того, как клиент сам узнает о них) используются предыдущие потребности клиентов и доступные данные.
