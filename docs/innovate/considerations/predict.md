---
title: 'Облачные инновации: прогнозирование и влияние'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Введение в облачные инновации — прогнозирование и влияние
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 2702f1e2807bd2119117283dcb8cfc4fb567c8f5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557158"
---
# <a name="predict-and-influence"></a>Прогнозирование и влияние

В цифровой экономике есть два класса приложений: исторические и прогнозируемые. Многие клиентские потребности могут выполняться исключительно с использованием исторических данных, включая данные практически в реальном времени. В настоящее время большинство решений основное внимание уделяется статистической обработке данных. Затем они обрабатывают эти данные и совместно используют их для клиента в виде цифрового или внешнего интерфейса.

По мере того, как прогнозное моделирование станет более экономичным и легко доступным, клиентские возможности переводятся в направлении вперед, что приводит к более качественным решениям и действиям. Однако этот спрос не всегда должен приводить к прогнозному решению. В большинстве случаев историческое представление может предоставить достаточно данных, чтобы помочь клиенту принять решение самостоятельно.

К сожалению, у клиентов есть представление мйопик, которое ведет к решениям на основе их немедленной окружающей среды и сферы влияния. По мере роста параметров и принятия решений по числу и влиянию мйопик представление может не привести к удовлетворению нужд клиента. В то же время, так как гипотеза рассматривается в масштабе, компания, предоставляющая решение, может видеть тысячи или миллионы решений клиентов. Можно увидеть закономерности и влияние этих шаблонов. Прогнозная возможность — это разумная инвестиция, когда понимание этих шаблонов требуется для принятия решений, соответствующих потребностям клиентов.

## <a name="examples-of-predictions-and-influence"></a>Примеры прогнозов и влияния

Использование данных для создания прогнозов может быть продемонстрировано в различных приложениях и внешних интерфейсах.

- **Электронная коммерция:** Предлагаемые элементы являются примером прогноза. В зависимости от того, какие другие приобретены вместе, веб-сайт может предлагать продукты, которые можно добавить в корзину.
- **Скорректированная реальность:** IoT предлагает дополнительные примеры. Одно устройство на строке сборки обнаруживает подъем температуры компьютеров. На основе облачной прогнозной модели определяется способ реагирования. На основе этого прогноза другое устройство указывает на необходимость замедлит строку сборки, пока компьютер не сможет его выдать.
- **Потребительские продукты:** Сотовые телефоны, интеллектуальные дома, даже ваш автомобиль содержат некоторую степень прогнозных возможностей, предлагая действия на основе таких факторов, как расположение или время суток. При согласовании прогноза и начальной гипотезы эти прогнозы влияют на ваше поведение. Когда они становятся очень зрелыми, прогнозирование ведет к действию, например к собственному автомобильу.

## <a name="developing-predictive-capabilities"></a>Разработка прогнозных возможностей

