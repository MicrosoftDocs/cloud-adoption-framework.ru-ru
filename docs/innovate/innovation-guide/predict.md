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
ms.openlocfilehash: 2e8a4b21fa23eef21d0330c1f89e56fd7d56814a
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2020
ms.locfileid: "88567841"
---
<!-- cSpell:ignore ONNX -->

# <a name="innovate-with-ai"></a>Инновации с использованием ИИ

Внедряя инновации, ваша компания получит множество сведений о бизнесе и о клиентах. С помощью ИИ ваша компания может:

- прогнозировать потребности клиентов;
- автоматизировать бизнес-процессы;
- обнаруживать сведения, скрытые в неструктурированных данных;
- взаимодействовать с клиентами новыми способами для улучшения качества обслуживания.

 В этой статье описано несколько подходов к внедрению ИИ. Представленная ниже таблица поможет вам найти оптимальное решение с учетом потребностей реализации.

| Категория решения | Описание                                                                                                                              | Необходимые навыки              |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| Машинное обучение            | **Машинное обучение Azure** <br> Создавайте и развертывайте собственные модели машинного обучения, а также управляйте ими.                                                       | Специалист по обработке и анализу данных и разработчик |
| Приложения и агенты ИИ             | **Azure Cognitive Services** <br> Используйте модели ИИ, ориентированные на конкретные предметные области, для обработки визуальных данных, речи и языка, а также принятия решений. Такие модели можно настроить с использованием ваших данных. <br><br> **Служба Azure Bot** <br> Привлекайте больше клиентов, добавив ботов в приложения и на веб-сайты. | Разработчик                    |
| Интеллектуальный анализ знаний            | **Когнитивный поиск Azure** <br> Извлекайте полезные данные, скрытые в вашем содержимом, включая документы, контракты, изображения и данные других типов.      | Разработчик                    |

## <a name="machine-learning"></a>Машинное обучение

Azure предоставляет расширенные возможности машинного обучения. Создавайте, обучайте и развертывайте модели машинного обучения в облаке и на пограничных устройствах, используя Машинное обучение Azure. Ускорьте разработку моделей с помощью автоматизированного машинного обучения. Вы не ограничены в выборе средств и платформ.

См. статьи [Что такое служба "Машинное обучение Microsoft Azure"?](/azure/machine-learning/overview-what-is-azure-ml) и [Руководство. Начало работы по созданию эксперимента Машинного обучения с помощью пакета SDK для Python](/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Дополнительные сведения о формате модели с открытым кодом и среде выполнения для машинного обучения см. в документации по [ONNX Runtime](http://onnxruntime.ai).

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Специалисты по анализу и обработке данных могут использовать Машинное обучение Azure для обучения и создания моделей с использованием визуального интерфейса перетаскивания и таких языков, как Python и R. Начало работы со службой "Машинное обучение Azure":

1. На портале Azure найдите и выберите область **Машинное обучение**.

1. Щелкните **Добавить**, а затем выполните инструкции, приведенные на портале, чтобы создать рабочую область.

1. Новая рабочая область позволяет специалистам по обработке и анализу данных применять для обучения, сборки, развертывания и администрирования моделей подходы с разным объемом кода.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning resources" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к ресурсам Машинного обучения Azure на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="ai-applications-and-agents"></a>Приложения и агенты ИИ

Для создания приложений ИИ Azure предоставляет набор предварительно созданных служб ИИ, которые называются Cognitive Services. Кроме того, Azure предлагает службу-бот. С ее помощью разработчики могут создавать агенты ИИ для общения, которые повышают уровень вовлеченности клиентов и сотрудников.

### <a name="ai-applications"></a>Приложения ИИ

Службы Cognitive Services позволяют внедрять в приложения возможности ИИ для обработки визуальных данных, речи и языка. Для большинства прогнозных моделей дополнительное обучение не требуется. Эти службы полезны, если среди ваших сотрудников нет специалиста по анализу и обработке данных для обучения прогнозной модели. Для других служб требуется минимальное обучение.

Сведения о требуемом объеме обучения, а также список доступных служб для принятия решений и обработки визуальных данных, речи и языка см. в документации по [Cognitive Services](/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

#### <a name="action"></a>Действие

Начало работы с API Cognitive Services:

1. На портале Azure найдите и выберите **Cognitive Services**.

1. Нажмите кнопку **Добавить**, чтобы найти API-интерфейс Cognitive Services в Azure Marketplace.

1. Найдите и выберите службу:

    - Если вы знаете имя нужной службы, введите его в поле **Поиск в Marketplace**. Затем выберите службу.

    - Чтобы получить список API Cognitive Services, щелкните ссылку **Показать больше** рядом с заголовком **Cognitive Services**. Затем выберите службу.

1. Щелкните **Создать**, а затем выполните инструкции, приведенные на портале, чтобы подготовить службу к работе.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к Cognitive Services на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

### <a name="ai-agents"></a>Агенты ИИ

Обеспечьте более естественное взаимодействие с клиентами и повысьте уровень их вовлеченности с помощью средств для общения, которые работают на основе Bot Framework и Службы Azure Bot. Кроме того, используйте API Cognitive Services, например LUIS, QnA Maker и службу "Речь". Они помогают вашим клиентам выполнять типичные задачи, позволяя сотрудникам центра обработки вызовов сосредоточиться на более важных и сложных вопросах.

Дополнительные сведения о создании ботов см. в схеме обучения [Создание интеллектуальных ботов в Службе Azure Bot](/learn/paths/create-bots-with-the-azure-bot-service/).

#### <a name="action"></a>Действие

Начало работы со Службой Azure Bot:

1. На портале Azure найдите и выберите элемент **Службы ботов**.

1. Щелкните **Добавить**, а затем — **Бот веб-приложений** или **Регистрация каналов ботов**.

1. Нажмите кнопку **создания**. Затем выполните инструкции, приведенные на портале, чтобы подготовить службу к работе.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices]" submitText="Go to Azure Bot Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Перейдите непосредственно к Службе Azure Bot на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices).

::: zone-end

## <a name="knowledge-mining"></a>Интеллектуальный анализ знаний

Когнитивный поиск Azure помогает извлечь скрытые полезные сведения из содержимого, включая документы, изображения и мультимедиа. Вы можете выявлять закономерности и связи в содержимом, определять тональность и извлекать ключевые фразы.

<!-- docsTest:ignore "Azure Search" -->

Когнитивный поиск Azure использует тот же стек естественного языка, который используется в Bing и Microsoft Office. Сосредоточьтесь на внедрении инноваций, уделяя меньше времени обслуживанию сложного облачного решения для поиска.

Дополнительные сведения см. в статье [Что собой представляет Когнитивный поиск Azure?](/azure/search/search-what-is-azure-search)

### <a name="action"></a>Действие

Чтобы начать работу:

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
