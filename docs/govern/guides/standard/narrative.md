---
title: 'Стандартное руководство для предприятий: Описание стратегии управления'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Это руководство создает вариант использования для управления во время межоблачного внедрения в облако уровня Standard.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 434a4d0238a4633210d31013e9787c3a0a92fc7a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029680"
---
# <a name="standard-enterprise-guide-the-narrative-behind-the-governance-strategy"></a>Стандартное руководство для предприятий: Описание стратегии управления

В следующем примере описывается вариант использования для управления во время [межоблачного внедрения в облако уровня Standard](./index.md). Прежде чем приступать к реализации пути, важно понимать предположения и основания, которые отражаются в этом предложении. Тогда вы сможете более точно применить стратегию управления для собственной организации.

## <a name="back-story"></a>Предыстория

Совет директоров начал год с планов по активизации бизнеса несколькими способами. Чтобы увеличить свою долю на рынке, они побуждают руководителей улучшить качество обслуживания клиентов. Они также стремятся к выпуску новых продуктов и служб, которые сделают компанию признанным лидером в этой отрасли. Совет директоров также начал параллельную реализацию инициативы по сокращению отходов и излишних затрат. Несмотря на то что действия совета директоров и руководства могут показаться пугающими, они нацелены на то, чтобы направить как можно больше средств на будущий рост.

В прошлом ИТ-директор компании был устранен от участия в этих стратегических разговорах. Тем не менее, так как перспективы развития неразрывно связаны с техническим ростом, теперь ИТ-отдел привлекается к участию, чтобы содействовать продвижению этих больших планов. От ИТ-отдела ожидают новых идей. Группа не готова к этим изменениям и, скорее всего, испытывают трудности с обучением.

## <a name="business-characteristics"></a>Характеристики бизнеса

Бизнес-профиль этой компании выглядит следующим образом:

- Все продажи и операции осуществляются в одной стране с низким процентом клиентов из других стран.
- Бизнес работает как единое подразделение, бюджет которого соответствует функциям, включая продажи, маркетинг, операции и ИТ-системы.
- В представлении руководства ИТ-системы приводят лишь к оттоку капитала и являются местом возникновения затрат.

## <a name="current-state"></a>Текущее состояние

Далее описано текущее состояние ИТ-систем и облачных операций компании.

- ИТ-команда управляет двумя размещенными средами инфраструктуры. Одна среда содержит производственные ресурсы, а вторая — ресурсы для аварийного восстановления и некоторые ресурсы для разработки и тестирования. За размещение этих сред отвечают два разных поставщика. ИТ-команда ссылается на эти два центра обработки данных как на рабочий центр и центр аварийного восстановления соответственно.
- Сначала ИТ-команда перенесла пользовательские учетные записи электронной почты в службу Office 365 в облачной среде. Это произошло полгода назад. В облаке было развернуто еще несколько других ИТ-ресурсов.
- Группы разработки приложений работают в рабочей мощности для разработки и тестирования, чтобы узнать о возможностях облака.
- Команда бизнес-аналитики экспериментирует с большими данными в облаке и управляет ими на новых платформах.
- Компания имеет слабо определенную политику, сообщающую, что личные данные клиентов и финансовые данные не могут размещаться в облаке, что ограничивает критически важные приложения в текущих развертываниях.
- Инвестиции в ИТ контролируются в основном по капитальным затратам. Эти инвестиции планируются ежегодно. В последние несколько лет инвестиции были немного большими, чем расходы на основные требования к техническому обслуживанию.

## <a name="future-state"></a>Будущее состояние

В ближайшие несколько лет ожидаются следующие изменения.

- Руководитель просматривает политику для персональных данных и финансовых данных, чтобы обеспечить будущие цели состояния.
- Команды разработки приложений и бизнес-аналитики намереваются выпустить облачные решения в рабочей среде в течение следующих 24 месяцев, основываясь на концепции взаимодействия с клиентами и использования новых продуктов.
- В этом году команда ИТ-специалистов завершит работу по удалению рабочих нагрузок аварийного восстановления в центре обработки данных аварийного восстановления, переместив 2000 виртуальных машин в облако. Ожидается, что в течение следующих пяти лет это позволит сэкономить около 25 млн долл. США.
    ![Затраты на локальные ресурсы в сравнении с Azure, демонстрирующие возврат на сумму * 25M долларов США за следующие пять лет](../../../_images/govern/calculator-small-to-medium-enterprise.png)
- Компания планирует изменить то, как она обеспечивает инвестиции, перепланируя фиксированный капитальный расход в качестве эксплуатационных расходов. Такое изменение повысит контролируемость инвестиций и ускорит другие запланированные ИТ-проекты.

## <a name="next-steps"></a>Следующие шаги

Компания разработала корпоративную политику для реализации системы управления. Корпоративная политика определяет многие технические решения.

> [!div class="nextstepaction"]
> [Описание начальной корпоративной политики](./initial-corporate-policy.md)