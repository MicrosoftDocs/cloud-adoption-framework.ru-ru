---
title: Пять аспектов управления облаком
description: Используйте платформу внедрения облачных технологий для Azure, чтобы узнать об управлении затратами, ускорении развертывания, базовом удостоверении, согласованности ресурсов и базовом плане безопасности.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: c1c54d7587bf73f5c9348c878caea7ae7cde89ae
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220198"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Пять аспектов управления облаком

<!-- docsTest:disable TODO -->
<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsI">
    <li style="display: flex; flex-direction: column;">
        <div class="cardSize">
            <div class="cardPadding" style="padding-bottom:10px;">
                <div class="card" style="padding-bottom:10px;">
                    <div class="cardText" style="padding-left:0px;">
Любое изменение бизнес-процессов или технологических платформ создает риск. Группы управления облаком, члены которых иногда называются Cloud хранителей, являются решениями для устранения этих рисков и обеспечения минимального перерыва для внедрения или внедрения инноваций.
    <br>
    <br>
Модель управления инфраструктурой внедрения в облаке помогает принимать решения (независимо от выбранной облачной платформы), сосредоточенные на <a href="./corporate-policy.md">разработке корпоративной политики</a> и <a href="#disciplines-of-cloud-governance">пяти дисциплинах управления облаком</a>. <a href="./guides/index.md">Практические руководства по проектированию</a> демонстрируют эту модель с помощью служб Azure. Узнайте о дисциплинах в модели управления облачной инфраструктуры внедрения.
                    </div>
                </div>
            </div>
        </div>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="../_images/operational-transformation-govern-highres.png" style="display: flex; flex-direction: column; flex: 1 0 auto;">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardText" style="padding-left:0px;">
    <img src="../_images/operational-transformation-govern-highres.png" alt="Diagram of the Cloud Adoption Framework governance model: Corporate policy and governance disciplines">
    <br>
    <i>Рис. 1. схема корпоративной политики и пяти дисциплин управления облаком.</i>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="disciplines-of-cloud-governance"></a>Дисциплины управления облаком

С любой облачной платформой существуют распространенные дисциплины управления, которые помогают сообщать о политиках и выровняйте цепочек инструментов. Эти дисциплины помогут принять решения о правильном уровне автоматизации и применении корпоративной политики для облачных платформ.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsA">
<li style="display: flex; flex-direction: column;">
    <a href="./cost-management/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/cost-management.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Управление затратами</h3>
                        <p>Стоимость является основной проблемой пользователей облака. Разработайте политику контроля затрат для всех облачных платформ.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./security-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/security-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Основные способы защиты</h3>
                        <p>Безопасность — это сложная тема, уникальная для каждой компании. После установки требований безопасности политики управления облаком и принудительное применение применяют эти требования в конфигурациях сети, данных и ресурсов.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./identity-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/identity-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Основные способы идентификации</h3>
                        <p>Несоответствия в применении требований к удостоверению могут увеличить риск нарушения. В соответствии с планом основы удостоверений основное внимание уделяется обеспечению единообразного применения удостоверения в рамках внедрения в облако.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./resource-consistency/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/resource-consistency.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Согласованность ресурсов</h3>
                        <p>Облачные операции зависят от конфигурации непротиворечивого ресурса. Используя средства управления, можно постоянно настраивать ресурсы для управления рисками, связанными с подключением, отсмещением, обнаружением и восстановлением.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./deployment-acceleration/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/deployment-acceleration.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Ускорение развертывания</h3>
                        <p>Централизованное развертывание, стандартизация и согласованность в подходах к развертыванию и настройке улучшают методики управления. При обеспечении с помощью средств управления на основе облака они создают облачный фактор, который может ускорить действия по развертыванию.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->
