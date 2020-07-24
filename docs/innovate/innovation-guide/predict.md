---
title: Инновации в Azure. Инновации с использованием ИИ
description: Узнайте о решениях Azure для прогнозирования потребностей клиентов, автоматизируйте бизнес-процессы, извлекайте информацию, которая скрыта в неструктурированных данных, а также реализуйте новые способы общения с клиентами для предоставления лучших возможностей.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/26/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 74db213a6d03eaf3df75f8eed88260bb1e457cee
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86448866"
---
<!-- cSpell:ignore ONNX -->

::: zone target="docs"

# <a name="azure-innovation-guide-innovate-with-ai"></a>Руководство по инновациям Azure. Инновации с использованием ИИ

::: zone-end

::: zone target="chromeless"

# <a name="innovate-with-ai"></a>Инновации с использованием ИИ

::: zone-end

Внедряя инновации, ваша компания получит множество сведений о бизнесе и о клиентах. С помощью ИИ ваша компания сможет прогнозировать потребности клиентов, автоматизировать бизнес-процессы, извлекать информацию, которая скрыта в неструктурированных данных, а также реализовать новые способы общения с клиентами для предоставления лучших возможностей. В этой статье описано несколько подходов к внедрению ИИ. Представленная ниже таблица поможет вам найти оптимальное решение с учетом потребностей реализации.

| Категория решения | Описание                                                                                                                              | Необходимые навыки              |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| Машинное обучение            | **Машинное обучение Azure** <br> Создавайте и развертывайте собственные модели машинного обучения, а также управляйте ими.                                                       | Специалист по обработке и анализу данных и разработчик |
| Приложения и агенты ИИ             | **Azure Cognitive Services** <br> Используйте модели ИИ, ориентированные на конкретные предметные области, для обработки визуальных данных, речи и языка, а также принятия решений. Такие модели можно настроить с использованием ваших данных. <br><br> **Служба Azure Bot** <br> Привлекайте больше клиентов, добавив ботов в приложения и на веб-сайты. | Разработчик                    |
| Интеллектуальный анализ знаний            | **Когнитивный поиск Azure** <br> Извлекайте полезные данные, скрытые в вашем контенте, включая документы, контракты, изображения и данные других типов.      | Разработчик                    |

## <a name="machine-learning"></a>[Машинное обучение](#tab/MachineLearning)

Azure предоставляет расширенные возможности машинного обучения. Быстро и легко создавайте, обучайте и развертывайте модели машинного обучения в облаке и на пограничных устройствах, используя Машинное обучение Azure. Ускоряйте разработку моделей с помощью автоматизированного машинного обучения. Вы не ограничены в выборе средств и платформ.

