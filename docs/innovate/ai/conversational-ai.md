---
title: Искусственный AI
description: Для беседы Azure предлагает разработчикам службы Azure Bot и пакет SDK и инструменты для создания многофункциональных интерактивных приложений.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 835092c436f442dd9126009aee64ab54424f3e79
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/26/2020
ms.locfileid: "88878713"
---
# <a name="conversational-ai"></a>Искусственный AI

Платформа Azure искусственного интеллекта Майкрософт призвана помочь разработчикам внедрять и ускорять проекты. В частности, для общения с искусственным интеллектом Azure предоставляет разработчикам Azure Bot и пакет SDK и средства для создания многофункциональных диалоговых возможностей. Кроме того, разработчики могут использовать Cognitive Services Azure (службы искусственного интеллекта, доступные в качестве интерфейсов API), такие как Language Understanding (LUIS), QnA Maker и речь, чтобы добавить возможности чат-бот для понимания и проговаривать с конечными пользователями.

Распространенные сценарии для решений AI или чат-бот:

- Информационное сообщение Q&чат-бот
- Служба поддержки клиентов или чат-бот
- Служба технической поддержки или HR чат-бот
- Электронная коммерция или продажи чат-бот
- Устройства с поддержкой речи

> [!NOTE]
> Корпорация Майкрософт предлагает разработчикам, которые хотят создать чат-бот, в основном без кода или с небольшим кодом, на основе программы-Bot. Кроме того, разработчики не размещают робота и не контролируют естественный язык или другие модели AI с Cognitive Services.

## <a name="checklist"></a>Контрольный список

Ознакомьтесь со службой Azure Bot и Microsoft Bot Framework.

- Bot Framework — это предложение с открытым исходным кодом, которое предоставляет пакет SDK (доступен на C#, JavaScript, Python и Java) для разработки, сборки и тестирования программы Bot. Он также предлагает бесплатный холст визуальной разработки в среде Bot Framework composer и средство тестирования в эмуляторе Bot Framework.
- Служба Azure Bot — это выделенная служба в Azure, которая позволяет размещать или публиковать программу Bot в Azure и подключаться к популярным каналам.

- [Сведения о службе Azure Bot и обзоре платформы Bot](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
- [Принципы разработки ботов](/azure/bot-service/bot-service-design-principles?view=azure-bot-service-4.0)
- [Поиск последних версий пакета SDK и инструментов для платформы Bot](/azure/bot-service/what-is-new?view=azure-bot-service-4.0)

Один из самых простых способов начать работу — использовать QnA Maker, часть Cognitive Services Azure, которая позволяет интеллектуально преобразовать документ или веб-сайт с часто задаваемыми вопросами в Q&в течение нескольких минут.

- [Узнайте, как создать робот с помощью Q&возможности быстро с QnA Maker](/azure/bot-service/bot-builder-tutorial-add-qna?tabs=csharp&view=azure-bot-service-4.0)
- [Непосредственное тестирование службы QnA Maker](https://www.qnamaker.ai/)

Загрузка и использование пакета SDK и инструментов Bot Framework для разработки с помощью Bot

- [5-минутные краткие руководства по композитору платформы Bot](/composer/)
- [Сборка и тестирование программы-роботы с помощью пакета SDK для Bot Framework (C#, JavaScript, Python)](/azure/bot-service/dotnet/bot-builder-dotnet-sdk-quickstart?view=azure-bot-service-4.0)

Узнайте, как добавить Cognitive Services, чтобы сделать робот еще более интеллектуальным.

- [Руководство разработчика по созданию приложений искусственного интеллекта](https://www.oreilly.com/library/view/a-developers-guide/9781492080619/) (электронная книга)
- Дополнительные сведения о [Cognitive Services](/azure/cognitive-services/)

Узнайте, как создать собственный виртуальный помощник с помощью акселераторов решений Bot и выбрать общий набор навыков, таких как календарь, электронная почта, интересующая точка и задача.

- [Решение виртуального помощника для платформы Bot](https://microsoft.github.io/botframework-solutions/index)

## <a name="next-steps"></a>Дальнейшие шаги

[Интеллектуальный анализ знаний](./knowledge-mining.md)
