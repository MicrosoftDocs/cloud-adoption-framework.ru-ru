---
title: Общие сведения об основных способах защиты
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Общие сведения об основных способах защиты
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 3d193a2fd71ffcda2b117d722603b08c27144aa3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026426"
---
# <a name="security-baseline-discipline-overview"></a>Общие сведения об основных способах защиты

Основные способы защиты — это один из [пяти аспектов системы управления облачными ресурсами](../governance-disciplines.md) в [модели управления Cloud Adoption Framework](../index.md). Безопасность является компонентом любого ИТ-развертывания, а облако создает уникальные угрозы безопасности. Многие компании следуют нормативным требованиям, из-за которых защита конфиденциальных данных становится главным приоритетом при рассмотрении облачных технологий. Выявление потенциальных угроз безопасности в облачной среде и определение процессов и процедур для устранения этих угроз должно быть приоритетом для любой команды по обеспечению ИТ-безопасности или кибербезопасности. Аспект, описывающий применение основных способов защиты, обеспечивает последовательное применение технических требований и ограничений безопасности к облачным средам по мере их развития.

> [!NOTE]
> Система управления основными способами защиты не заменяет существующие ИТ-группы, процессы и процедуры, которые ваша организация использует для защиты размещенных в облаке ресурсов. Основная цель этой дисциплины — выявить бизнес-угрозы, связанные с безопасностью, и предоставить рекомендации по их устранению ИТ-персоналу, отвечающему за инфраструктуру безопасности. При разработке политик и процессов управления не забудьте привлечь соответствующих ИТ-специалистов к процессам планирования и проверки.

В этой статье описывается подход к разработке дисциплины "Основные способы защиты" как части стратегии управления облаком. Основная аудитория этого руководства — облачные архитекторы вашей организации и другие участники вашей команды по управлению облачными решениями. Тем не менее решения, политики и процессы, вытекающие из этой дисциплины, должны включать привлечение соответствующих членов команды безопасности и ИТ-команды, особенно руководителей технических отделов, отвечающих за реализацию сетевых подключений, шифрования и служб идентификации, а также обсуждение с ними связанных с этим вопросов.

Для успеха облачных развертываний и общего успех бизнеса критически важно принимать правильные решения. Если вашей организации не хватает собственных специалистов в области кибербезопасности, рассмотрите возможность привлечения внешних консультантов по безопасности как компонента этой дисциплины. Кроме того, рассмотрите возможность внедрения службы [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services) либо [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) для перехода на облачную службу, или других внешних экспертов по внедрению облачных технологий для обсуждения проблем, связанных с этой дисциплиной.

## <a name="policy-statements"></a>Правила политики

Действующие правила политики и соответствующие требования к архитектуре служат основой дисциплины об основных способах защиты. Примеры правил политики см. в статье [Deployment Acceleration sample policy statements](./policy-statements.md) (Правила примера политики ускорения развертывания). Эти примеры можно использовать в качестве отправной точки для политик системы управления организации.

> [!CAUTION]
> Примеры политик взяты из общего опыта клиентов. Чтобы лучше согласовать эти политики с конкретными потребностями системы управления облаком, выполните следующие шаги для создания политик, соответствующих уникальным потребностям вашей компании.

## <a name="developing-security-baseline-governance-policy-statements"></a>Разработка правил политики управления основными способами защиты

В следующих шести пунктах показаны примеры и потенциальные варианты, которые следует учитывать при разработке системы управления основными способами защиты. Используйте каждый пункт как отправную точку при принятии решений с участием команды по управлению облачными решениями и соответствующими бизнес-представителями, а также с ИТ-отделами вашей организации и отделами по обеспечению безопасности. Так вы сможете определить политики и способы управления рисками, связанными с безопасностью.

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
                        <h3>Шаблон основных способов защиты</h3>
                        <p class="x-hidden-focus">Скачайте шаблон для документирования дисциплины "Основные способы защиты".</p>
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
                        <p class="x-hidden-focus">Вы должны распознать мотивы и риски, связанные с дисциплиной "Основные способы защиты".</p>
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
                        <p class="x-hidden-focus">Показатели, которые помогут понять, настало ли время для инвестиций в дисциплину "Основные способы защиты".</p>
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
                        <p class="x-hidden-focus">Здесь предложены процессы для поддержки соблюдения политики в дисциплине "Основные способы защиты".</p>
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
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Цепочка инструментов</h3>
                        <p class="x-hidden-focus">Службы Azure, которые можно использовать для поддержки дисциплины "Основные способы защиты".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Дополнительная информация

Начните с оценки бизнес-рисков в конкретной среде.

> [!div class="nextstepaction"]
> [Описание бизнес-рисков](./business-risks.md)
