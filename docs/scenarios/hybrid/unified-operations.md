---
title: Единые операции для гибридного, многооблачного и пограничной
description: Реализуйте эффективные элементы управления для согласованного управления операциями в гибридных, многооблачных и пограничных развертываниях.
author: brianblanchard
ms.author: brblanch
ms.date: 01/12/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: e2e-hybrid
ms.openlocfilehash: 1f1385095de368d52e4a4790c0267defbc96bb80
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799128"
---
# <a name="introduction-to-unified-operations"></a>Введение в единые операции

Одна облачная панель мониторинга, в гибридной, многооблачной и пограничной.

Гибридные, многооблачные и пограничные подходы могут привести к увеличению эксплуатационных расходов. Непредвиденное увеличение затрат является результатом дублирования или разнородных операций с одним набором практических рекомендаций для каждого поставщика облачных служб. **Единые операции** — это преднамеренный подход к поддержке одного набора средств и процессов для согласованного управления каждым поставщиком облачных решений с помощью общего набора рекомендаций по управлению и эксплуатации.

## <a name="understand-and-minimize-costs-through-unified-operations"></a>Понимать и сокращать затраты благодаря единым операциям

В гибридных и многооблачных стратегиях первое увеличение затрат на накладные расходы может быть дубликатом служебных программ облачной платформы: сети, удостоверений, управления, безопасности и инструментария. В долгосрочной перспективе могут возникать бизнес-задачи, такие как сотрудники основных функций или группы с навыками, необходимыми для управления различными средами.

