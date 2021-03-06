---
title: Стратегическое влияние SAP в облаке
description: Ознакомьтесь с стратегическим влиянием SAP в облаке.
author: JefferyMitchell
ms.author: brblanch
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: think-tank
ms.openlocfilehash: 30188cdc1568a9f55e6c6dd4fd2e9504416ecc6b
ms.sourcegitcommit: 36e85ac734b184de3f29884b744ea74c81ccc72b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2021
ms.locfileid: "103442832"
---
# <a name="the-strategic-impact-of-sap-in-the-cloud"></a>Стратегическое влияние SAP в облаке

Продукты SAP формируют критически важную платформу для многих организаций. Если эти продукты основаны на бизнес-процессах Организации, зависимости от SAP можно просмотреть в портфеле. План внедрения в облако для этой платформы может напрямую и косвенно повлиять на внедрение облака для всех связанных рабочих нагрузок. Хотя SAP обычно не является первой платформой, которую Организация перемещает в облако, она может быть наиболее важной. Понимание стратегии миграции в облако SAP и целей внедрения в будущие состояния очень важно для успеха всех остальных планов внедрения в облако.

В этой статье используется [шаблон стратегии и плана](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) и другие ресурсы из облачной инфраструктуры внедрения для сбора стратегического влияния внедрения SAP в облаке.

## <a name="reasons-to-move-an-sap-platform-to-the-cloud"></a>Причины для перемещения платформы SAP в облако

SAP — это влиятельные платформа, и организации имеют несколько мотиваций для внедрения SAP в облако. Когда Организация считает облачную стратегию для SAP, для формирования планов внедрения в облако, как правило, применяются следующие мотивации:

- **Критические бизнес-события:** Клиенты часто применяют SAP в облаке, чтобы уменьшить договоры, нормативные требования, соответствие требованиям или независимости риски.

- **Мотивации миграции:** Если другие активы зависят от SAP для успешного переноса, клиенты стремятся сосредоточиться на снижении затрат, сложности или эксплуатационных издержках.

- **Мотивация инноваций:** Облако разблокирует новые возможности для SAP, чтобы расширить и предоставить средства и услуги для форматирования.

- **Требования к гибкому масштабированию инфраструктуры:** Облако обеспечивает возможность беспрепятственного масштабирования с помощью инфраструктуры в рамках бизнес-преобразования с помощью SAP S/4HANA.

Клиентам SAP часто назначены все четыре категории. Для успешной реализации платформы SAP в облаке необходимо, чтобы группа облачных стратегий (в том числе бизнес-руководителей и ИТ) просмотрела и назначит приоритеты, перечисленные в области " [мотивация облака](../../strategy/motivations.md)". Эти входные данные помогут группе внедрения облачных решений принимать взвешенные решения на протяжении всего процесса реализации.

Причины внедрения платформы SAP в облако часто основываются на стратегических задачах Организации. Следующие разделы предназначены для вашей организации, если ваша команда просматривает этот сценарий внедрения:

1. Циклы обновления инфраструктуры SAP потребовали значительных капитальных затрат. Если ваша инфраструктура SAP вызвана обновлением, то преимущества внедрения облака могут разблокировать своевременные стратегии, чтобы снизить затраты.

1. SAP, охватывающие контракты, блокируются поставщиками в течение нескольких лет. Если управление размещением, управляемой службой или контрактами на обслуживание приближается к продлению, некоторые возможности внедрения в облако и их преимущества предназначены для улучшения гибкости, разблокировки новых нововведений и оптимизации операций для наиболее важных платформ.

1. Обновления и обновления контракта могут активироваться циклами обновления SAP или бизнес-драйвером, который можно расширить на HANA, SAP Business Suite или другие функции SAP. Если ваша организация пытается расширить возможности SAP, внедрение облачных решений предоставит возможности для снижения затрат, внедрения инноваций, оптимизации и повышения гибкости.

## <a name="how-to-measure-progress-during-an-sap-adoption"></a>Измерение хода выполнения во время внедрения SAP

Когда вы понимаете основные причины этого сценария, Группа облачных стратегий может определить измеримые результаты для дальнейших действий по внедрению. Примеры бизнес-результатов, часто встречающихся во время внедрения облака, можно просмотреть в статье о [результатах бизнеса](../../strategy/business-outcomes/index.md).

Учитывая влияние платформы SAP, необходимо определить ряд определенных целей и измеряемых ключевых результатов. Как правило, Окрс, цели и ключевые результаты могут помочь разорвать внедрение SAP на управляемые усилия. Прочитайте [цели и основные результаты](../../strategy/business-outcomes/okr.md) , чтобы понять окрс более подробно.

## <a name="how-to-build-a-business-justification-for-cloud-migration"></a>Создание делового обоснования для миграции в облако

[Создание делового обоснования для миграции в облако](../../strategy/cloud-migration-business-case.md) может развеять ряд общих мифы для финансового плана команды. Однако вашей группе финансового отдела может потребоваться разработать подробную финансовую модель, чтобы учитывать перемещение элементов, связанных с внедрением SAP в облаке.

В [Forresterе об общем экономической влиянии Microsoft Azure для SAP](https://azure.microsoft.com/resources/sap-on-azure-forrester-tei/) предусмотрен анализ, в котором следующие обоснования обычно защищаются:

- Преимущества для льгот на рынке свыше $3 000 000 долларов США
- При предотвращении затрат превышен $7 000 000 долл. США
- 102-процент рентабельности инвестиций
- Оплата за девять месяцев

Фактические возвращаемые значения, скорее всего, будут отличаться для отдельных клиентов. Однако таблицы в Forresterном исследовании могут захватывать финансовые данные организации для проверки и деятельности по обоснованиям.

Изучите, что начальное Деловое обоснование — это оценка направления, которая может помочь в оценке стратегического выравнивания. Ваша организация может создать прозрачность между группой облачных стратегий и другими заинтересованными лицами, подтверждая, что это обоснование может значительно измениться во всех действиях по планированию. Ищите согласие, что достаточно ценности для [сбора данных инвентаризации и разработки плана](./plan.md). После того как ваше цифровое пространство будет соустановлено и оценено, вы сможете уточнить обоснование и предоставить более четкие планы для финансовых возвратов.

## <a name="next-step-plan-for-an-sap-cloud-adoption-in-azure"></a>Следующий шаг: планирование внедрения SAP в облаке в Azure

В следующих статьях приводятся указания по конкретным точкам в процессе внедрения в облако, которые помогут вам в освоении SAP в Azure.

- [Планирование внедрения SAP в облаке в Azure](./plan.md)
- [Проверка среды или целевых зон Azure](./ready.md)
- [Перенос платформы SAP в Azure](./migrate.md)
- [Новаторство с помощью SAP](./innovate.md)
- [Управление SAP](./manage.md)
