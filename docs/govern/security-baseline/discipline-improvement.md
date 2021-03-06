---
title: Улучшения дисциплины "Базовая система безопасности"
description: Изучите потенциальные задачи, которые компания выполняет для разработки и развития базовой специализации в области безопасности на каждом этапе внедрения облака.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: 35441db19fb468e1f993e9e8ca6029975db5f2a5
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101792403"
---
# <a name="security-baseline-discipline-improvement"></a>Улучшения дисциплины "Базовая система безопасности"

В плане безопасности основное внимание уделяется способам установки политик, защищающих сеть, активы и наиболее важный объем данных, которые будут находиться в решении поставщика облачных решений. В рамках пяти дисциплин управления облаком базовая дисциплина безопасности включает классификацию цифрового пространства и данных. Она также содержит документацию о допустимости в рамках бизнес-деятельности, рисках и стратегиях их устранения, связанных с безопасностью данных, ресурсов и сети. С технической точки зрения это также касается принятия решений о [шифровании](../../decision-guides/encryption/index.md), [требованиях к сети](../../decision-guides/software-defined-network/index.md), [стратегиях гибридной идентификации](../../decision-guides/identity/index.md)и [процессах](./compliance-processes.md) , используемых для разработки базовых политик безопасности для облака.

В этой статье описаны задачи, которые компания может выполнить для развития и совершенствования дисциплины "Базовая система безопасности". Эти задачи можно разделить на этапы планирования, создания, внедрения и реализации облачного решения. Итеративное выполнение этих этапов позволяет разработать [поэтапный подход к системе управления облаком](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Этапы инкрементного подхода к управлению облаком ](../../_images/govern/adoption-phases.png)
 *рис. 1. этапы инкрементного подхода к управлению облаком.*