Гибридные и многооблачные стратегии привели к неправильному завершению работы облачных решений, чем локальные технологии. Последнее Forrester консультационное исследование, проведенное корпорацией Майкрософт, показало, что Гибридная и многооблачная стратегия может обеспечить очень значительную рентабельность [инвестиций в три года, а также значительно избежать затрат на локальную инфраструктуру и персонал](https://azure.microsoft.com/resources/forrester-tei-microsoft-azure-iaas/) для организаций. Основная среда Accenture и всервице, а также исследование энергии в дальнейшем выражает, что облачные решения добавляют значительно повышенную эффективность энергопотребления для крупных развертываний, а [организации сокращают энергопотребление и выбросы на более чем 30% по сравнению с бизнес-приложениями, установленными локально](https://download.microsoft.com/download/7/3/9/739BC4AD-A855-436E-961D-9C95EB51DAF9/Microsoft_Cloud_Carbon_Study_2018.pdf), а также для небольших развертываний, что достигает 90-процентных уменьшений от общей облачной службы.

Организации могут модернизировать и оптимизировать общие операции, используя простой подход к снижению рисков, увеличению затрат или проблемам, связанным с основными функциями. "**Единые операции**" — это подход к гибридным, многооблачным и граничным облачным стратегиям, который сокращает краткосрочное дублирование и долгосрочные ограничения для ваших технологических сотрудников. В этой статье описывается нейтральный к поставщику подход к использованию Объединенных операций для расширения одной плоскости корпоративного управления в распределенных ресурсах в гибридных, многооблачных и пограничных средах.

Далее приводятся дополнительные статьи, в которых описывается подход Azure к единым операциям [: обеспечение](./govern.md) [управления и управление операциями](./manage.md) в разнородных гибридных, многооблачных и пограничных средах. Общей целью в подходе, характерном для Azure к объединенным операциям, является Инвентаризация, систематизация и управление ИТ-ресурсами в любой инфраструктуре. Эта централизованная плоскость управления предприятием обеспечивает согласованное управление облачными операциями в локальных, многооблачных и пограничных средах.

## <a name="primary-cloud-platform"></a>Основная облачная платформа

Успешные гибридные, многооблачные и граничные стратегии начинаются с основной облачной платформы.

![Основная облачная платформа с возможностями, службами и элементами управления для поддержки ваших процессов.](../../_images/hybrid/primary-cloud-provider.png)

Как в общедоступном, так и в частном облаке, основная облачная платформа предназначена для размещения рабочих процессов, а также набора определенных облачных средств. В Azure эти средства являются [регионами Azure](https://azure.microsoft.com/global-infrastructure/), а в локальной среде — центрами обработки данных. Эти средства обеспечивают облачные службы узла, необходимые для управления основными операциями, а также для поддержки других рабочих нагрузок, размещенных на платформе. Основная облачная платформа также будет включать ряд элементов управления, предназначенных для поддержки операций в этом облаке.

> [!NOTE]
> Основная облачная платформа может не размещать все или даже большинство рабочих нагрузок, но **службы и элементы управления, необходимые для выполнения основных процессов для управления операциями, обеспечения соответствия требованиям, безопасности и т. д**.
>
> [!CAUTION]
> Возможно, у вас уже есть основная облачная платформа. К сожалению, многие облачные платформы были разработаны и созданы до выполнения операций, требующих гибридные, многооблачные и пограничные варианты развертывания. Это часто порабатывает клиентов для репликации процессов, используя различные облачные элементы управления для управления облачными службами на каждой облачной платформе. Если стратегия облака вызывает гибридные, многооблачные или пограничные варианты развертывания **и** основная облачная платформа не поддерживает их, рассмотрите платформу, которая может развернуть необходимые функции для Объединенных операций.
>

## <a name="defining-unified-operations"></a>Определение Объединенных операций

Принцип работы Объединенных операций прост: реализация расширения или шлюза для применения элементов управления в основном облачном поставщике в гибридных, многооблачных и пограничных развертываниях. Управляйте своими операциями и контролируйте их согласованно в разнородных локальных, многооблачных и пограничных средах.

При реализации унифицированных операций единая плоскость управления предприятием распространяется на распределенные ресурсы Организации, обеспечивая согласованное управление, разработку приложений и облачные службы для любой инфраструктуры в любом месте. Благодаря обеспечению согласованного управления и контроля для организаций шлюз с такими облачными элементами управления расширяет согласованность служб управления операциями и данных в различных локальных, многооблачных и граничных средах.

При определении основной облачной платформы важно убедиться, что в облаке есть необходимые наборы инструментов для управления всеми облаками в портфеле. Многие облачные платформы были разработаны и созданы до операций, требующих гибридных, многооблачных или пограничных вариантов развертывания. Недостаточные возможности в текущих средствах работы могут потребовать от рабочих групп реплицировать процессы. Использование различных облачных элементов управления для управления облачными службами на каждой облачной платформе. Если стратегия облака вызывает гибридные, многооблачные или пограничные варианты развертывания **и** основная облачная платформа не поддерживает их, следует рассмотреть платформу, которая может развернуть необходимые функции для Объединенных операций.

## <a name="unified-operations"></a>Единые операции

Единое управление облаком и эксплуатация в портфеле распределенных ресурсов (в любом месте) обеспечивает интегрированную гибридную и облачную стратегию, которая может повысить будущие инновации, гибкость и рост бизнеса в вашей организации. Добавление шлюза для облачных элементов управления, расширяющих возможности управления и данных в локальные, многооблачные и пограничные, обеспечивает единообразное управление и управляемость для организаций. неотъемлемая Гибридная и многооблачная стратегия, которая может увеличить будущие инновации, гибкость и рост бизнеса в Организации. Реализуйте расширение (или шлюз), чтобы применить элементы управления в вашем основном облачном поставщике в гибридных, многооблачных и пограничных развертываниях.

![Единые операции расширяют облачные элементы управления в гибридные, многооблачные и пограничные развертывания](../../_images/hybrid/primary-cloud-provider-extended.png)

> [!WARNING]
> Реализация Объединенных операций может быть относительно простой. Но если облачная платформа не может управлять необходимыми основными процессами обработки, она потребует дополнительных капитальных затрат, с дорогостоящими разработками для создания расширений или шлюзов к другим облакам. Основной фактор ограничения, по которому клиенты создают дублирующие или фрактуред операции и процессы, обусловлено существующими основными облачными платформами с такими ограничениями.
>
> Несогласованный подход к реализации унифицированных операций может привести к неэффективному увеличению затрат на организацию с повышенными эксплуатационными затратами (от повторяющихся служебных программ облачной платформы или с помощью средств управления) и отрицательным влиянием на бизнес (группы персонала без необходимых навыков облака).
>

Если текущий поставщик основных облачных служб не предоставляет необходимые возможности для Объединенных операций, рассмотрите возможность оптимизации операций и процессов с помощью современного поставщика облачных служб.

## <a name="unified-operations-decomposed"></a>Унифицированные операции разлагаются

На этом рисунке показаны отдельные компоненты, необходимые для Объединенных операций, и показано, как они взаимодействуют друг с другом. В следующих разделах представлены подробные сведения о каждом отдельном компоненте Operations.

![Инфографика, показывающие компоненты, необходимые для доставки Объединенных операций (см. оставшуюся часть этой статьи).](../../_images/hybrid/unified-operations.png)

## <a name="customer-processes"></a>Клиентские процессы

Основная цель Объединенных операций — создание во всех развертываниях как можно более согласованных процессов. Ни один поставщик облачных служб не сможет достичь соответствия характеристик 100% для всех гибридных, многооблачных и пограничных развертываний. Однако поставщик должен иметь возможность предоставлять базовые наборы функций, общие для всех развертываний, чтобы обеспечить согласованность [](./govern.md) процессов [контроля и управления операциями](./manage.md) .

![Клиентские процессы, которые могут поддерживаться едиными операциями](../../_images/hybrid/unified-operations-customer-processes.png)

Чаще всего клиенты нуждаются в возможности обеспечить согласованность в определенных процессах управления и контроля операций. Чтобы удовлетворить долгосрочные требования, решение единой операции должно иметь возможность масштабироваться в соответствии с этими общими процессами, указанными ниже.

### <a name="common-governance-processes-tasks"></a>Общие процессы управления (задачи)

- **Управление затратами:** Просмотр, управление и оптимизация затрат, а также поиск **и предоставление рекомендаций по устранению рисков для ИТ-рисков, связанных с облаком**.
- Базовый план безопасности — аудит, применение или автоматизация требований из рекомендованных средств управления безопасностью, а также **Поиск и предоставление рекомендаций по устранению** рисков, связанных с безопасностью.
- **Согласованность ресурсов:** Подключение, упорядочение и Настройка ресурсов и служб, а затем **выявление и предоставление рекомендаций по предотвращению рисков для потенциальных бизнес-рисков**.
- **Базовый уровень удостоверений:** Применяйте проверку подлинности и авторизацию для идентификации пользователя и доступа, а затем **выявление и предоставление рекомендаций по устранению рисков для потенциальных бизнес-рисков, связанных с идентификацией**.
- **Ускорение развертывания:** Согласованность дисков с помощью шаблонов, автоматизации и конвейеров (для развертываний, выравнивания конфигурации и многократно используемых ресурсов), **Установка политик для обеспечения соответствия, согласованности и повторяемости развертывания и настройки ресурсов**.

### <a name="common-operations-management-processes-tasks"></a>Общие процессы управления операциями (задачи)

- **Инвентаризация и видимость:** Учетная запись для и обеспечение отчетов для всех активов, а затем **сбора и мониторинга состояния выполнения инвентаризации в средах корпоративного уровня**.
- **Оптимизированные операции:** Мониторинг, исправление и оптимизация поддерживаемых ресурсов, а **также снижение рисков в сфере бизнеса от снижения конфигурации или уязвимостей от несовместимости управления исправлениями**.
- **Защита и восстановление:** Рекомендации по резервному копированию, непрерывности бизнес-процессов и аварийному восстановлению, а **также снижение длительности и влияния непредотвращенных простоев**.
- [Операции с платформой](../../manage/azure-management-guide/platform-specialization.md): специализированные операции для распространенных технологических платформ, таких как SQL, ВВД и SAP (для рабочих нагрузок со средним и высоким уровнем серьезности).
- [Операции рабочей нагрузки](../../manage/azure-management-guide/workload-specialization.md): специализированные операции (для высокоприоритетных и критически важных рабочих нагрузок) с более высокими требованиями к операциям.

Операции с платформой и рабочей нагрузкой выполняют эквивалентный *итеративный процесс* для **улучшения проектирования системы, автоматизируют исправление, масштабирование изменений с помощью каталога услуг и постоянно улучшают проектирование, автоматизацию и масштабирование системы**.

Основная облачная платформа должна иметь возможность предоставлять необходимые технические возможности и инструменты для автоматизации процессов, а также выполнять поставленные выше задачи по управлению и эксплуатации. Решение для унифицированных операций должно обеспечить возможность расширения этих процессов во всех гибридных, многооблачных и пограничных развертываниях.

## <a name="primary-cloud-controls"></a>Основные элементы управления облаком

Основная облачная платформа должна включать ряд важных функций для упрощения или автоматизации пользовательских процессов, которые обычно требуются в облаке:

![Стандартные облачные элементы управления, указанные в следующих маркерах](../../_images/hybrid/unified-operations-cloud-controls.png)

### <a name="basic-features"></a>Основные возможности

Все эти основные функции необходимы для предоставления плана внедрения в облако, в масштабе:

- **Поиск, индексирование, группирование и маркировка** всех развернутых ресурсов, расширенная видимость и управление.
- **Темплатизе, автоматизируйте и расширяйте Инструментарий** для единообразных развертываний.
- **Создайте границы доступа и безопасности** для защиты развернутых ресурсов.

### <a name="enhanced-features"></a>Улучшенные функции

Вам, скорее всего, потребуется большинство улучшенных функций для работы в гибридной и многооблачной среде.

- **Отчеты о производительности и инвентаризации**
- **Аудит и Автоматизация безопасности и соответствия требованиям**
- **Отслеживание и отчеты о приложениях и зависимостях**

### <a name="automated-controls"></a>Автоматизированные элементы управления

Автоматизируйте среду с помощью средств, модернизировать свои операции и оптимизируя эксплуатационные расходы:

- **Политика среды и в гостевой системе**
- **Конфигурация и обновления**
- **Защита и восстановление**

Скорее всего, эти функции уже включены в наборы элементов управления, используемые в настоящее время для работы с основным поставщиком облачных служб. В этом наборе элементов управления может быть доступно множество дополнительных функций и автоматизированных процессов. Это основные функциональные возможности управления, которые должны быть доступны в гибридном, многооблачном и пограничном решении в рамках решения единой системы.

Это обусловлено тем, что они реализованы как основные элементы управления, которые описаны выше, так как мы обычно видим фрактуред или дублирующиеся операции. Как упоминалось ранее, несогласованный подход к реализации унифицированных операций влияет на повышение эксплуатационных расходов (например, на дубликаты служебных программ облачной платформы, средства операций), а также на ранних этапах поездки на внедрение облака.

### <a name="hybrid-multicloud-gateway-and-enterprise-control-plane"></a>Гибридный, многооблачный шлюз и плоскость управления предприятием

Чтобы расширить свои основные облачные элементы управления, необходимо настроить расширение или шлюз. Этот тип расширения позволяет элементам управления видеть ресурсы, развернутые за пределами облачной платформы, и взаимодействовать с ними (**на самом деле, создавая одну плоскость управления и обеспечивая более заметную видимость для разнородных разнородных сред**).

В облачных платформах Майкрософт это расширение [**Azure Arc**](/azure/azure-arc/overview) . Служба "Дуга Azure" расширяет те же элементы управления и процессы, которые используются, чтобы управлять облаком Azure для других общедоступных и частных облаков, а также пограничных. Это облачные элементы управления, которые позволяют единым операциям подходить к согласованным процессам управления и эксплуатации в разнородных локальных, многооблачных и пограничных средах.

Единые операции расширяют возможности [**ARM**](/azure/azure-resource-manager/management/overview) (Azure Resource Manager), операционной системы Azure. ARM выходит за пределы Azure, чтобы проецировать эти разбросанные ресурсы в Azure и представлять их в качестве привилегированных. Применяя службы Azure и управление к любой инфраструктуре, единый подход расширяет возможности Azure и обеспечивает новые гибридные и многооблачные решения.

Использование унифицированных операций позволяет организовывать, управлять и защищать любую среду в любом месте, обеспечивая централизованную видимость, эксплуатацию и соответствие требованиям. Создавайте облачные приложения в любом месте и в масштабе с помощью стандартизированных служб приложений, от развертывания до мониторинга. Развертывайте службы Azure в любом месте, быстрее, согласованно и в масштабе, используя постоянно обновленные службы с поддержкой дуги Azure.

Создание, эксплуатация и управление в традиционных, облачных и распределенных приложениях с согласованными элементами управления и процессами, обеспечивающими управление и эксплуатацию, расширяет возможности облачных вычислений для дискретных ресурсов. Новые гибридные и многооблачные сценарии могут быть разблокированы от упрощенного управления, более быстрой разработки приложений и согласованных служб Azure, которые расширены для всех сред ресурсов, в любой инфраструктуре во всей ИТ.

Центральная плоскость управления Azure, в которой основное внимание уделяется стандартизации, взаимодействию и соответствию, обеспечивает согласованность и единообразное управление и эксплуатацию в гибридных и многооблачных инфраструктурах, что может повысить производительность, снизить риски и ускорить внедрение и применение технологий в облаке для организаций.

## <a name="next-steps"></a>Дальнейшие действия

Чтобы приступить к работе в гибридном и многооблачном стратегиях, начните с краткого рассмотрения [стратегии гибридной и многооблачной](./strategy.md)работы.
