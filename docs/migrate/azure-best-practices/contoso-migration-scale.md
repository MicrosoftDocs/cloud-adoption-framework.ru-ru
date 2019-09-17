---
title: Масштабирование миграции в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как Contoso справляется с масштабной миграцией в Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 30a510d5acd5773253524200ea65e52a3325e10d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829622"
---
# <a name="scale-a-migration-to-azure"></a>Масштабирование миграции в Azure

В этой статье показано, как вымышленная компания Contoso выполняет масштабную миграцию в Azure. Компания планирует и выполняет миграцию более 3000 рабочих нагрузок, 8000 баз данных и более 10 000 виртуальных машин.

## <a name="business-drivers"></a>Бизнес-факторы

Совместными усилиями ИТ-руководство и деловые партнеры определили указанные ниже цели этой миграции.

- **Адаптация к расширению бизнеса.** По мере развития компании Contoso растет нагрузка на локальные системы и инфраструктуру.
- **Повышение эффективности.** Contoso необходимо удалить ненужные процедуры и оптимизировать процессы для разработчиков и пользователей. Бизнес нуждается в том, чтобы ИТ были быстрыми и чтобы не тратить время или деньги, обеспечивая более высокие требования клиентов.
- **Повышение гибкости.** ИТ-отдел компании Contoso должен проявлять большую гибкость в отношении потребностей бизнеса. Должна реагировать быстрее, чем изменения на рынке, чтобы включить успех в глобальную экономику реагирования. Он не должен мешать или становиться помехой для бизнеса.
- **Масштабирование.** По мере того как бизнес успешно растет, ИТ-отдел компании Contoso должен предоставлять системы, способные расти в том же темпе.
- **Улучшение моделей затрат.** Компании Contoso требуется снизить потребности в капитале, указанные в бюджете ИТ-отдела. Компания Contoso хочет использовать возможности облака для масштабирования ресурсов и снижения потребности в дорогостоящем оборудовании.
- **Снижение затрат на лицензии.** Компании Contoso требуется минимизировать затраты на облако.

## <a name="migration-goals"></a>Цели миграции

Группа, работающая над облачной инфраструктурой компании Contoso, определила цели этой миграции. Эти цели использовались для определения оптимального метода миграции.

**Требования** | **Сведения**
--- | ---
**Быстрый переход на Azure** | Компания Contoso хочет как можно быстрее начать перенос приложений и виртуальных машин в Azure.
**Составление полного списка ресурсов** | Компании Contoso требуется полный список используемых ею приложений, баз данных и виртуальных машин.
**Оценка и классификация приложений** | Компания Contoso хочет воспользоваться всеми преимуществами облака. По умолчанию предполагается, что все службы будут выполняться как PaaS. Модель IaaS будет использоваться в случаях, где PaaS не подходит.
**Обучение и переход на модель DevOps** | Компания Contoso намеревается перейти на модель DevOps. Будет проведено обучение по Azure и DevOps, после чего группы будут реорганизованы (при необходимости).

После уточнения целей и требований компания Contoso проверяет инфраструктуру ИТ и определяет процесс миграции.

## <a name="current-deployment"></a>Текущее развертывание

После планирования и настройки [инфраструктуры Azure](contoso-migration-infrastructure.md) и испытания различных сочетаний подтверждений концепции миграции, перечисленных в таблице выше, компания Contoso готова приступить к полной миграции в Azure в нужном масштабе. Вот что компании Contoso необходимо перенести.

<!--markdownlint-disable MD033 -->

**Элемент** | **Объем** | **Сведения**
--- | --- | ---
**Рабочие нагрузки** | Более 3000 приложений | Приложения, которые выполняются на виртуальных машинах.<br/><br/>  Это приложения для Windows, SQL и OSS LAMP.
**Базы данных** | Около 8500. | Базы данных SQL Server, MySQL и PostgreSQL.
**Виртуальные машины** | Более 35 000 | Виртуальные машины, которые выполняются на узлах VMware под управлением серверов vCenter Server.

<!--markdownlint-enable MD033 -->

## <a name="migration-process"></a>Процесс миграции

Теперь, когда компания Contoso уточнила бизнес-факторы и цели миграции, она определяет четырехэтапный подход к процессу миграции.

- **Этап 1. Оценка.** Обнаружение имеющихся ресурсов и выяснение их пригодности для переноса в Azure.
- **Этап 2. Миграция.** Перемещение ресурсов в Azure. Способ перемещения приложений и объектов в Azure будет зависеть от имеющихся приложений и требуемого результата.
- **Этап 3. Оптимизация.** После перемещения ресурсов в Azure компании Contoso необходимо улучшить и оптимизировать их, чтобы достичь максимальной производительности и эффективности.
- **Этап 4. Защита и управление.** Выполнив все предыдущие этапы, компания Contoso использует соответствующие ресурсы и службы Azure для обеспечения безопасности своих облачных приложений в Azure, а также для управления ими и их отслеживания.

