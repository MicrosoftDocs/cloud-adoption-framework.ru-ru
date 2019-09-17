---
title: Миграция в облако
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Миграция в облако с помощью Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: 982451c9043f775c2e211d9b166ca2d094479ca9
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816403"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Миграция в облако с помощью Cloud Adoption Framework

Любой корпоративный [план внедрения в облако](../plan/index.md) будет включать рабочие нагрузки, которые не обязательно будут значительным образом использоваться при создании бизнес-логики. Эти рабочие нагрузки можно перенести в облако, используя столько подходов (lift-and-shift, lift-and-optimize или modernize), сколько вам нужно. Каждый из этих подходов считается переносом. Следующие задачи помогут определить итеративные процессы для оценки, миграции, оптимизации, а также защиты этих рабочих нагрузок и управления ими.

## <a name="getting-started"></a>Начало работы

Чтобы подготовиться к этому этапу жизненного цикла миграции в облако, ниже представлена последовательность из пяти задач.

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/prerequisites.md?tabs=Checklist">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Требования к миграции</h3>
Разверните и подготовьте зону для размещения нескольких первых рабочих нагрузок, которые будут перенесены в Azure. Создайте стратегию и план внедрения в облако.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Перенос первой рабочей нагрузки</h3>
Используйте руководство по миграции Azure для переноса первой рабочей нагрузки. Там описаны средства и подходы, используемые в процессе переноса.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./expanded-scope/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Расширенные сценарии миграции</h3>
Используйте расширенный контрольный список, чтобы определить сценарии, для которых может потребоваться изменить будущие решения, связанные с архитектурой состояния, процессами миграции, конфигурацией зоны размещения или самим процессом миграции.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Рекомендации</h3>
Внесите требуемые изменения в соответствии с рекомендациями, чтобы обеспечить правильную реализацию стратегии миграции с учетом расширенной области или рабочей нагрузки либо архитектуры.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/5.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Улучшение процессов</h3>
Миграция — это интенсивный процесс. По мере его выполнения используйте соответствующие рекомендации для оценки и отладки различных аспектов.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="iterative-migration-process"></a>Итеративный процесс миграции

По существу, миграция в облако состоит из четыре простых этапов: оценка, миграция, оптимизация, а также защита и управление. В этом разделе документации CAF описано, как повысить рентабельность на каждом из этапов процесса и сопоставить эти этапы с планом внедрения в облако. Все эти этапы итеративного процесса представлены ниже.

