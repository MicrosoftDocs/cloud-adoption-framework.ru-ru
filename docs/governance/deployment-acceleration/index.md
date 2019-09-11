---
title: Общие сведения о дисциплине "Ускорение развертывания"
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Сведения об ускорении развертывания в связи с управлением облаком.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 5ae0769fd40bc88673adc031b5b1aa5c7d93d4d8
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816930"
---
# <a name="deployment-acceleration-discipline-overview"></a>Общие сведения о дисциплине "Ускорение развертывания"

Ускорение развертывания — это один из [пяти аспектов системы управления облачными ресурсами](../governance-disciplines.md) в [модели управления Cloud Adoption Framework](../index.md). Эта дисциплина сосредоточена на способах создания политики для контроля конфигурации или развертывания ресурсов. В рамках пяти аспектов управления облачными решениями ускорение развертывания отвечает за развертывание, обеспечение соответствия конфигураций и повторное использование скриптов. Эти действия можно выполнять вручную или автоматически с помощью DevOps. В любом случае политики останутся практически неизменными. По мере развития этого аспекта команда по управлению облачными решениями может работать как партнер в процессах DevOps и стратегиях развертывания, ускоряя развертывания и устраняя препятствия для внедрения облачных решений за счет применения повторно используемых ресурсов.

В этой статье описывается процесс ускорения развертывания, который происходит в компании во время планирования, разработки, внедрения и реализации облачного решения. Невозможно учесть в одном документе требования всех компаний. Поэтому каждый раздел этой статьи описывает предложенный минимум и возможные действия. Целью этих действий является создание [минимально жизнеспособного продукта для политики](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy) и разработка платформы для усовершенствования [поэтапной политики](../policy-compliance/index.md#incremental-policy-growth). Команде по управлению облачными решениями необходимо определить, какие инвестиции потребуются для выполнения этих действий, чтобы улучшить возможности по ускорению развертывания.

> [!NOTE]
> Дисциплина "Ускорение развертывания" не заменит имеющихся ИТ-специалистов, процессов и процедур, которые позволяют вашей организации выполнять эффективное развертывание и настраивать облачные ресурсы. Основная цель этой дисциплины — выявить потенциальные бизнес-риски и предоставить рекомендации по их снижению для ИТ-специалистов, отвечающих за управление вашими ресурсами в облаке. При разработке политик и процессов управления не забудьте привлечь соответствующих ИТ-специалистов к процессам планирования и проверки.

Основная аудитория этого руководства — облачные архитекторы вашей организации и другие участники вашей команды по управлению облачными решениями. Тем не менее решения, политики и процессы, вытекающие из этой дисциплины, должны включать взаимодействие и обсуждения с соответствующими участниками вашего бизнеса и ИТ-специалистами, особенно с теми, кто отвечает за развертывание и настройку облачных рабочих нагрузок.

## <a name="policy-statements"></a>Правила политики

Действующие правила политики и соответствующие требования к архитектуре служат основой дисциплины "Ускорение развертывания". Чтобы увидеть примеры правил политики, см. статью [Deployment Acceleration sample policy statements](./policy-statements.md) (Пример правил политики "Ускорение развертывания"). Эти примеры можно использовать в качестве отправной точки для политик системы управления организации.

> [!CAUTION]
> Примеры политик взяты из общего опыта клиентов. Чтобы лучше согласовать эти политики с конкретными потребностями системы управления облаком, выполните следующие шаги для создания правил политики, соответствующих уникальным потребностям вашей компании.

## <a name="developing-deployment-acceleration-governance-policy-statements"></a>Разработка правил политики управления ускорением развертывания

Следующие шесть пунктов помогут определить политики управления для контроля развертывания и настройки ресурсов в вашей облачной среде.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/governance/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Шаблон ускорения развертывания</h3>
                        <p class="x-hidden-focus">Скачайте шаблон для документирования дисциплины "Ускорение развертывания"</p>
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
                            <img src="../../_images/governance/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Бизнес-риски</h3>
                        <p class="x-hidden-focus">Вы должны распознать мотивы и риски, связанные с дисциплиной "Ускорение развертывания".</p>
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
                            <img src="../../_images/governance/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Индикаторы и метрики</h3>
                        <p class="x-hidden-focus">Индикаторы, которые помогут понять, настало ли время для инвестиций в дисциплину "Ускорение развертывания".</p>
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
                            <img src="../../_images/governance/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Процессы, обеспечивающие соблюдение политики</h3>
                        <p class="x-hidden-focus">Здесь предложены процессы для поддержки соблюдения политики в дисциплине "Ускорение развертывания".</p>
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
                            <img src="../../_images/governance/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Зрелость</h3>
                        <p class="x-hidden-focus">Сопоставление развития системы управления облаком с этапами внедрения облачных технологий.</p>
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
                            <img src="../../_images/governance/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Цепочка инструментов</h3>
                        <p class="x-hidden-focus">Службы Azure, которые могут быть использованы для поддержки дисциплины "Ускорение развертывания".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Дополнительная информация

Начните с оценки [бизнес-рисков](./business-risks.md) в конкретной среде.

> [!div class="nextstepaction"]
> [Описание бизнес-рисков](./business-risks.md)

<!-- markdownlint-enable MD033 -->
