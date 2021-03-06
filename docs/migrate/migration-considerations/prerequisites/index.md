---
title: Предварительные требования для миграции
description: Ознакомьтесь с предварительными требованиями, которые помогут вам подготовиться к миграции в облако и избежать распространенных причин сбоев при миграции.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: internal
ms.openlocfilehash: 9e4f6b71d63c8246551f96e624c8415c6554c68e
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101788765"
---
# <a name="prerequisites-for-migration"></a>Предварительные требования для миграции

Перед началом любой миграции необходимо подготовить к предстоящим изменениям целевую среду для миграции. В нашем примере *средой* считается техническая облачная платформа. Кроме того, она определяется существующей бизнес-средой и образом мышления, который стал основой для принятия решения о миграции. Аналогичным образом сюда относится и культура работы в тех командах, которые реализуют изменения и пользуются их результатами. Недостаток подготовки к таким изменениям является самой распространенной причиной проблем с миграцией. В этой серии статей описано, как обеспечить соответствие требованиям к подготовке среды.

## <a name="objective"></a>Назначение

Обеспечение деловой, культурной и технической готовности перед началом реализации итеративного плана миграции.

## <a name="review-business-drivers"></a>Оценка бизнес-факторов

Прежде чем начинать миграцию в облако, изучите [методику планирования](../../../plan/index.md) и [методику подготовки](../../../ready/index.md) в Cloud Adoption Framework, чтобы правильно подготовить свою организацию к внедрению облака и миграции. В частности, изучите бизнес-требования и предполагаемые результаты, которые определяют потребность в миграции.

- [Начало работы. Ускорение миграции](../../../get-started/migrate.md)
- [Почему мы переходим к облаку?](../../../strategy/motivations.md)

## <a name="definition-of-done"></a>Определение готовности

Предварительные требования считаются выполненными, если справедливы следующие условия:

- **Готовность бизнеса.** Команда по вопросам облачной стратегии определила общие элементы и приоритеты предстоящих работ по миграции, описывающие цифровые активы для переноса в период двух-трех очередных выпусков продукта. Команда по вопросам облачной стратегии и команда по внедрению облачных решений согласовали начальную стратегию по управлению изменениями.
- **Культурная готовность.** Согласованы роли, обязанности и ожидания команды по внедрению облачных решений, команды по вопросам облачной стратегии и всех затронутых пользователей в отношении рабочих нагрузок, которые будут перенесены в период двух-трех очередных выпусков продукта.
- **Техническая готовность.** Зона размещения (или выделенное место размещения в облаке), куда будут переноситься ресурсы, соответствует минимальным требованиям для размещения первой рабочей нагрузки.

> [!CAUTION]
> Подготовка является ключом к успеху миграции. Но при этом слишком тщательная подготовка может привести к *аналитическому параличу*. Так называют ситуацию, в которой затраты времени на планирование серьезно задерживают реальные действия по переносу. Описанные в этой статье процессы и требования призваны помочь вам в принятии решений, но не позволяйте им мешать реальной работе.
>
> Выберите для первоначальной миграции относительно простую рабочую нагрузку. Используйте процессы, описанные в этой статье, при планировании и реализации этой первой миграции. Выполнение первой миграции позволит вашей команде быстро понять основные принципы работы с облаком и вынудит более тщательно разобраться в нем. Благодаря приобретенному опыт ваша команда сможет выполнять более крупные и сложные миграции.

## <a name="accountability-during-prerequisites"></a>Ответственность на период определения предварительных требований

За готовность на этапе выполнения предварительных требований отвечают две команды:

- **Команда по вопросам облачной стратегии**. Она отвечает за подбор и определение приоритетности для двух-трех рабочих нагрузок, которые будут лучшими кандидатами для миграции.
- **Команда по внедрению облачных решений**. Она отвечает за проверку готовности технический среды и оценку возможности миграции для предложенных рабочих нагрузок.

По каждому из трех определений готовности, которые мы определили в предыдущей статье, должен быть назначен один ответственный от каждой команды.

## <a name="responsibilities-during-prerequisites"></a>Обязанности на период определения предварительных требований

Помимо ответственности на обобщенном уровне, некоторые действия необходимо напрямую закрепить за конкретным исполнителем или группой. Ниже приведены примеры обязанностей, влияющих на эти действия:

- **Приоритеты бизнеса.** Обеспечьте принятие бизнес-решений по переносу рабочих нагрузок и по общим временным рамкам. См. дополнительные сведения о [причинах для миграции к облаку](../../../strategy/motivations.md).
- **Готовность к управлению изменениями.** Разработайте план отслеживания технических изменений на период миграции и проинформируйте о нем все заинтересованные стороны.
- **Согласование с бизнес-пользователями.** Разработайте план подготовки сообщества бизнес-пользователей к выполнению миграции.
- **Инвентаризация и анализ цифровых активов.** Применение инструментов для инвентаризации и анализа цифровых активов. См. подробнее в обсуждении [цифровых активов](../../../digital-estate/index.md) на сайте Cloud Adoption Framework.
- **Готовность к внедрению облака.** Оцените целевую среду развертывания и убедитесь, что она соответствует всем требованиям для нескольких первых рабочих нагрузок. См. [руководство по настройке Azure](../../../ready/azure-setup-guide/index.md).

В остальных статьях этой серии мы поможем вам разобраться с каждым из этих элементов.

## <a name="next-steps"></a>Дальнейшие действия

Вооружившись общим пониманием предварительных требований, вы теперь готовы взяться за первое из них: [ранние решения по миграции](./decisions.md).

> [!div class="nextstepaction"]
> [Ранние решения по миграции](./decisions.md)