![Модель миграции Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

## <a name="creating-a-balanced-cloud-portfolio"></a>Создание сбалансированного портфеля облачных решений

В сбалансированном портфеле технологий всегда будут очень разные ресурсы в разных состояниях. Часть приложений уже устарела и почти не поддерживается. Другие приложения или ресурсы находятся на этапе обслуживания, но уже не развиваются. Для новых бизнес-процессов изменение рыночных условий диктует необходимость в постоянных улучшениях и модернизации. Когда возникает возможность создать новый поток дохода, в среду включаются новые приложения или ресурсы. На разных этапах жизненного цикла ресурса влияние инвестиций на доход и прибыль будет разным. Чем более поздний этап жизненного цикла проходит приложение, тем меньше возможностей получить доход от внедрения новых функций или модернизации.

Облако предоставляет несколько механизмов внедрения со сходным соотношением показателей инвестиций и рентабельности. Создание облачных приложений может значительно снизить эксплуатационные расходы. После выпуска облачного приложения можно существенно ускорить циклы разработки новых функций и решений. Модернизация приложения также предоставляет аналогичные преимущества, избавляя от устаревших ограничений, связанных с локальными моделями разработки. К сожалению, эти два подхода довольно трудоемки и зависят от числа доступных разработчиков, их навыков и опыта. Зачастую усилия можно прикладывать более эффективно — способные разработчики с навыками модернизации приложений с большей долей вероятности будут создавать новые приложения. В условиях ограничений для реализации крупномасштабных проектов модернизации не всегда найдется нужное число опытных и мотивированных сотрудников. При сбалансированном портфеле модернизацию лучше использовать только для тех приложений, для которых в локальной версии были запланированы существенные улучшения.

## <a name="envision-an-end-state"></a>Определение целевого состояния

Для эффективного преобразования должно быть определено целевое состояние. Следует хотя бы примерно представлять себе целевое состояние, прежде чем делать первый шаг. На этом изображении представлено исходное состояние с существующими приложениями, данными и инфраструктурой, которое определяет состояние цифровых активов. В ходе миграции к каждому активу применяется один из вариантов, представленных справа.

## <a name="migration-implementation"></a>Реализация миграции

В этих статьях описываются две стратегии со сходными целями — миграция в Azure большой доли существующих ресурсов. Но бизнес-результаты и текущее состояние существенно влияют на выбор процессов для достижения этой цели. Здесь небольшие отклонения привели к двум радикально отличающимся подходам к достижению сходного целевого состояния.

![Модель миграции Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

Эта модель управляет процессом добавочных изменений для достижения целевого состояния, разделяя миграцию на две основные составляющие.

**Подготовка к миграции**. Определите примерный список предстоящих работ с учетом текущего состояния и требуемых результатов.

- **Бизнес-результаты**. Ключевые бизнес-цели, ради которых выполняется миграция.
- **Оценка цифровых активов**. Приблизительная оценка числа и состояния рабочих нагрузок, которые предстоит перенести.
- **Роли и обязанности**. Четкое определение структуры групп, распределения обязанностей и прав доступа.
- **Требования к управлению изменениями.** Периодичность, процессы и документация, требуемые для оценки и утверждения изменений.

Эти входные данные определяют объем невыполненной работы по миграции. Анализ этих данных позволяет составить ранжированный список приложений, которые будут переноситься в облако. Этот список определяет методы и процессы миграции в облако. Со временем он будет увеличиваться за счет документации, требуемой для управления изменениями.

**Процесс миграции**. Каждое действие миграции в облако относится к одному из перечисленных ниже процессов в соответствии со списком невыполненных работ по миграции.

- **Оценка**. Оцените существующий ресурс и составьте для него план миграции.
- **Миграция**. Реплицируйте функции ресурса в облако.
- **Оптимизация**. Определите для облачного ресурса баланс между производительностью, стоимостью, доступностью и оперативной емкостью.
- **Защита и управление**. Подготовьте облачный ресурс к текущей эксплуатации.

Сведения, собранные при подготовке списка невыполненных работ по миграции, определяют сложность и объем усилий, которые потребуются при миграции в облако в рамках каждой итерации и для каждого нового выпуска функций.

## <a name="transition-to-the-end-state"></a>Переход к целевому состоянию

Целью является плавная и частично автоматизированная миграция в облако. В ходе миграции используются средства, предоставляемые поставщиком облачных технологий, для быстрой репликации и подготовки к работе ресурсов в облаке. После проверки пользователи перенаправляются в облачное решение путем внесения простого изменения сетевых параметров. Для многих сценариев доступны технологии, позволяющие добиться такой цели. Некоторые примеры демонстрируют впечатляющую скорость, с которой можно реплицировать в Azure десять тысяч виртуальных машин.

Но в любом случае требуется поэтапный подход к миграции. В большинстве сред для успешной миграции следует разделить длинный список переносимых виртуальных машин на небольшие блоки. Многие факторы могут ограничить число виртуальных машин, которые можно перенести за определенный период. Исходящая скорость сетевого подключения — один из таких примеров технических ограничений. Большая же их часть определяется способностью бизнеса проверять изменения и адаптироваться к ним.

Поэтапный подход к миграции, используемый в Cloud Adoption Framework, помогает создать последовательный план с учетом и описанием всех технических и культурных ограничений. Эта модель ускоряет миграцию и одновременно снижает издержки этого процесса для ИТ-отдела и бизнеса в целом. Ниже представлены два примера поэтапной миграции, выполняемой на основе списка невыполненных работ по миграции.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./azure-migration-guide/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Руководство по миграции в Azure</h3>
                        <p><b>Сводка.</b> Клиент выполняет миграцию виртуальных машин числом не более 1000. Менее десяти поддерживаемых приложений, принадлежат владельцу приложения, а не ИТ-отделу организации. Всеми остальными приложениями, виртуальными машинами и данными для них управляют члены группы по внедрения облачных решений. Члены этой группы имеют административный доступ к рабочим средам в существующем центре обработки данных.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./expanded-scope/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Руководство для сложного сценария</h3>
                        <p><b>Сводка.</b> Клиент выполняет миграцию, которая сложным образом влияет на весь его бизнес, культуру и технологии. Это руководство описывает несколько конкретных проблем, связанных со сложностью, и способы их решения.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

Эти две стратегии представляют крайние варианты для клиентов, которые собираются вложить средства и ресурсы в миграцию в облако. Большинство компаний использую элементы, взятые из обоих вариантов. Ознакомившись со стратегией развития, примените модель миграции Cloud Adoption Framework, чтобы организовать обсуждение вопросов, связанных с миграцией, и измените базовую стратегию с учетом конкретных потребностей.

## <a name="next-steps"></a>Дополнительная информация

Выберите одну из стратегий развития:

> [!div class="nextstepaction"]
> [Руководство по миграции в Azure](./azure-migration-guide/index.md)
>
> [Руководство по расширенному сценарию миграции](./expanded-scope/index.md)