В одном документе невозможно учесть требования всех компаний. Поэтому в этой статье описываются минимально требуемые и возможные действия для каждого этапа в процессе совершенствования системы управления. Первоначальная цель этих действий заключается в том, чтобы помочь вам создать [политику MVP](../guides/index.md#an-incremental-approach-to-cloud-governance) и создать платформу для улучшения добавочной политики. Ваша группа по управлению облаком должна принять решение о том, сколько инвестиций в эти действия для повышения специализации в плане безопасности.

> [!CAUTION]
> Ни минимальное, ни потенциальное действие, описанное в этой статье, соответствует определенным корпоративным политикам или требованиям, предъявляемым к сторонним требованиям. Это руководство призвано облегчить обсуждения по согласованию модели управления облаком с обоими требованиями.

## <a name="planning-and-readiness"></a>Планирование и готовность

На этом этапе развития системы управления ликвидируется разрыв между бизнес-показателями и стратегиями практических действий. В ходе этого процесса руководство определяет конкретные метрики, сопоставляет их с цифровыми активами и начинает планировать общий процесс миграции.

**Минимальные рекомендуемые действия.**

- Рассмотрите [цепочку инструментов для базовой системы безопасности](./toolchain.md).
- Разработка черновика с рекомендациями по архитектуре документов и их распространение среди ключевых заинтересованных лиц.
- Проведите обучение и привлеките к участию людей и команды, на работу которых повлияет создание рекомендаций по архитектуре.
- Добавьте задачи по обеспечению безопасности с указанием приоритета в список невыполненных работ по миграции.

**Возможные действия.**

- Определите схему классификации данных.
- Выполните процесс планирования цифровых активов для инвентаризации текущих ИТ-ресурсов, участвующих в бизнес-процессах и вспомогательных операциях.
- Выполните [проверку политики](../../govern/policy-compliance/cloud-policy-review.md), чтобы начать процесс модернизации существующих корпоративных политик ИТ-безопасности, и определите политики MVP для известных рисков.
- Просмотрите рекомендации по безопасности вашей облачной платформы. Для Azure эти службы можно найти на [портале доверия служб Майкрософт](https://servicetrust.microsoft.com).
- Определите, содержит ли базовая политика безопасности [жизненный цикл разработки системы](https://www.microsoft.com/sdl)безопасности.
- Оцените бизнес-риски, связанные с сетью, данными и ресурсами, на основе следующих выпусков (от одного до трех) и измерьте допустимые отклонения по отношению к этим рискам в вашей организации.
- Ознакомьтесь с обзорными [тенденциями корпорации Майкрософт в кибербезопасности](https://www.microsoft.com/security/operations/security-intelligence-report) отчете, чтобы получить общие сведения о текущей ориентации системы безопасности.
- Рассмотрите возможность разработки роли [девсекопс](https://www.microsoft.com/devsecops) в Организации.

## <a name="build-and-predeployment"></a>Сборка и предразвертывание

Для успешной миграции среды необходимы некоторые технические и нетехнические требования. Этот процесс нацелен на решения, подготовленность и базовую инфраструктуру, которые должны быть готовы до миграции.

**Минимальные рекомендуемые действия.**

- Реализуйте [базовые показатели безопасности цепочки инструментов](./toolchain.md) , выполнив развертывание на этапе предразвертывания.
- Обновление руководств по архитектуре документация и распространение среди ключевых заинтересованных лиц.
- Выполните задачи по обеспечению безопасности, включенные в приоритетный список невыполненных работ по миграции.
- Разработайте обучающие материалы и документы, информационные сообщения, поощрения и другие программы, которые помогут пользователям освоиться.

**Возможные действия.**

- Определите стратегию [шифрования](../../decision-guides/encryption/index.md) данных, размещенных в облаке, для своей организации.
- Оцените вашу стратегию [идентификации](../../decision-guides/identity/index.md) для развертывания в облаке. Определите, как ваше облачное решение идентификации будет сосуществовать или интегрироваться с локальными поставщиками удостоверений.
- Определите политики границы сети для вашего проекта [программно-конфигурируемой сети (SDN)](../../decision-guides/software-defined-network/index.md), чтобы обеспечить безопасную виртуальную сеть.
- Оцените политики доступа Организации с [минимальными правами](/azure/active-directory/roles/delegate-by-task) и используйте роли на основе задач для предоставления доступа к конкретным ресурсам.
- Примените механизмы безопасности и мониторинга ко всем облачным службам и виртуальным машинам.
- По возможности автоматизируйте [политики безопасности](../../decision-guides/policy-enforcement/index.md).
- Изучите базовую политику безопасности и определите, нужно ли изменять планы в соответствии с рекомендациями, такими как, изложенные в [жизненном цикле разработки системы безопасности](https://www.microsoft.com/sdl).

## <a name="adopt-and-migrate"></a>Внедрение и миграция

Миграция представляет собой последовательный процесс перемещения, тестирования и внедрения приложений или рабочих нагрузок в существующей цифровой инфраструктуре.

**Минимальные рекомендуемые действия.**

- Перенос [базовых показателей безопасности цепочки инструментов](./toolchain.md) из предварительного развертывания в рабочую среду.
- Обновление руководств по архитектуре документация и распространение среди ключевых заинтересованных лиц.
- Разработайте обучающие материалы и документы, информационные сообщения, поощрения и другие программы, которые помогут пользователям освоиться.

**Возможные действия.**

- Ознакомьтесь с последними базовыми показателями безопасности и сведениями об угрозах, чтобы найти новые бизнес-риски.
- Определите допустимые отклонения для устранения новых угроз безопасности, которые могут возникнуть.
- Выявите отклонения от политики и примените исправления.
- Настройте автоматизацию защиты и контроля доступа для обеспечения максимального соответствия политике.
- Убедитесь, что рекомендации, определенные на этапах сборки и предварительного развертывания, выполнены правильно.
- Проверьте политики доступа с минимальными правами и настройте элементы управления доступом, чтобы обеспечить максимальную безопасность.
- Проверьте свою цепочку инструментов базовой системы безопасности на ваших рабочих нагрузках, чтобы определить уязвимости и устранить их.

## <a name="operate-and-post-implementation"></a>Эксплуатация и действия после реализации

Когда преобразование завершится, системы управления и эксплуатации должны сохраняться для поддержки естественного жизненного цикла приложений или рабочих нагрузок. Этот этап развития системы управления посвящен действиям, которые обычно следуют за внедрением решения, когда цикл трансформации становится более стабильным.

**Минимальные рекомендуемые действия.**

- Проверьте и уточните [базовые показатели безопасности цепочки инструментов](./toolchain.md).
- Настройте уведомления и отчеты для оповещения о потенциальных проблемах безопасности.
- Уточнение рекомендаций по архитектуре для руководства по процессам внедрения в будущем.
- Периодически проводите обучение для задействованных команд, чтобы обеспечить соблюдение рекомендаций по архитектуре.

**Возможные действия.**

- Определите шаблоны и поведение для своих рабочих нагрузок и настройте свои инструменты мониторинга и создания отчетов так, чтобы выявлять любую аномальную активность, доступ или использование ресурсов и получать оповещения о них.
- Постоянно обновляйте политики мониторинга и создания отчетов для выявления новых уязвимостей, эксплойтов и атак.
- Подготовьте процедуры для быстрой остановки несанкционированного доступа и отключения ресурсов, которые мог скомпрометировать злоумышленник.
- Регулярно проверяйте новейшие рекомендации по обеспечению безопасности и по возможности применяйте их к вашей политике безопасности, возможностям автоматизации и мониторинга.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы ознакомились с концепцией управления безопасностью в облаке, ознакомьтесь с рекомендациями и методами обеспечения безопасности от корпорации Майкрософт для Azure в [этой статье](./azure-security-guidance.md).

> [!div class="nextstepaction"]
> [Сведения о руководстве по безопасности для Azure](./azure-security-guidance.md) 
>  [Введение в безопасность Azure](/azure/security/fundamentals/overview) 
>  [Сведения о ведении журналов, составлении отчетов и мониторинге](../../decision-guides/logging-and-reporting/index.md)