Эти этапы не выполняются последовательно во всей организации. Каждая часть проекта миграции Contoso будет находиться на определенном этапе процесса оценки и переноса. Оптимизация, обеспечение безопасности и управление будут выполняться в течение длительного времени.

## <a name="phase-1-assess"></a>Этап 1. Оценить

Компания Contoso начинает процесс с изучения и оценки локальных приложений, данных и инфраструктуры. Ниже приведены действия специалистов Contoso:

- Компании Contoso необходимо обнаружить приложения, сопоставить зависимости между приложениями и определить порядок миграции и приоритеты.
- При проведении оценки компания составит полный список приложений и ресурсов. Наряду с новым списком компания Contoso использует и обновит существующую базу данных управления конфигурацией (CMDB) и каталог служб.
  - CMDB содержит технические конфигурации для приложений Contoso.
  - Каталог служб содержит операционные данные приложений, включая связанных с ними деловых партнеров и Соглашения об уровне обслуживания (SLA).

### <a name="discover-apps"></a>Обнаружение приложений

Компания Contoso использует тысячи приложений на целом ряде серверов. Помимо CMDB и каталога служб компании Contoso необходимы инструменты обнаружения и оценки.

- Эти инструменты должны обеспечить механизм, позволяющий передавать данные оценки в процесс миграции.
- Инструменты оценки должны предоставлять данные, которые помогут создать интеллектуальный список физических и виртуальных ресурсов компании Contoso. Эти данные должны включать в себя сведения о профилях и метрики производительности.
- По завершении обнаружения у компании Contoso должен быть полный список ресурсов, а также метаданные, связанные с ними. Этот список будет использоваться для определения плана миграции.

### <a name="identify-classifications"></a>Определение классификаций

Компания Contoso определяет несколько общих категорий для классификации ресурсов в списке. Эти классификации крайне важны для принятия решений о миграции компанией. Список классификаций помогает установить приоритеты для миграции и выявить сложные проблемы.

**Категория** | **Назначенное значение** | **Сведения**
--- | --- | ---
Бизнес-группа | Список имен бизнес-групп. | Какая группа ответственна за элемент списка?
Кандидат для подтверждения концепции | Да/нет | Можно ли использовать приложение для подтверждения концепции или в качестве раннего последователя для миграции в облако?
Технический долг | Отсутствует; имеется некоторый или серьезный | Использует ли элемент списка неподдерживаемый продукт, платформу или операционную систему?
Влияние брандмауэра | Да/нет | Взаимодействует ли приложение с Интернетом или сетью за пределами трафика?  Интегрируется ли оно с брандмауэром?
Проблемы с безопасностью | Да/нет | Известны какие-либо проблемы безопасности, связанные с приложением?  Использует ли приложение незашифрованные данные или устаревшие платформы?

### <a name="discover-app-dependencies"></a>Обнаружение зависимостей приложений

В процессе оценки компании Contoso необходимо определить, где выполняются приложения, и выявить зависимости и связи между серверами приложений. Компания сопоставляет среду поэтапно.

1. На первом шаге она определяет, как серверы и компьютеры связаны с отдельными приложениями, расположениями в сети и группами.
2. Имея эту информацию, компания Contoso может четко определить приложения, которые имеют несколько зависимостей и поэтому подходят для быстрого переноса.
3. Компания может использовать сопоставление, чтобы выявить более сложные зависимости и взаимодействие между серверами приложений. Затем компания Contoso может сгруппировать эти серверы логически, в соответствии с приложениями, и спланировать стратегию миграции на основе этих групп.

Выполнение сопоставления гарантирует, что все компоненты приложений будут идентифицированы и учтены при создании плана миграции.

![Сопоставление зависимостей](./media/contoso-migration-scale/dependency-map.png)

### <a name="evaluate-apps"></a>Оценка приложений

В качестве последнего этапа в процессе обнаружения и оценки компания Contoso может оценить результаты оценки и сопоставления, чтобы выяснить, как перенести каждое приложение в каталоге служб.

Чтобы описать этот процесс оценки, в список добавляется ряд дополнительных классификаций.