Решения, которые постоянно предоставляют точные прогнозные возможности, обычно включают в себя пять основных характеристик: данные, аналитические сведения, закономерности, прогнозы и взаимодействия. Каждый из них необходим для разработки прогнозных возможностей. Как и для всех замечательных нововведений, для разработки прогнозных возможностей потребуется [обязательство в итерации](./index.md#commitment-to-iteration). В каждой итерации одна или несколько из следующих характеристик были бы преждевременно проверили все более сложные клиентские данные.

![Действия по прогнозированию возможностей](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Эта статья может быть применима, если гипотеза клиента, разработанная в статье [сборка с сопереживаниеом клиентов](./build.md) , содержит прогнозные возможности. Но для прогнозных возможностей требуются значительные затраты времени и энергии. Если прогнозные возможности являются [техническими пиковыми](./build.md#reduce-complexity-and-delay-technical-spikes), а не источником достижимого значения клиента, то рекомендуется отложить прогнозирование до тех пор, пока гипотеза клиента не будет проверена в масштабе.

## <a name="data"></a>Данные

Самый простой из приведенных выше характеристик — это данные. Каждая из предыдущих дисциплин для разработки цифровых инвентионс создаст данные. Эти данные могут участвовать в разработке прогнозов. Дополнительные сведения о способах получения данных в прогнозное решение см. в статьях о [демократизинг данных](./data.md) или [взаимодействии с устройствами](./devices.md).

Для предоставления прогнозных возможностей можно использовать несколько источников данных:

## <a name="insights"></a>Аналитические сведения

Эксперты в предметной области используют данные о требованиях клиентов и возможностях для разработки базового бизнес-аналитики из исследования необработанных данных. Эти аналитические сведения могут выявить вхождения требуемых вариантов поведения клиента (или другие нежелательные результаты). Во время итераций по прогнозам эти аналитические данные могут помочь в определении потенциальных корреляций, что может оказать негативное воздействие на положительные результаты. Рекомендации по включению экспертов для разработки ценных сведений см. в статье [демократизинг Data](./data.md).

## <a name="patterns"></a>Шаблоны

Человек по своей природе испытываю трудности с обнаружением закономерностей на больших объемах данных. Компьютеры были разработаны для этой цели. Машинное обучение ускоряет эту задачу с помощью обнаружения шаблонов в большом объеме данных, называемой моделью машинного обучения. Затем эти шаблоны применяются с помощью алгоритмов машинного обучения для прогнозирования того, что произойдет при введении в алгоритм нового набора точек данных.

Используя аналитику в качестве отправной точки, машинное обучение проводит обучение и применяет прогнозные модели к данным, чтобы сделать их более прописными для шаблонов данных. С помощью нескольких итераций обучения, тестирования и внедрения эти модели и алгоритмы могут точно прогнозировать будущие результаты.

[Машинное обучение Azure служба](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) — это собственное средство облака в Azure для создания и обучения моделей на основе данных. Этот инструмент также включает [Рабочий процесс для ускорения разработки алгоритмов машинного обучения](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Этот рабочий процесс можно использовать для разработки алгоритмов с помощью визуального интерфейса или Python.

Для более надежных моделей машинного обучения [службы ML в Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) предоставляют платформу машинного обучения, созданную на основе кластеров Apache Hadoop. Такой подход позволяет более детально управлять базовыми кластерами, хранилищами и узлами вычислений. Использование Azure HDInsight также обеспечивает более сложную интеграцию с помощью таких средств, как масштабируемый и Spark, для создания прогнозов на основе интегрированных и принимаемых данных, даже для работы с данными из потока. [Решение прогноза задержки рейсов](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) демонстрирует каждую из этих расширенных возможностей прогнозирования задержек рейсов на основе условий погоды. Решение HDInsight также позволяет корпоративным элементам управления, таким как безопасность данных, доступ к сети и мониторинг производительности, эксплуатацию закономерности.

## <a name="predictions"></a>Прогнозирование

После построения и обучения шаблона его можно применить с помощью интерфейсов API, которые могут делать прогнозы во время доставки цифрового опыта. Большинство этих API построены на основе хорошо обученной модели, основанной на шаблоне в данных. Но по мере того, как клиенты развертывают общие рабочие нагрузки в облаке, облачные поставщики могут предоставлять общие API-интерфейсы прогнозирования для более быстрого внедрения прогнозов.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) — пример построения ПРОГНОЗного API-поставщика облачных служб. Эта служба включает прогнозирующие API-интерфейсы для контроля содержимого, обнаружения аномалий или предложений по персонализации содержимого. Эти API готовы к использованию на основе общих шаблонов содержимого, которые корпорация Майкрософт использовала для обучения моделей. Каждый из этих интерфейсов API делает прогнозы на основе данных, которые вы передаюте в API.

[Машинное обучение Azure служба](https://docs.microsoft.com/azure/machine-learning) позволяет развертывать пользовательские алгоритмы, которые можно создавать и обучать только на основе собственных данных. Дополнительные сведения о развертывании прогнозов с помощью Машинное обучение Azure см. [здесь](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

В статье [Настройка кластеров HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) обсуждаются процессы предоставления прогнозов, разработанных для служб ML в Azure HDInsight.

## <a name="interactions"></a>Взаимодействия

После того, как прогноз станет доступен через API, можно использовать прогноз поведения клиента. Это зависит от вида взаимодействий. Взаимодействие с алгоритмом машинного обучения происходит в других цифровых или внешних интерфейсах. По мере сбора данных с помощью приложения или интерфейса эти данные выполняются с помощью алгоритмов машинного обучения. Когда алгоритм прогнозирует результат, этот прогноз может быть предоставлен обратно клиенту с помощью существующего интерфейса.

Дополнительные сведения о создании взаимодействия внутри окружающей среды см. в статье о взаимодействии в [настроенном решении](./devices.md#adjusted-reality).

## <a name="next-steps"></a>Дальнейшие действия

Исходя из знаний о [дисциплинах инноваций](./invention.md) в [методологии](./index.md) инноваций, вы знакомы с техническими инструментами, необходимыми для [создания с помощью сопереживание](./build.md).

> [!div class="nextstepaction"]
> [Сборка с помощью сопереживание](./build.md)