См. [общие сведения о Машинном обучении Azure](https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml) и [руководстве по началу работы с первым экспериментом машинного обучения](https://docs.microsoft.com/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Дополнительные сведения о формате модели с открытым кодом и среде выполнения для машинного обучения см. в документации по [ONNX Runtime](http://onnxruntime.ai).

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Специалисты по анализу и обработке данных могут использовать Машинное обучение Azure для обучения и создания модели с использованием таких языков, как Python и R, а также визуального интерфейса перетаскивания. Начало работы со службой "Машинное обучение Azure":

1. На портале Azure найдите и выберите область **Машинное обучение**.

1. Выберите элемент **Добавить**, а затем выполните инструкции, приведенные на портале, чтобы создать рабочую область.

1. Новая рабочая область предоставляет специалистам по обработке и анализу данных как подход с малым использованием кода, так и подход на основе кода к обучению, сборке и развертыванию моделей, а также управлению ими.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning resources" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к ресурсам Машинного обучения Azure на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="ai-applications-and-agents"></a>[Приложения и агенты ИИ](#tab/AIAppsAndAgents)

Azure предоставляет набор предварительно созданных служб ИИ, которые называются Cognitive Services. Они позволяют без труда создавать приложения ИИ. Кроме того, Azure предлагает службу-бот. С ее помощью разработчики могут создавать агенты ИИ для общения, которые повышают уровень вовлеченности клиентов и сотрудников.

### <a name="ai-applications"></a>Приложения ИИ

Службы Cognitive Services позволяют внедрять в приложения возможности ИИ для обработки визуальных данных, речи и языка, а также для принятия решений без дополнительного обучения прогнозных моделей. Эти службы — оптимальный и эффективный вариант, если среди ваших сотрудников нет специалиста по анализу и обработке данных для обучения прогнозной модели. Для некоторых служб обучение не требуется, для других же нужен только минимальный курс.

Список доступных служб для обработки визуальных данных, речи и языка, а также принятия решений и сведения о требуемом объеме обучения см. в документации по [Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

#### <a name="action"></a>Действие

Начало работы с API Cognitive Services:

1. На портале Azure найдите и выберите **Cognitive Services**.

1. Нажмите кнопку **Добавить**, чтобы найти API-интерфейс Cognitive Services в Azure Marketplace.

1. Найдите и выберите службу:

    - Если вы знаете имя нужной службы, введите его в поле **Поиск в Marketplace**. Затем выберите службу.

    - Чтобы получить список API-интерфейсов Cognitive Services, щелкните ссылку **Подробности** рядом с заголовком **Cognitive Services**. Затем выберите службу.

1. Выберите элемент **Создать**, а затем выполните инструкции, приведенные на портале, чтобы подготовить службу к работе.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к Cognitive Services на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

### <a name="ai-agents"></a>Агенты ИИ

Обеспечьте более естественное взаимодействие с клиентами и повысьте уровень их вовлеченности с помощью средств для общения, которые работают на основе Bot Framework и Службы Azure Bot. Кроме того, используйте API-интерфейсы Cognitive Services, например Распознавание речи (LUIS), QnA Maker и службу "Речь", чтобы ваши клиенты могли самостоятельно выполнять распространенные задачи и агенты вашего центра обработки вызовов могли сосредоточиться на более специфических и важных аспектах.

Дополнительные сведения о создании ботов см. в схеме обучения, посвященной [Службе Azure Bot](https://docs.microsoft.com/learn/paths/create-bots-with-the-azure-bot-service/).

#### <a name="action"></a>Действие

Начало работы со Службой Azure Bot:

1. На портале Azure найдите и выберите элемент **Службы ботов**.

1. Выберите элемент **Добавить**, а затем — элемент **Бот веб-приложений** или **Регистрация каналов ботов**.

1. Выберите элемент **Создать**, а затем выполните инструкции, приведенные на портале, чтобы подготовить службу к работе.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices]" submitText="Go to Azure Bot Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к Службе Azure Bot на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices).

::: zone-end

## <a name="knowledge-mining"></a>[Интеллектуальный анализ знаний](#tab/KnowledgeMining)

Когнитивный поиск Azure помогает извлечь скрытые полезные сведения из содержимого, включая документы, изображения и мультимедиа. Это ориентированная только на облако служба поиска со встроенными возможностями ИИ. Она позволяет выявлять закономерности и связи в вашем содержимом, определять тональность, извлекать ключевые фразы и выполнять многие другие задачи.

<!-- docsTest:ignore "Azure Search" -->

Когнитивный поиск Azure (прежнее название — Поиск Azure) использует тот же интегрированный стек естественного языка Майкрософт, который Bing и Microsoft Office использовали более десяти лет, а также службы ИИ для обработки визуальных данных, языка и речи. Сосредоточьтесь на внедрении инноваций, уделяя меньше времени обслуживанию сложного облачного решения для поиска.

Дополнительные сведения см. в статье [Что собой представляет Когнитивный поиск Azure?](https://docs.microsoft.com/azure/search/search-what-is-azure-search)

### <a name="action"></a>Действие

Начало работы с Когнитивным поиском Azure:

1. На портале Azure найдите и выберите элемент **Когнитивный поиск Azure**.

1. Выполните инструкции, приведенные на портале, чтобы подготовить службу к работе.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FSearchServices]" submitText="Go to Azure Cognitive Search" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к службе "Когнитивный поиск Azure" на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FSearchServices).

::: zone-end

---