**Категория** | **Назначенное значение** | **Сведения**
--- | --- | ---
Бизнес-группа | Список имен бизнес-групп. | Какая группа ответственна за элемент списка?
Кандидат для подтверждения концепции | Да/нет | Можно ли использовать приложение для подтверждения концепции или в качестве раннего последователя для миграции в облако?
Технический долг | Отсутствует; имеется некоторый или серьезный | Использует ли элемент списка неподдерживаемый продукт, платформу или операционную систему?
Влияние брандмауэра | Да/нет | Взаимодействует ли приложение с Интернетом или сетью за пределами трафика?  Интегрируется ли оно с брандмауэром?
Проблемы с безопасностью | Да/нет | Известны какие-либо проблемы безопасности, связанные с приложением?  Использует ли приложение незашифрованные данные или устаревшие платформы?
Стратегия миграции | Повторное размещение, рефакторинг, перепроектирование или перестроение | Какого типа миграция необходима для приложения? Как приложение будет развернуто в Azure? [Узнайте больше](contoso-migration-overview.md#migration-patterns).
Техническая сложность | 1–5 | Насколько сложной является миграция? Это значение должно определяться отделом DevOps компании Contoso и соответствующими партнерами.
Важность для бизнеса | 1–5 | Насколько важно приложение для бизнеса? Например, приложению небольшой рабочей группы может быть назначена оценка "1", а критически важному приложению, используемому по всей организацией, может быть назначена оценка "5". Эта оценка повлияет на уровень приоритета миграции.
Приоритет миграции | 1, 2, 3 | Какой приоритет миграции у приложения?
Риск при миграции | 1–5 | Какой уровень риска для переноса приложения? Это значение должно быть согласовано с отделом DevOps компании Contoso и соответствующими партнерами.

### <a name="figure-out-costs"></a>Определение затрат

Чтобы определить затраты и потенциальную экономию для миграции в Azure, компания Contoso может использовать [калькулятор совокупной стоимости владения](https://azure.microsoft.com/pricing/tco/calculator), чтобы вычислить и сравнить совокупную стоимость владения Azure с локальным развертыванием.

### <a name="identify-assessment-tools"></a>Определение инструментов оценки

Компания Contoso выбирает инструменты для обнаружения, оценки и создания списка ресурсов. Она определяет набор инструментов и служб Azure, инструментов и сценариев для собственных приложений, а также инструментов партнеров. В частности, компании Contoso необходимо узнать, как можно использовать службу "Миграция Azure" для выполнения оценки в нужном масштабе.

#### <a name="azure-migrate"></a>Миграция Azure

С помощью службы "Миграция Azure" можно обнаруживать и оценивать локальные виртуальные машины VMware для подготовки к миграции в Azure. Ниже приведены функции Миграции Azure.

1. Обнаружение. Позволяет обнаружить локальные виртуальные машины VMware.
    - Миграция Azure поддерживает обнаружение на нескольких серверах vCenter Server (последовательное) и может выполнять обнаружение в отдельных проектах Миграции Azure.
    - Миграция Azure выполняет обнаружение с помощью Сборщика миграции, выполняемого на виртуальной машине VMware. Один и тот же сборщик может обнаруживать виртуальные машины на разных серверах vCenter Server и отправлять данные в разные проекты.
2. Оценка готовности. Позволяет определить, подходят ли ваши локальные компьютеры для работы в Azure. Оценка включает в себя следующее.
    - Рекомендации по размеру. Рекомендации по размеру виртуальных машин Azure на основе журнала производительности локальных виртуальных машин.
    - Расчетная месячная стоимость. Расчет затрат на работу локальных виртуальных машин в Azure.
3. Определение зависимостей. Визуализация зависимостей локальных компьютеров для создания оптимальных групп компьютеров для оценки и миграции.

![Миграция Azure](./media/contoso-migration-scale/azure-migrate.png)

##### <a name="migrate-at-scale"></a>Миграция в соответствующем масштабе

Компании Contoso необходимо использовать Миграцию Azure в соответствии с масштабом миграции.

- Компания будет выполнять последовательную оценку приложений с помощью Миграции Azure. Это гарантирует, что Миграция Azure будет возвращать актуальные данные на портал Azure.
- Администраторы Contoso изучают [развертывание Миграции Azure в нужном масштабе](/azure/migrate/how-to-scale-assessment).
- Компания Contoso отмечает ограничения Миграции Azure, кратко изложенные в следующей таблице.

**Действие** | **Ограничение**
--- | ---
Создание проекта Миграции Azure | 10 000 виртуальных машин
Обнаружение | 10 000 виртуальных машин
Оценка | 10 000 виртуальных машин

Компания Contoso будет использовать Миграцию Azure следующим образом.

- В среде vCenter компания упорядочит виртуальные машины по папкам. Это упростит акцентирование внимания, так как будут оцениваться виртуальные машины в определенной папке.
- Миграция Azure использует Сопоставление служб Azure для оценки зависимостей между компьютерами. Для этого требуется установить агенты на оцениваемые виртуальные машины.
  - Компания Contoso использует автоматизированные сценарии для установки необходимых агентов Windows или Linux.
  - С помощью сценариев можно выполнить установку на виртуальные машины в папке vCenter.

#### <a name="database-tools"></a>Инструменты базы данных

Помимо Миграции Azure компания Contoso уделит внимание инструментам оценки баз данных. Такие инструменты, как [Помощник по миграции данных](/sql/dma/dma-overview?view=sql-server-2017), помогут оценить базы данных SQL Server для миграции.

Помощник по миграции данных (DMA) поможет компании Contoso выяснить, совместимы ли локальные базы данных с доступными решениями баз данных Azure, такими как База данных SQL Azure, SQL Server на виртуальной машине IaaS в Azure, и Управляемый экземпляр SQL Azure.

Помимо DMS у компании имеются другие сценарии, которые она использует для обнаружения и описания баз данных SQL Server. Они находятся в репозитории GitHub.

#### <a name="partner-assessment-tools"></a>Инструменты оценки от партнеров

Существует несколько других инструментов партнеров, которые могут помочь компании Contoso оценить локальную среду для миграции в Azure. [Узнайте больше](https://azure.microsoft.com/migration/partners) о партнерских решениях для Миграции Azure.

## <a name="phase-2-migrate"></a>Этап 2. Перенос

По завершении оценки компании Contoso необходимо определить инструменты для перемещения приложений, данных и инфраструктуры в Azure.

### <a name="migration-strategies"></a>Стратегии миграции

Существуют четыре общие стратегии миграции, которые может рассмотреть компания Contoso.

<!--markdownlint-disable MD033 -->

**Стратегия** | **Сведения** | **Использование**
--- | --- | ---
**Повторное размещение** | Этот подход, который часто называют миграцией по методу lift-and-shift, позволяет быстро перенести имеющиеся приложения в Azure без написания специального кода.<br/><br/> Приложение переносится в облачную среду "как есть", без рисков и затрат, связанных с изменениями кода. | Компания Contoso может повторно разместить менее стратегически важные приложения, не изменяя код.
**Рефакторинг** | Также называемая "переупаковкой", эта стратегия требует минимального изменения кода приложений или конфигураций для подключения приложения к PaaS Azure и позволяет эффективнее использовать возможности облака. | Компания Contoso может выполнить рефакторинг стратегических приложений, чтобы сохранить базовые функции, но переместить их на платформу Azure, например в Службу приложений Azure.<br/><br/> Для этого потребуется внести в код минимальные изменения.<br/><br/> С другой стороны, компании Contoso необходимо будет обслуживать платформу виртуальных машин, так как корпорация Майкрософт не будет ею управлять.
**Перепроектирование** | Эта стратегия предполагает изменение или расширение базы кода приложений для оптимизации архитектуры приложений в соответствии с возможностями облака и масштабом.<br/><br/> Приложение модернизируется для использования устойчивой, высокомасштабируемой, независимо развертываемой архитектуры.<br/><br/> Службы Azure могут ускорить процесс, обеспечив уверенное масштабирование приложений и удобное управления ими.
**Перестроение** | Эта стратегия предполагает перестройку приложения "с нуля" с помощью собственных облачных технологий.<br/><br/> Платформа как услуга (PaaS) Azure обеспечивает полноценную среду разработки и развертывания в облаке. Она позволяет избежать некоторых затрат и сложности лицензий на программное обеспечение и устраняет потребность в базовой инфраструктуре приложений, ПО промежуточного слоя и других ресурсах. | Компания Contoso может переписать важные приложения "с нуля", чтобы воспользоваться преимуществами облачных технологий, таких как бессерверные компьютеры или микрослужбы.<br/><br/> Компания будет управлять разрабатываемыми приложениями и службами, а Azure будет управлять всем остальным.

<!--markdownlint-enable MD033 -->

Данные также необходимо учитывать, в особенности объем баз данных компании Contoso. Стандартным подходом компании Contoso является использование служб PaaS, таких как База данных SQL Azure, позволяющих воспользоваться всеми преимуществами облачных функций. Перейдя на службы PaaS для баз данных, компании будет достаточно только обслуживать данные, предоставив заботу о базовой платформе корпорации Майкрософт.

### <a name="evaluate-migration-tools"></a>Оценка инструментов миграции

Компания Contoso в основном использует несколько служб и инструментов Azure для миграции.

- [Azure Site Recovery.](/azure/site-recovery/site-recovery-overview) Управляет аварийным восстановлением и переносит локальные виртуальные машины в Azure.
- [Azure Database Migration Service](/azure/dms/dms-overview). Переносит в Azure локальные базы данных, например SQL Server, MySQL и Oracle.

#### <a name="azure-site-recovery"></a>Служба Azure Site Recovery

Azure Site Recovery — это основная служба Azure для управления аварийным восстановлением и миграцией как в самой среде Azure, так и из локальных сайтов в Azure.

1. Site Recovery обеспечивает репликацию данных с локальных сайтов в Azure и управляет ею.
2. Если настроена и запущена репликация, можно выполнить отработку отказа локальных компьютеров в Azure, завершив миграцию.

Компания Contoso уже [выполнила подтверждение концепции](contoso-migration-rehost-vm.md), чтобы узнать, как Site Recovery может помочь при миграции в облако.

##### <a name="using-site-recovery-at-scale"></a>Использование Site Recovery в нужном масштабе

Компания Contoso намеревается выполнить несколько миграций по методу lift-and-shift. Чтобы обеспечить успешную миграцию, Site Recovery будет реплицировать пакеты по 100 виртуальных машин за раз. Чтобы выяснить, как это будет происходить, компании Contoso необходимо запланировать емкость для предложенной миграции Site Recovery.

- Необходимо собрать сведения об объемах трафика компании. например:
  - Компании Contoso необходимо определить скорость изменения для виртуальных машин, которые нужно реплицировать.
  - Кроме того, необходимо учесть возможности сетевого подключения локального сайта к Azure.
- Учитывая требования к емкости и объему, компании Contoso необходимо выделить достаточную пропускную способность, соответствующую скорости ежедневного изменения данных для необходимых виртуальных машин, чтобы обеспечить соответствие целевой точке восстановления (RPO).
- Наконец, необходимо выяснить, сколько серверов необходимо для выполнения компонентов Site Recovery, которые необходимы для развертывания.

###### <a name="gather-on-premises-information"></a>Сбор сведений о локальной инфраструктуре

Компания Contoso может использовать [Планировщик развертывания Site Recovery](/azure/site-recovery/site-recovery-deployment-planner) для выполнения следующих действий.

- С его помощью компания может удаленно профилировать виртуальные машины без влияния на рабочую среду. Это помогает уточнить требования к пропускной способности и хранилищу для репликации и отработки отказа.
- Компания может запустить этот инструмент, не устанавливая в локальной среде какие-либо компоненты Site Recovery.
- Инструмент собирает данные о виртуальных машинах (совместимых и несовместимых), дисках на каждой виртуальной машине и обновлениях данных на каждом диске. Он также проверяет соответствие требованиям к пропускной способности сети и инфраструктуре Azure для успешной репликации и отработки отказа.
- Компании Contoso необходимо обеспечить выполнение этих условий, а затем запустить планировщик на компьютерах Windows Server, которые соответствуют минимальным требованиям к серверу конфигурации Site Recovery. Сервер конфигурации — это компьютер Site Recovery, требуемый для репликации локальных виртуальных машин VMware.

###### <a name="identify-site-recovery-requirements"></a>Определение требований Site Recovery

В дополнение к реплицируемым виртуальным машинам службе Site Recovery требуется несколько компонентов для миграции VMware.

<!--markdownlint-disable MD033 -->

**Компонент** | **Сведения**
--- | ---
**Сервер конфигурации** | Обычно виртуальная машина VMware настраиваются с помощью шаблона OVF.<br/><br/> Компонент сервера конфигурации используется для координации обмена данными между локальным источником и Azure, а также для управления репликацией данных.
**Сервер обработки** | По умолчанию устанавливается на сервере конфигурации.<br/><br/> Компонент сервера обработки получает данные репликации, оптимизирует их путем кэширования, сжатия и шифрования и отправляет эти данные в службу хранилища Azure.<br/><br/> Сервер обработки также устанавливает службу Mobility Service Azure Site Recovery на виртуальные машины, которые требуется реплицировать, и выполняет автоматическое обнаружение локальных компьютеров.<br/><br/> Для масштабируемых развертываний требуются дополнительные, изолированные серверы, обрабатывающие большие объемы трафика репликации.
**Mobility Service** | Агент Mobility Service устанавливается на каждой виртуальной машине, которая будет перенесена с помощью Site Recovery.

<!--markdownlint-enable MD033 -->

Компании Contoso необходимо выяснить, как развернуть эти компоненты с учетом емкости.

<!--markdownlint-disable MD033 -->

**Компонент** | **Требования к емкости**
--- | ---
**Максимальная скорость ежедневного изменения** | Один сервер обработки может поддерживать скорость ежедневного изменения до 2 ТБ. Так как виртуальная машина может использовать только один сервер обработки, максимальная скорость ежедневного изменения данных, поддерживаемая для реплицированной виртуальной машины, составляет 2 ТБ.
**Максимальная пропускная способность** | Учетная запись хранения Azure ценовой категории "Стандартный" может обрабатывать не более 20 000 запросов в секунду, и число операций ввода-вывода в секунду на реплицируемой виртуальной машине не должно превышать это ограничение. Например, если виртуальная машина содержит 5 дисков, с каждым из которых может выполняться 120 операций ввода-вывода в секунду (размером в 8 КБ), то этот показатель не будет превышать ограничение в 500 операций ввода-вывода в секунду на диск в Azure.<br/><br/> Обратите внимание на то, что число необходимых учетных записей хранения определяется путем деления общего числа операций ввода-вывода в секунду для исходного компьютера на 20 000. Реплицированный компьютер может принадлежать только одной учетной записи хранения в Azure.
**Сервер конфигурации** | Исходя из оценки репликации 100–200 виртуальных машин и [требований к размеру сервера конфигурации](/azure/site-recovery/site-recovery-plan-capacity-vmware#size-recommendations-for-the-configuration-server-and-inbuilt-process-server), компания Contoso оценивает требования к компьютеру сервера конфигурации следующим образом.<br/><br/> ЦП: 16 виртуальных ЦП (2 сокета * 8 ядер с частотой 2,5 ГГц)<br/><br/> Память: 32 ГБ<br/><br/> Диск кэша: 1 TБ<br/><br/> Частота изменения данных: от 1 ТБ до 2 ТБ.<br/><br/> В дополнение к требованиям к размеру компании Contoso будет необходимо обеспечить оптимальное расположение сервера конфигурации. Он должен находиться в той же сети и сегменте локальной сети, что и переносимые виртуальные машины.
**Сервер обработки** | Компания Contoso развернет выделенный изолированный сервер обработки, способный реплицировать 100–200 виртуальных машин.<br/><br/> ЦП: 16 виртуальных ЦП (2 сокета * 8 ядер с частотой 2,5 ГГц)<br/><br/> Память: 32 ГБ<br/><br/> Диск кэша: 1 TБ<br/><br/> Частота изменения данных: от 1 ТБ до 2 ТБ.<br/><br/> Сервер обработки будет сильно нагружен, поэтому он должен быть расположен на узле ESXi, соответствующем требованиям к дисковым операциям ввода-вывода, трафику и ЦП для репликации. Компания Contoso рассмотрит выделенный узел для этой цели.
**Сеть** | Компания Contoso изучила текущую инфраструктуру VPN-подключений типа "сеть — сеть" и решила реализовать Azure ExpressRoute. Эта реализация важна, так как она уменьшит задержку и повысит пропускную способность для основного региона Azure "Восточная часть США 2", используемого компанией.<br/><br/> **Мониторинг** Компании Contoso необходимо будет внимательно отслеживать данные, поступающие с сервера обработки. Если объем данных превысит возможности пропускной способности сети, компания рассмотрит [регулирование пропускной способности сервера обработки](/azure/site-recovery/site-recovery-plan-capacity-vmware#control-network-bandwidth).
**Служба хранилища Azure** | Для миграции компания Contoso должна определить требуемое количество целевых учетных записей хранения Azure соответствующего типа. Служба Site Recovery реплицирует данные виртуальной машины в службу хранилища Azure.<br/><br/> Site Recovery может реплицировать данные в учетные записи хранения ценовой категории "Стандартный" или "Премиум" (диски SSD).<br/><br/> Для принятия решения о хранилище компании Contoso нужно проверить [ограничения хранилища](/azure/virtual-machines/windows/disks-types) и учесть ожидаемый рост и увеличение использования со временем. Учтя скорость и приоритет миграций, компания Contoso решила использовать диски SSD ценовой категории "Премиум".<br/><br/>
Компания Contoso приняла решение использовать управляемые диски для всех виртуальных машин, развертываемых в Azure. Требуемое число операций ввода-вывода в секунду определит тип используемых дисков: HDD (цен. категория "Стандартный"), SSD (цен. категория "Стандартный") или SSD (цен. категория "Премиум").<br/><br/>

<!--markdownlint-enable MD033 -->

#### <a name="azure-database-migration-service"></a>Служба миграции баз данных Azure

Azure Database Migration Service — это полностью управляемая служба, которая обеспечивает непрерывную перенос данных из множества источников баз данных на платформы данных Azure с минимальным временем простоя.

- DMS объединяет в себе функциональные возможности существующих средств и служб. Она использует Помощник по миграции данных (DMA) для создания отчетов об оценке с рекомендациями по совместимости баз данных и необходимым изменениям.
- DMS использует простой процесс самостоятельной миграции с интеллектуальной оценкой, которая помогает устранять потенциальные проблемы перед миграцией.
- DMS может выполнить миграцию в нужном масштабе из нескольких источников в целевую базу данных Azure.
- DMS обеспечивает поддержку сред от SQL Server 2005 до SQL Server 2017.

DMS — не единственный инструмент для переноса баз данных, предлагаемый корпорацией Майкрософт. Вы можете изучить [сравнение инструментов и служб](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services).

##### <a name="using-dms-at-scale"></a>Использование DMS в нужном масштабе

Компания Contoso использует DMS при миграции из среды SQL Server.

- При подготовке DMS компании необходимо настроить правильный размер и оптимизировать производительность для переноса данных. Компания Contoso выберет параметр "Business-critical tier with 4 vCores" (Уровень критически важных для бизнеса ресурсов с 4 виртуальными ядрами), чтобы служба могла воспользоваться преимуществами нескольких ЦП для параллелизации и ускорения передачи данных.

    ![Масштабирование DMS](./media/contoso-migration-scale/dms.png)

- Еще один способ масштабирования, доступный компании Contoso, — временное увеличение масштаба целевого экземпляра базы данных SQL Azure или MySQL до номера SKU ценовой категории "Премиум" во время переноса данных. Это сводит к минимуму регулирование баз данных, которое может повлиять на операции передачи данных при использовании номеров SKU более низких ценовых категорий.

##### <a name="using-other-tools"></a>Использование других инструментов

В дополнение к DMS компания Contoso может использовать другие инструменты и службы для получения сведений о виртуальных машинах.

- У нее имеются сценарии для упрощения миграции вручную. Они хранятся в репозитории GitHub.
- Для миграции может также использоваться ряд [инструментов от партнеров](https://azure.microsoft.com/migration/partners).

## <a name="phase-3-optimize"></a>Этап 3. Оптимизация

После того, как компания Contoso переместит ресурсы в Azure, их нужно упростить, чтобы увеличить производительность и повысить рентабельность инвестиций с помощью инструментов управления затратами. Учитывая, что Azure — это служба с оплатой по мере использования, для компании Contoso крайне важно понять, как работают системы, и убедиться, что их размер выбран правильно.

### <a name="azure-cost-management"></a>Управление затратами Azure

Чтобы повысить рентабельность инвестиций в облако, компания Contoso будет использовать бесплатный инструмент "Управление затратами Azure".

- С помощью этого лицензированного решения, разработанного Cloudyn, дочерним подразделением корпорации Майкрософт, компания Contoso может прозрачно и точно управлять расходами на облако. Оно предоставляет инструменты для мониторинга, распределения и сокращения затрат на облако.
- Управление затратами Azure предоставляет простые отчеты на панели мониторинга, позволяющие распределять затраты, а также управлять виртуальными счетами и возвратными платежами.
- Управление затратами может оптимизировать расходы на облако, выявляя недостаточно нагруженные ресурсы, которые компания Contoso может настроить и использовать.
- Дополнительные сведения об управлении расходами см. [на этой странице](/azure/cost-management/overview).

![Управление затратами](./media/contoso-migration-scale/cost-management.png)

### <a name="native-tools"></a>Собственные инструменты

Компания Contoso также будет использовать сценарии для поиска неиспользуемых ресурсов.

- При крупной миграции часто остаются фрагменты данных, например виртуальные жесткие диски (VHD), которые подлежат оплате, но уже не представляют ценности для компании. Используемые сценарии хранятся в репозитории GitHub.
- Компания Contoso воспользуется результатами работы, выполненной ИТ-отделом корпорации Майкрософт, и рассмотрит возможность реализации набора средств оптимизации ресурсов Azure (ARO).
- Компания Contoso может развернуть учетную запись службы автоматизации Azure с предварительно настроенными модулями runbook и расписаниями в своей подписке, чтобы начать экономить средства. Оптимизация ресурсов Azure в подписке происходит автоматически после включения или создания расписания, включая оптимизацию новых ресурсов.
- Это обеспечивает возможности децентрализованной автоматизации для снижения затрат. Можно указать следующие особенности.
  - Автоматическое откладывание обработки виртуальных машин Azure при недостаточном числе ресурсов ЦП.
  - Планирование откладывания и возобновления обработки виртуальных машин Azure.
  - Планирование откладывания и возобновления обработки виртуальных машин Azure по возрастанию или убыванию с помощью тегов Azure.
  - Массовое удаление групп ресурсов по запросу.
- Приступите к работе с набором средств АRО, доступном в этом [репозитории GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

### <a name="partner-optimization-tools"></a>Инструменты оптимизации запросов

Можно использовать такие инструменты от партнеров, как [Hanu](https://hanu.com/insight) и [Scalr]( https://www.scalr.com/cost-optimization).

## <a name="phase-4-secure-and-manage"></a>Этап 4. Защита и управление

На этом этапе компания Contoso использует ресурсы защиты и управления Azure для контроля, защиты и мониторинга облачных приложений в Azure. Эти ресурсы помогают работать с защищенной и хорошо управляемой средой, используя продукты, доступные на портале Azure. Компания Contoso начинает использовать эти инструменты во время миграции. Благодаря поддержке гибридного использования Azure большинство из этих решений обеспечивают согласованную работу с гибридным облаком.

### <a name="security"></a>Безопасность

Компания Contoso будет использовать центр безопасности Azure, чтобы обеспечить унифицированное управление безопасностью и расширенную защиту от угроз для гибридных облачных рабочих нагрузок.

- Центр безопасности позволяет получить полные сведения о безопасности ваших облачных приложений в Azure и обеспечить контроль над ними.
- Компания Contoso может быстро обнаруживать угрозы и реагировать на них, а также снижать уровень риска угроз, активировав адаптивную защиту.

[Узнайте больше](https://azure.microsoft.com/services/security-center) о центре безопасности Azure.

### <a name="monitoring"></a>Отслеживание

Компании Contoso необходимо отслеживать работоспособность и производительность недавно перенесенных на платформу Azure приложений, инфраструктуры и данных. Компания воспользуется встроенными инструментами мониторинга облака Azure, такими как Azure Monitor, рабочая область Log Analytics и Application Insights.

- С их помощью компания Contoso может легко собирать данные из ресурсов и получать подробные аналитические сведения. Например, компания Contoso может получать данные об использовании памяти, дисков и ЦП для виртуальных машин с помощью датчиков, просматривать зависимости приложений и сети для нескольких виртуальных машин, а также отслеживать производительность приложений.
- С помощью этих облачных инструментов мониторинга компания приступит к работе и выполнит интеграцию с решениями по управлению службами.
- [Узнайте больше](/azure/monitoring-and-diagnostics/monitoring-overview) о мониторинге Azure.

### <a name="business-continuity-and-disaster-recovery"></a>Непрерывность бизнес-процессов и аварийное восстановление

Компании Contoso потребуется стратегия непрерывности бизнес-процессов и аварийного восстановления (BCDR) для ресурсов Azure.

- Azure предоставляет [встроенные функции BCDR](/azure/architecture/resiliency/disaster-recovery-azure-applications) для защиты данных и обеспечения работоспособности приложений и служб.
- Помимо использования встроенных функций, компании Contoso необходимо обеспечить восстановление после сбоев, избежать дорогостоящего прерывания работы, выполнить требования соответствия и защитить данные от программ-шантажистов и ошибок пользователей. Выполните указанные ниже действия.
  - Компания Contoso развернет экономичное решение Azure Backup для резервного копирования ресурсов Azure. Так как это встроенная служба, настроить резервное копирование в облако можно за несколько простых шагов.
  - Компания Contoso настроит аварийное восстановление виртуальных машин Azure с помощью Azure Site Recovery. Это решение будет использоваться для репликации, отработки отказа и восстановления размещения между указанными регионами Azure. Это гарантирует, что приложения, работающие на виртуальных машинах Azure, останутся доступными в дополнительном регионе по выбору компании Contoso при возникновении сбоев в основном регионе. [Узнайте больше](/azure/site-recovery/azure-to-azure-quickstart).

## <a name="conclusion"></a>Заключение

В этой статье было описано планирование миграции в Azure в нужном масштабе, выполненное компанией Contoso. Процесс миграции был разделен на четыре этапа. Начав с оценки и миграции, после выполнения миграции компания перешла к оптимизации, защите и управлению. В большинстве случаев важно спланировать проект миграции как единый процесс, но переносить системы в организации, разделяя наборы компонентов на классификации и количества, которые лучше подходят для организации. Оценивая данные и применяя классификации, можно разделить проект на ряд небольших миграций, которые можно выполнить быстро и безопасно. Совокупность этих меньших миграций быстро превратится в большую успешную миграцию к Azure.