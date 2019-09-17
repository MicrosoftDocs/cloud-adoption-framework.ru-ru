---
title: Примеры правил политик ускорения развертывания
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Примеры правил политик ускорения развертывания
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3262157cbdb24100192c1c641346c82ec831222d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829011"
---
# <a name="deployment-acceleration-sample-policy-statements"></a>Примеры правил политик ускорения развертывания

Отдельные правила облачной политики служат рекомендациями по устранению конкретных рисков, выявленных в процессе оценки рисков. В этих правилах должна предоставляться краткая сводка по рискам и планам их устранения. Каждое определение правила должно включать следующие сведения:

- **Технический риск**. Сводная информация о риске, которому посвящена эта политика.
- **Правило политики**. Четкое описание требований политики.
- **Варианты архитектуры**. Практические рекомендации, спецификации или другие руководства, которые позволят ИТ-специалистам и разработчикам реализовать эту политику.

Следующие примеры политик относятся к общим бизнес-рискам, связанным с конфигурацией. Эти инструкции представляют собой примеры, на которые можно ссылаться при разработке заявлений политики в целях удовлетворения потребностей Организации. Эти примеры не предназначены для использования в качестве описательных, и существует несколько параметров политики для работы с каждым определенным риском. Тесно с бизнесом и ИТ-группами, чтобы определить лучшие политики для уникального набора рисков.

## <a name="reliance-on-manual-deployment-or-configuration-of-systems"></a>Зависимость от развертывания вручную или настройки систем

**Технический риск:** Вмешательство человека при развертывании или настройке увеличивает вероятность влияния человеческого фактора и снижает повторяемость и предсказуемость развертывания и настройки системы. Это также обычно приводит к более медленному развертыванию системных ресурсов.

**Правило политики**. Развертывание всех ресурсов в облаке должно выполняться с использованием шаблонов или сценариев автоматизации, если это возможно.

**Возможные варианты проектирования:** [Шаблоны Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview#template-deployment) предоставляют подход "инфраструктура как код" для развертывания ваших ресурсов в Azure. [Стандартные блоки Azure](https://github.com/mspnp/template-building-blocks/wiki) предоставляют программу командной строки и набор шаблонов Resource Manager, предназначенных для упрощения развертывания ресурсов Azure.

## <a name="lack-of-visibility-into-system-issues"></a>Отсутствие видимости системных проблем

**Технический риск:** Недостаточный мониторинг и диагностика бизнес-систем не позволяют персоналу операций выявлять и устранять проблемы до того, как произойдет сбой системы, и могут значительно увеличить время, необходимое для правильного устранения сбоя.

**Правило политики**. Будут реализованы следующие политики.

- Ключевые показатели и меры диагностики будут определены для всех производственных систем и компонентов, а инструменты мониторинга и диагностики будут применяться к этим системам и регулярно контролироваться операционным персоналом.
- При выполнении операций будут использоваться средства мониторинга и диагностики в непроизводственных средах, таких как промежуточное хранение и контроль качества, чтобы определить проблемы системы до их появления в рабочей среде.

**Возможные варианты проектирования:** [Azure Monitor](/azure/azure-monitor), который также включает Log Analytics и Application Insights, предоставляет инструменты для сбора и анализа телеметрии, чтобы помочь изучить принцип работы вашего приложения и заранее выявлять проблемы, влияющие на них, и ресурсы, от которых они зависят.

## <a name="configuration-security-reviews"></a>Проверки конфигурации системы безопасности

**Технический риск:** Со временем новые угрозы безопасности могут повысить риск несанкционированного доступа к защищенным ресурсам.

**Правило политики**. Процессы системы управления облаком должны включать ежеквартальные проверки с командами управления настройкой. Это позволит определять вредоносные субъекты и шаблоны использования, которые должны блокироваться конфигурацией облачных ресурсов.

**Возможные варианты проектирования:** Организуйте ежеквартальное совещание по рассмотрению вопросов безопасности, в котором участвуют как члены группы управления, так и ИТ-специалисты, отвечающие за настройку облачных ресурсов и приложений. Проверьте существующие данные и метрики безопасности, чтобы установить зазоры в текущей политике и средствах ускорения развертывания и обновить политику, чтобы устранить все новые риски.

## <a name="next-steps"></a>Следующие шаги

Используйте примеры, приведенные в этой статье, в качестве отправной точки для разработки политик по конкретным бизнес-рискам, соответствующих вашим планам внедрения облачных систем.

Чтобы начать создание собственных правил пользовательской политики, имеющих отношение к управлению удостоверениями, скачайте [шаблон основных способов идентификации](./template.md).

Чтобы ускорить внедрение этой дисциплины, выберите [руководство по управлению](../journeys/index.md) , которое наиболее полно соответствует вашей среде. Затем измените архитектуру с учетом принятых решений по корпоративной политике.

Основываясь на рисках и рискоустойчивости, создайте процесс управления и информирования о соблюдении политики Ускорения развертывания.

> [!div class="nextstepaction"]
> [Разработка процессов, обеспечивающих соблюдение требованиям](./compliance-processes.md)