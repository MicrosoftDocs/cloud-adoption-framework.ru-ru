---
title: Обзор дисциплины "Управление затратами"
description: Ознакомьтесь с подходом к разработке дисциплины "Управление затратами" в составе стратегии управления облаком.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 4b0d1c727a0b224071d008e82af16a142e98d60a
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220742"
---
# <a name="cost-management-discipline-overview"></a>Обзор дисциплины "Управление затратами"

Управление затратами — это одна из [пяти дисциплин системы управления облачными ресурсами](../governance-disciplines.md) в [модели управления Cloud Adoption Framework](../index.md). Для многих клиентов управление затратами считается серьезной проблемой при внедрении облачных технологий. Найти баланс между требованиями к производительности, скоростью внедрения и затратами на облачные службы может оказаться сложной задачей. Это особенно важно во время основных бизнес-преобразований, которые реализуют облачные технологии. В этом разделе описывается подход к разработке дисциплины "Управление затратами" как части стратегии системы управления облаком.

> [!NOTE]
> Дисциплина "Управление затратами" не заменяет имеющиеся бизнес-отделы, методы учета и процедуры, задействованные в финансовом управлении ИТ-затрат организации. Этот аспект отвечает за определение потенциальных рисков для облачных ресурсов, связанных с ИТ-затратами, и предоставление рекомендаций по их устранению для бизнес-команд и ИТ-отделов, ответственных за развертывание облачных решений и управление ими.

Основная аудитория этого руководства — облачные архитекторы вашей организации и другие участники вашей команды по управлению облачными решениями. Тем не менее решения, политики и процессы, вытекающие из этой дисциплины, должны включать взаимодействие и обсуждения с соответствующими членами ваших бизнес- и ИТ-отделов, особенно с теми, кто отвечает за владение, управление и оплату за использование облачных рабочих нагрузок.

## <a name="policy-statements"></a>Правила политики

Действующие правила политики и соответствующие требования к архитектуре служат основой дисциплины "Управление затратами". Примеры правил политики см. в статье [Примеры правил политики Управления затратами](./policy-statements.md). Эти примеры можно использовать в качестве отправной точки для политик системы управления организации.

> [!CAUTION]
> Примеры политик взяты из общего опыта клиентов. Чтобы лучше согласовать эти политики с конкретными потребностями системы управления облаком, выполните следующие шаги для создания правил политики, соответствующих уникальным потребностям вашей компании.

## <a name="develop-governance-policy-statements"></a>Разработка положений политики системы управления

Следующие шесть шагов помогут вам определить политики системы управления для контроля затрат в вашей среде.

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
                        <h3>Шаблон дисциплины "Управление затратами"</h3>
                        <p class="x-hidden-focus">Скачайте шаблон для документирования дисциплины "Управление затратами".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
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
                        <p class="x-hidden-focus">Изучите мотивы и риски, связанные с дисциплиной "Управление затратами".</p>
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
                        <p class="x-hidden-focus">Показатели, которые помогут понять, следует ли инвестировать в дисциплину "Управление затратами".</p>
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
                        <p class="x-hidden-focus">Здесь предложены процессы для соблюдения политики в дисциплине "Управление затратами".</p>
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
                        <p class="x-hidden-focus">Службы Azure, которые можно использовать для поддержки дисциплины "Управление затратами".</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Дальнейшие действия

Начните с оценки бизнес-рисков в конкретной среде.

> [!div class="nextstepaction"]
> [Описание бизнес-рисков](./business-risks.md)

<!-- markdownlint-enable MD033 -->
