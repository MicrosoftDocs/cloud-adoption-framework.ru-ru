---
title: Общие сведения о дисциплине базовой системы идентификации
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Описание базовый системы идентификации в отношении системы управления облаком
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: f4787feca5d25e8d7a12a2219215e47980314970
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818103"
---
# <a name="identity-baseline-discipline-overview"></a>Общие сведения о дисциплине базовой системы идентификации

Основные способы идентификации — это один из [пяти аспектов системы управления облачными ресурсами](../governance-disciplines.md) в [модели управления Cloud Adoption Framework](../index.md). Идентификатор все чаще рассматривается в качестве основного периметра безопасности в облаке, что является переходом от традиционного подхода к безопасности сети. Службы идентификации предоставляют основные механизмы, поддерживающие контроль доступа и организацию ресурсов в информационной среде, а дисциплина "Базовая система идентификации" дополняет [дисциплину "Базовая система безопасности"](../security-baseline/index.md), последовательно применяя требования проверки подлинности и авторизации в рамках усилий по принятию облака.

> [!NOTE]
> Система управления базовой идентификацией не заменяет существующие ИТ-подразделения, процессы и процедуры, которые позволяют вашей организации управлять службами идентификации и защищать их. Основная цель этой дисциплины — выявить потенциальные бизнес-риски, связанные с идентификацией, и предоставить рекомендации по их устранению для ИТ-специалистов, отвечающих за внедрение, обслуживание и эксплуатацию инфраструктуры управления идентификацией. При разработке политик и процессов управления не забудьте привлечь соответствующих ИТ-специалистов к процессам планирования и проверки.

В этом разделе документации по Cloud Adoption Framework описано, как включить аспект работы с основными способами идентификации в стратегию управления облачными решениями. Основная аудитория этого руководства — облачные архитекторы вашей организации и другие участники вашей команды по управлению облачными решениями. Тем не менее решения, политики и процессы, вытекающие из этой дисциплины, должны включать привлечение соответствующих участников ИТ-команды, отвечающих за внедрение решениями по управлению идентификацией в вашей организации и управление ими, а также обсуждение с ними связанных с этим вопросов.

Если вашей организации не хватает внутреннего опыта в области базовой системы идентификации и безопасности, рассмотрите возможность привлечения внешних консультантов в рамках этой дисциплины. Кроме того, рассмотрите возможность привлечения [служб консультирования Майкрософт](https://www.microsoft.com/enterprise/services), службы [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) по внедрению облака или других внешних экспертов по внедрению облачных технологий для обсуждения проблем, связанных с этой дисциплиной.

## <a name="policy-statements"></a>Правила политики

Действующие правила политики и соответствующие требования к архитектуре служат основой дисциплины "Базовая система идентификации". Примеры правил политики см. в [этой статье](./policy-statements.md). Эти примеры можно использовать в качестве отправной точки для политик системы управления организации.

> [!CAUTION]
> Примеры политик взяты из общего опыта клиентов. Чтобы лучше согласовать эти политики с конкретными потребностями системы управления облаком, выполните следующие шаги для создания правил политики, соответствующих уникальным потребностям вашей компании.

## <a name="developing-identity-baseline-governance-policy-statements"></a>Разработка правил политики системы управления базовой идентификацией

В следующих шести пунктах показаны примеры и потенциальные варианты, которые следует учитывать при разработке системы управления базовых способов идентификации. Используйте каждый пункт как отправную точку при принятии решений с участием команды по управлению облачными решениями и соответствующими бизнес-представителями, а также с ИТ-отделами вашей организации. Так вы сможете определить политики и способы управления рисками, связанными с идентификацией.

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
                        <h3>Шаблон базовой системы идентификации</h3>
                        <p class="x-hidden-focus">Скачайте шаблон для документирования дисциплины "Базовая система идентификации".</p>
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
                        <p class="x-hidden-focus">Вы должны распознать мотивы и риски, связанные с дисциплиной "Базовая система идентификации".</p>
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
                        <p class="x-hidden-focus">Показатели, которые помогут понять, настало ли время для инвестиций в дисциплину "Базовая система идентификации".</p>
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
                        <p class="x-hidden-focus">Здесь предложены процессы для поддержки соблюдения политики в дисциплине "Базовая система идентификации".</p>
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
                        <p class="x-hidden-focus">Службы Azure, которые можно использовать для поддержки дисциплины "Базовая система идентификации".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Дополнительная информация

Начните с оценки [бизнес-рисков](./business-risks.md) в конкретной среде.

> [!div class="nextstepaction"]
> [Описание бизнес-рисков](./business-risks.md)