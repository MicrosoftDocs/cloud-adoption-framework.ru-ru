---
title: Общие сведения о дисциплине "Согласованность ресурсов"
description: Ознакомьтесь с подходом к разработке дисциплины "Согласованность ресурсов" в составе стратегии управления облаком.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 93064d0c3feb8b9ee129c404e58e8d0485dcdfe5
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706971"
---
# <a name="resource-consistency-discipline-overview"></a>Общие сведения о дисциплине "Согласованность ресурсов"

Согласованность ресурсов — это один из [пяти аспектов системы управления облачными ресурсами](../governance-disciplines.md) в [модели управления Cloud Adoption Framework](../index.md). Эта дисциплина направлена на создание политик, связанных с оперативным управлением рабочей средой, приложением или рабочей нагрузкой. Команды ИТ-специалистов часто выполняют мониторинг приложений, рабочей нагрузки и производительности ресурсов. Они также обычно выполняют задачи, которые поддерживают потребность в масштабировании, устраняют нарушения Соглашений об уровне обслуживания по аспектам производительности и предотвращают их, применяя автоматизированные исправления. В рамках пяти аспектов системы управления облачными ресурсами согласованность ресурсов обеспечивает согласованную настройку ресурсов для обнаружения с помощью ИТ-операций, добавление этих ресурсов в решения восстановления и возможность включения в повторяемые рабочие процессы.

> [!NOTE]
> Управление согласованностью ресурсов не заменит имеющихся ИТ-специалистов, процессов и процедур, которые позволят вашей организации эффективно управлять облачными ресурсами. Основная цель этой дисциплины — выявить потенциальные бизнес-риски и предоставить рекомендации по их снижению для ИТ-специалистов, отвечающих за управление вашими ресурсами в облаке. При разработке политик и процессов управления не забудьте привлечь соответствующих ИТ-специалистов к процессам планирования и проверки.

В этом разделе документации по Cloud Adoption Framework описано, как включить аспект согласованности ресурсов в стратегию управления облачными решениями. Основная аудитория этого руководства — облачные архитекторы вашей организации и другие участники вашей команды по управлению облачными решениями. Тем не менее решения, политики и процессы, вытекающие из этой дисциплины, должны включать привлечение соответствующих членов ИТ-команды, отвечающих за внедрение решениями по согласованности ресурсов в вашей организации и управление ими, а также обсуждение с ними связанных с этим вопросов.

Если вашей организации не хватает собственных специалистов в области стратегий согласованности ресурсов, рассмотрите возможность привлечения внешних консультантов как части этой дисциплины. Кроме того, рассмотрите возможность внедрения службы [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services) либо [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) для перехода на облачную службу, или других внешних экспертов по внедрению облачных технологий для обсуждения лучшего способа организации, отслеживания и оптимизации облачных ресурсов.

## <a name="policy-statements"></a>Правила политики

Действующие правила политики и соответствующие требования к архитектуре служат основой дисциплины согласованности ресурсов. Примеры правил политики см. в статье [Resource Consistency sample policy statements](./policy-statements.md) (Положения примера политики согласованности ресурсов). Эти примеры можно использовать в качестве отправной точки для политик системы управления организации.

> [!CAUTION]
> Примеры политик взяты из общего опыта клиентов. Чтобы лучше согласовать эти политики с конкретными потребностями системы управления облаком, выполните следующие шаги для создания правил политики, соответствующих уникальным потребностям вашей компании.

## <a name="develop-governance-policy-statements"></a>Разработка положений политики системы управления

В следующих шести пунктах показаны примеры и потенциальные варианты, которые следует учитывать при разработке системы управления согласованностью ресурсов. Используйте каждый пункт как отправную точку при принятии решений с участием команды по управлению облачными решениями и соответствующими бизнес-представителями, а также с ИТ-отделами вашей организации. Так вы сможете определить политики и процессы управления рисками, связанными с согласованностью ресурсов.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Шаблон согласованности ресурсов</h3>
                        <p class="x-hidden-focus">Скачайте шаблон для документирования дисциплины "Согласованность ресурсов".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li><li style="display: flex; flex-direction: column;">
    <a href="./business-risks.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Бизнес-риски</h3>
                        <p class="x-hidden-focus">Изучите мотивы и риски, связанные с дисциплиной "Согласованность ресурсов".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./metrics-tolerance.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Индикаторы и метрики</h3>
                        <p class="x-hidden-focus">Показатели, которые помогут понять, следует ли инвестировать в дисциплину "Согласованность ресурсов".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./compliance-processes.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Процессы, обеспечивающие соблюдение политики</h3>
                        <p class="x-hidden-focus">Здесь предложены процессы для соблюдения политики в дисциплине "Согласованность ресурсов".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./discipline-improvement.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Зрелость</h3>
                        <p class="x-hidden-focus">Согласование оптимизации управления облаком с этапами внедрения облачных технологий.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./toolchain.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Цепочка инструментов</h3>
                        <p class="x-hidden-focus">Службы Azure, которые можно использовать для поддержки дисциплины "Согласованность ресурсов".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Дальнейшие действия

Начните с оценки [бизнес-рисков](./business-risks.md) в конкретной среде.

> [!div class="nextstepaction"]
> [Описание бизнес-рисков](./business-risks.md)
