---
title: Обеспечение успеха клиента во время поездки на внедрение в облако
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Обеспечение успеха клиента во время поездки на внедрение в облако
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: overview
layout: LandingPage
ms.openlocfilehash: f2892dbfab86da07db2441aea7757846903ff7e9
ms.sourcegitcommit: 3669614902627f0ca61ee64d97621b2cfa585199
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2019
ms.locfileid: "73656588"
---
# <a name="enable-success-during-a-cloud-adoption-journey"></a>Включение успеха во время поездки на внедрение в облако

Инфраструктура внедрения облачных технологий — это бесплатное средство самообслуживания, которое помогает читателям выполнить различные усилия по внедрению в облако. Платформа помогает клиентам достичь успешных бизнес-задач, которые можно включить с помощью Microsoft Azure. Однако это содержимое также распознает, что читатель может решить широкие бизнес-задачи, культуру или технические проблемы, и иногда может потребоваться зависящее от облака расположение. Поэтому каждый раздел этого руководства начинается с подхода Azure-First, а затем — от теории, нейтральных к облаку, который может масштабироваться по множеству бизнес-и технических решений.

В рамках этой инфраструктуры включение — это основная тема. В следующем контрольном списке описываются фундаментальные принципы внедрения в облако, которые гарантируют успех пути внедрения как ИТ, так и бизнеса:

- **План:** Создание четких [результатов бизнеса](../strategy/business-outcomes/index.md), четко определенного [плана](../digital-estate/index.md)по работе с цифровыми разработкой и хорошо понятных невыполненных работ по [внедрению](../migrate/migration-considerations/prerequisites/migration-backlog-review.md).
- **Готово:** Обеспечьте готовность персонала с помощью [навыков и планов обучения](../ready/technical-skills.md).
- **Работают:** Определите управляемую операционную модель для программного выполнения действий в течение и долго после внедрения.
  - **[Организация](../organize/index.md):** Выровняйте людей и группы для предоставления правильных облачных операций и внедрения.
  - **Управляет:** Выровняйте правильные [дисциплины](../govern/index.md) управления, чтобы постоянно применять управление затратами, устранение рисков, соответствие требованиям и базовые показатели безопасности для всех облачных технологий.
  - **Управление:** Непрерывное [Управление](../manage/index.md) ИТ-портфелем для минимальных перерывов в работе бизнеса и обеспечения стабильной работы портфеля ИТ.
  - **Поддержка:** Выровняйте правильные [варианты партнерства и поддержки](../migrate/migration-considerations/assess/partnership-options.md).

## <a name="additional-tools"></a>Дополнительные средства

Помимо облачной инфраструктуры внедрения, корпорация Майкрософт охватывает дополнительные разделы, которые могут привести к успешному выполнению. В этой статье описываются некоторые распространенные средства, которые могут значительно улучшить успешность за пределами инфраструктуры облачного внедрения. Обеспечение управления облаком, устойчивыми архитектурами, техническими навыками и DevOps подход — это все важное в отношении успеха любых усилий по внедрению в облако. Читателям рекомендуется Закладка этой страницы как ресурс для повторного посещения в любом пути внедрения в облако.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsH">
<li style="display: flex; flex-direction: column;">
    <a href="../govern/guides/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Cloud Adoption Framework governance model" src="../_images/operational-transformation-govern-highres.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Система управления облаком</h3>
                        <p>Поймите бизнес-риски, сопоставьте эти риски с соответствующими политиками и процессами. Использование средств управления облаком и пяти дисциплин управления облаком сокращает риски и повышает вероятность успеха. Управление облаком помогает управлять затратами, создавать согласованность, улучшать безопасность и ускорить развертывание.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/framework/resiliency/overview" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Resilient architecture" src="https://docs.microsoft.com/azure/architecture/resiliency/images/redundancy.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Надежная архитектура (устойчивость)</h3>
                        <p>Процесс создания надежного приложения в облаке отличается от традиционной разработки приложений. Хотя ранее вы, возможно, приобретали оборудование более высокого уровня для вертикального масштабирования, в облачной среде вы должны выполнять горизонтальное масштабирование. Вместо того чтобы пытаться предотвратить все возможные сбои, нужно свести к минимуму воздействие сбоя каждого отдельного компонента.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="../ready/technical-skills.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Build Technical Skills" src="https://docs.microsoft.com/media/learn/Product/Learn/learningpath_graphic.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Технические навыки при создании</h3>
                        <p>Самым большим средством, помогающим в успехе внедрения в облако, является хорошо обученная группа. Изменяйте навыки существующих бизнес-и технических членов группы с помощью тематических схем обучения.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/devops/learn/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Learn DevOps" src="https://docs.microsoft.com/azure/devops/learn/_img/learn-devops.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Подход DevOps</h3>
                        <p>Преобразованное в корпорацию Майкрософт образование основано на подходе к росту языка и региональных параметров и DevOps подходу к техническому выполнению. Инфраструктура внедрения в облако внедряет обе платформы. Чтобы ускорить внедрение DevOps, ознакомьтесь с материалами Learning DevOps</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Architecture Center" src="https://docs.microsoft.com/azure/architecture/example-scenario/data/media/architecture-data-warehouse.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Центр архитектуры Azure</h3>
                        <p>Решения архитектуры, эталонные архитектуры, примеры сценариев, рекомендации и шаблоны облачного проектирования, помогающие в архитектуре решений, работающих в Azure.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://azure.microsoft.com/pricing/calculator/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Pricing Calculator" src="../_images/calculator-preview.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Калькулятор стоимости Azure</h3>
                        <p>Вычислите затраты на различные компоненты Azure, необходимые для создания или миграции выбранного решения.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Дальнейшие действия

С учетом основных возможностей облачной инфраструктуры внедрения, вероятность успеха при [переносе](./migrate.md) или внедрении [инноваций](./innovate.md) будет значительно выше.

> [!div class="nextstepaction"]
> [Миграция](./migrate.md)
>
> [Инновации](./innovate.md)
