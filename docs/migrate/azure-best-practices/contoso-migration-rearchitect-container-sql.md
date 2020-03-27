---
title: Перепроектирование приложения и перенос в контейнер Azure и Базу данных SQL Azure
description: Узнайте, как выполнить переопределение архитектуры локального приложения в контейнер Azure и базу данных SQL Azure с помощью инфраструктуры внедрения в облако для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 83a5c356f5144700173fa4df593e313e44e3172f
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356360"
---
<!-- cSpell:ignore reqs contosohost contosodc contosoacreus contososmarthotel smarthotel vcenter WEBVM SQLVM -->

# <a name="rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a>Повторное проектирование локального приложения на контейнеры Azure и Базу данных SQL Azure

В этой статье показано, как вымышленная компания Contoso перерабатывает приложение с двумя уровнями Windows .NET, работающее на виртуальных машинах VMware, в рамках миграции в Azure. Contoso переносит интерфейсную виртуальную машину в контейнер Azure для Windows, а базу данных приложения — в базу данных Azure SQL.

Приложение SmartHotel360, используемое в этом примере, предоставляется в виде открытого кода. Если вы хотите использовать его для тестирования, то можете скачать это приложение с сайта [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Бизнес-факторы

Совместными усилиями ИТ-руководство Contoso и деловые партнеры определили указанные ниже цели этой миграции.

- **Адаптация к расширению бизнеса.** По мере развития компании Contoso растет нагрузка на локальные системы и инфраструктуру.
- **Повышение эффективности.** Contoso необходимо удалить ненужные процедуры и оптимизировать процессы для разработчиков и пользователей. Бизнес нуждается в том, чтобы ИТ были быстрыми и чтобы не тратить время или деньги, обеспечивая более высокие требования клиентов.
- **Повышение гибкости.** ИТ-отдел компании Contoso должен проявлять большую гибкость в отношении потребностей бизнеса. Должна реагировать быстрее, чем изменения на рынке, чтобы включить успех в глобальную экономику реагирования. Он не должен мешать или становиться помехой для бизнеса.
- **Масштабирование.** По мере успешного развития бизнеса компания Contoso должна предоставлять системы, которые могут расти в том же темпе.
- **Сокращение затрат.** Компании Contoso требуется минимизировать затраты на лицензирование.

## <a name="migration-goals"></a>Цели миграции

Группа, работающая над облачной инфраструктурой компании Contoso, определила цели этой миграции. Эти цели использовались для определения оптимального метода миграции.

<!-- markdownlint-disable MD033 -->

**Цели** | **Сведения**
--- | ---
**Требования приложения** | Потребность использовать приложение в Azure всегда будет критически важной.<br/><br/> Должны быть доступны те же возможности производительности, что и в настоящее время в VMware.<br/><br/> Компания Contoso хочет прерывать поддержку Windows Server 2008 R2, на которой в настоящее время размещается приложение, а компания Contoso готова вкладывать приложения в приложение.<br/><br/> Компания Contoso хочет отказаться от SQL Server 2008 R2 до современной управляемой платформы баз данных и свести к минимуму потребность в управлении.<br/><br/> Contoso хочет использовать преимущества своих инвестиций в лицензирование SQL Server и Software Assurance по мере возможности.<br/><br/> Компания Contoso хочет масштабировать веб-уровень приложения по мере необходимости.
**Ограничения** | Приложение состоит из приложения ASP.NET и службы WCF, работающей на той же виртуальной машине. Contoso хочет разделить его между двумя веб-приложениями, используя Службу приложений Azure.
**Требования Azure** | Contoso хочет перенести приложение в Azure и запускать его в контейнере для более продолжительной работы. Но реализовать его в Azure с нуля они не хотят.
**DevOps** | Contoso хочет перейти на модель DevOps, используя Azure DevOps Services для конвейера сборки и выпуска кода.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Архитектура решения

Определив свои цели и требования, специалисты компании Contoso начинают разработку и анализ решения для развертывания и планируют процесс миграции, включая службы Azure, которые будут использоваться в ходе этой миграции.

### <a name="current-app"></a>Текущее приложение

- Локальное приложение SmartHotel360 распределено на уровни на двух виртуальных машинах (WEBVM и SQLVM).
- Виртуальные машины расположены на узле VMware ESXi **contosohost1.contoso.com** (версии 6.5).
- Средой VMware управляет сервер vCenter Server 6.5 (**vcenter.contoso.com**), который запущен на виртуальной машине.
- Contoso использует локальный центр обработки данных (contoso-datacenter) с локальным контроллером домена (**contosodc1**).
- После завершения миграции локальные виртуальные машины в центре обработки данных Contoso будут выведены из эксплуатации.

### <a name="proposed-architecture"></a>Предлагаемая архитектура

- Для уровня базы данных приложения компания Contoso сравнивает Базу данных SQL Azure с SQL Server (в [этой статье](https://docs.microsoft.com/azure/sql-database/sql-database-features)). Принимается решение продолжить работу с Базой данных SQL Azure по нескольким причинам:
  - База данных SQL Azure — это управляемая реляционная база данных. Она обеспечивает прогнозируемую производительность на нескольких уровнях обслуживания с почти нулевым администрированием. Среди преимуществ: динамическая масштабируемость без простоя, встроенная интеллектуальная оптимизация, глобальная масштабируемость и доступность.
  - Contoso использует упрощенную версию Помощника по миграции данных (DMA) для оценки и переноса локальной базы данных в SQL Azure.
  - Software Assurance позволит Contoso приобрести Базу данных SQL по сниженной цене, воспользовавшись Преимуществом гибридного использования Azure для SQL Server. Это может обеспечить экономию до 30 %.
  - База данных SQL предоставляет ряд функций безопасности, включая постоянное шифрование, динамическое маскирование данных, обеспечение безопасности на уровне строк и обнаружение угроз.
- Что касается веб-уровня приложения, компания Contoso решила преобразовать его в контейнер Windows с помощью служб Azure DevOps Services.
  - Contoso развернет приложение, используя Azure Service Fabric, и извлечет образ контейнера Windows из Реестра контейнеров Azure (ACR).
  - Прототип расширения приложения для включения анализа тональности будет реализован как еще одна служба в Service Fabric, подключенная к Cosmos DB. Он будет считывать сведения из твитов и отображать их в приложении.
- Чтобы реализовать конвейер DevOps, компания Contoso будет использовать Azure DevOps для управления исходным кодом (SCM) с репозиториями Git. Для сборки кода, а также его развертывания в Реестре контейнеров Azure и Azure Service Fabric будут использоваться автоматизированные сборки и выпуски.

    ![Архитектура сценария](./media/contoso-migration-rearchitect-container-sql/architecture.png)

### <a name="solution-review"></a>Проверка решения

Специалисты Contoso оценивают предлагаемый дизайн, составляя список плюсов и минусов.

<!-- markdownlint-disable MD033 -->

**Рассмотрение** | **Сведения**
--- | ---
**Преимущества** | Код приложения SmartHotel360 необходимо изменить для миграции в Azure Service Fabric. Тем не менее реализация изменений требует минимальных усилий при использовании инструментов пакета SDK для Service Fabric.<br/><br/> С переходом на Service Fabric Contoso может приступить к разработке микрослужб, чтобы через какое-то время быстро добавить их в приложение без риска для исходной базы кода.<br/><br/> Контейнеры Windows предоставляют те же преимущества, что контейнеры в целом. Они повышают гибкость, мобильность и управление.<br/><br/> Contoso может использовать преимущества своих инвестиций в программу Software Assurance, используя Преимущество гибридного использования Azure для SQL Server и Windows Server.<br/><br/> После миграции можно будет отказаться от поддержки Windows Server 2008 R2. [Дополнительные сведения](https://support.microsoft.com/lifecycle)<br/><br/> Contoso может настроить веб-уровень приложения с несколькими экземплярами, после чего он больше не будет являться единой точкой отказа.<br/><br/> Исчезнет зависимость от устаревающей платформы SQL Server 2008 R2.<br/><br/> База данных SQL поддерживает технические требования Contoso. Администраторы Contoso провели оценку локальной базы данных с помощью Помощника по миграции данных и установили, что она является совместимой.<br/><br/> База данных SQL содержит встроенные средства обеспечения отказоустойчивости, которые специалистам Contoso не нужно настраивать. Это гарантия того, что уровень данных больше не является единой точкой отказа.
**Недостатки** | По сравнению с другими вариантами миграции контейнеры более сложные. Для Contoso длительное изучение контейнеров может стать проблемой. Новый уровень сложности контейнеров представляет большую ценность, несмотря на длительное время, которое требуется на их изучение.<br/><br/> Рабочей группе в Contoso необходимо будет заполнить пробелы в знаниях, чтобы разобраться с Azure, контейнерами и микрослужбами приложения и обеспечить их обслуживание.<br/><br/> Если компания Contoso использует Помощник по миграции данных вместо Azure Database Migration Service для миграции базы данных, инфраструктура не будет готова к миграции баз данных в нужном масштабе.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Процесс миграции

1. Contoso подготавливает кластер Azure Service Fabric для Windows.

1. Компания подготавливает экземпляр SQL Azure и переносит в него базу данных SmartHotel360.

1. С помощью инструментов SDK для Service Fabric Contoso преобразует виртуальную машину веб-уровня в контейнер Docker.

1. Она подключает кластер Service Fabric и ACR и развертывает приложение с помощью Azure Service Fabric.

    ![Процесс миграции](./media/contoso-migration-rearchitect-container-sql/migration-process.png)

### <a name="azure-services"></a>Службы Azure

**Служба** | **Описание** | **Стоимость**
--- | --- | ---
[Помощник по миграции данных (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Оценивает и обнаруживает проблемы совместимости, которые могут повлиять на функциональность базы данных в Azure. Помощник оценивает соотношение характеристик между источниками и целями SQL и предоставляет рекомендации по улучшению производительности и надежности. | Это средство можно загрузить бесплатно.
[База данных SQL Azure](https://azure.microsoft.com/services/sql-database) | Предоставляет интеллектуальную, полностью управляемую реляционную облачную службу баз данных. | Стоимость зависит от функций, пропускной способности и размера. [Дополнительные сведения](https://azure.microsoft.com/pricing/details/sql-database/managed)
[Реестр контейнеров Azure](https://azure.microsoft.com/services/container-registry) | Хранит образы для всех типов развертываний контейнеров. | Стоимость зависит от функций, типа хранилища и длительности использования. [Дополнительные сведения](https://azure.microsoft.com/pricing/details/container-registry)
[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) | Эта служба предназначена для создания и использования постоянно доступных, масштабируемых и распределенных приложений. | Стоимость зависит от размера, расположения и продолжительности работы вычислительных узлов. [Дополнительные сведения](https://azure.microsoft.com/pricing/details/service-fabric)
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Предоставляет конвейер непрерывной интеграции и непрерывного развертывания (CI/CD) для разработки приложений. Конвейер запускается с репозиторием Git для управления кодом приложения, системой сборки для создания пакетов и других артефактов сборки и системой управления выпусками для развертывания изменений в средах разработки, тестирования и рабочей среде.

## <a name="prerequisites"></a>предварительные требования

Ниже показано, что необходимо компании Contoso для реализации этого сценария.

<!-- markdownlint-disable MD033 -->

**Требования** | **Сведения**
--- | ---
**Подписка Azure.** | Специалисты Contoso создали подписки ранее в этой серии статей. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Если вы создаете бесплатную учетную запись, вы являетесь администратором своей подписки и можете выполнять любые действия.<br/><br/> Если вы используете существующую подписку, в которой не являетесь администратором, администратор должен назначить вам права владельца или участника.
**Инфраструктура Azure** | [Узнайте, как](./contoso-migration-infrastructure.md) компания Contoso ранее настроила инфраструктуру Azure.
**Предварительные требования для разработчика** | Contoso необходимы следующие средства на рабочей станции разработчика:<br/><br/> - [выпуск Visual Studio Community 2017 15.5](https://www.visualstudio.com);<br/><br/> включенная рабочая нагрузка .NET;<br/><br/> - [Git](https://git-scm.com);<br/><br/> - [пакет SDK для Service Fabric версии 3.0 или более поздней](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started);<br/><br/> - [Docker CE (Windows 10) или Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install), настроенные на использование контейнеров Windows.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Шаги выполнения сценария

Ниже рассказывается, как выполняется миграция в компании Contoso.

> [!div class="checklist"]
>
> - **Шаг 1. подготавливает экземпляр базы данных SQL в Azure.** Специалисты компании Contoso выполняют подготовку экземпляра SQL в Azure. После миграции интерфейсной виртуальной машины уровня Интернета в контейнер Azure экземпляр контейнера с внешним веб-интерфейсом приложения будет указывать на эту базу данных.
> - **Шаг 2. Создание реестра контейнеров Azure (запись контроля доступа).** Contoso подготавливает корпоративный реестр контейнеров для образов контейнеров Docker.
> - **Шаг 3. подготавливаете Service Fabric Azure.** Подготавливает к работе кластер Service Fabric
> - **Шаг 4. Управление сертификатами Service Fabric.** Компания Contoso настраивает сертификаты для доступа Azure DevOps Services к кластеру.
> - **Шаг 5. Перенос базы данных с помощью DMA.** Специалисты Contoso переносят базу данных приложения с помощью Помощника по миграции данных.
> - **Шаг 6. Настройка Azure DevOps Services.** Компания Contoso настраивает новый проект в Azure DevOps Services и импортирует код в репозиторий Git.
> - **Шаг 7. Преобразование приложения.** Компания Contoso преобразовывает приложение в контейнер с помощью инструментов Azure DevOps и SDK.
> - **Шаг 8. Настройка сборки и выпуска.** Contoso настраивает конвейеры сборки и выпуска, чтобы создать и опубликовать приложение в Реестре контейнеров Azure и кластере Service Fabric.
> - **Шаг 9. расширение приложения.** После того как приложение становится общедоступным, Contoso расширяет его, чтобы использовать возможности Azure, а затем повторно публикует его в Azure с помощью конвейера.

## <a name="step-1-provision-an-azure-sql-database"></a>Шаг 1. Подготовка базы данных SQL Azure

Администраторы Contoso подготавливают базу данных SQL Azure.

1. Они решают создать **базу данных SQL** в Azure.

    ![Подготовка SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

1. Администраторы указывают имя базы данных в соответствии с базой данных, работающей на локальной виртуальной машине (**SmartHotel.Registration**). Они размещают базу данных в группе ресурсов ContosoRG. Это группа ресурсов, которую специалисты компании используют для рабочих ресурсов в Azure.

    ![Подготовка SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

1. Специалисты компании настраивают новый экземпляр SQL Server (**sql-smarthotel-eus2**) в основном регионе.

    ![Подготовка SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

1. Они задают ценовую категорию в соответствии с потребностями сервера и базы данных, а также предпочитают сэкономить с помощью предложения "Преимущество гибридного использования Azure", так как у них уже есть лицензия SQL Server.

1. Для определения размера они используют вариант приобретения на основе виртуальных ядер и устанавливают ограничения в соответствии с ожидаемыми требованиями.

    ![Подготовка SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

1. Затем они создают экземпляр базы данных.

    ![Подготовка SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

1. После создания экземпляра они открывают базу данных и отмечают сведения, которые им нужны при использовании Помощника по миграции данных.

    ![Подготовка SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)

**Нужна дополнительная помощь?**

- [Получение справки](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) о подготовке Базы данных SQL.
- [Дополнительные сведения об](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) ограничениях ресурсов в модели приобретения на основе виртуальных ядер.

## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a>Шаг 2. Создание Реестра контейнеров Azure и подготовка контейнера Azure

Контейнер Azure создается с использованием экспортированных файлов из виртуальной машины веб-уровня. Контейнер размещается в Реестре контейнеров Azure (ACR).

1. Администраторы Contoso создают Реестр контейнеров на портале Azure.

     ![Реестр контейнеров](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

1. Специалисты компании предоставляют имя для реестра (**contosoacreus2**) и размещают его в основном регионе в группе ресурсов, которая используется для ресурсов инфраструктуры. Они обеспечивают доступ для администраторов и устанавливают для реестра номер SKU ценовой категории "Премиум", чтобы была возможность использовать георепликацию.

    ![Реестр контейнеров](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)

## <a name="step-3-provision-azure-service-fabric"></a>Шаг 3. Подготовка Azure Service Fabric

Контейнер SmartHotel360 будет запускаться в кластере Azure Service Fabric. Администраторы Contoso создают кластер Service Fabric следующим образом:

1. Создайте ресурс Service Fabric в Azure Marketplace.

     ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

1. В разделе **основных сведений** специалисты компании предоставляют уникальное имя DS для кластера и учетные данные для доступа к локальной виртуальной машине. Они размещают ресурс в рабочей группе ресурсов (**ContosoRG**) в основном регионе "Восточная часть США 2".

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png)

1. В разделе **Конфигурация типа узла** нужно ввести имя типа узла, параметры устойчивости, размер виртуальной машины и конечные точки приложения.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png)

1. В разделе **Создать Key Vault** они создают Key Vault в своей группе ресурсов инфраструктуры. В нем будет размещаться сертификат.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png)

1. В разделе **Политики доступа** они предоставляют доступ к виртуальным машинам для развертывания хранилища ключей.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png)

1. Затем нужно указать имя для сертификата.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png)

1. На странице сводки специалисты компании копируют ссылку, используемую для загрузки сертификата. Это необходимо для подключения к кластеру Service Fabric.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png)

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png)

1. После успешной проверки они подготавливают кластер.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png)

1. В мастере импорта сертификатов специалисты импортируют загруженный сертификат на компьютеры разработки. Сертификат используется для проверки подлинности в кластере.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png)

1. После подготовки кластера специалисты компании подключаются к проводнику кластеров Service Fabric Explorer.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png)

1. Им нужно выбрать правильный сертификат.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png)

1. После загрузки Service Fabric Explorer администратор Contoso может управлять кластером.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png)

## <a name="step-4-manage-service-fabric-certificates"></a>Шаг 4. Управление сертификатами Service Fabric

Компании Contoso необходимы сертификаты кластера, чтобы разрешить Azure DevOps Services доступ к нему. Администраторы Contoso настраивают их.

1. Они открывают портал Azure и переходят к Key Vault.

1. Они открывают сертификаты и копируют отпечаток сертификата, созданного в ходе подготовки.

    ![Копирование отпечатка](./media/contoso-migration-rearchitect-container-sql/cert1.png)

1. Они копируют его в текстовый файл для последующего использования.

1. Теперь они добавляют сертификат клиента, который будет использовать администратор на кластере. Это позволяет Azure DevOps Services подключаться к кластеру для развертывания приложений в контейнере выпуска. Для этого они открывают Key Vault на портале, а затем выбирают **сертификаты** > **создать/импортировать**.

    ![Создание сертификата клиента](./media/contoso-migration-rearchitect-container-sql/cert2.png)

1. Они вводят имя сертификата и указывают различающееся имя X.509 в поле **Субъект**.

     ![Имя сертификата](./media/contoso-migration-rearchitect-container-sql/cert3.png)

1. После создания сертификата они скачивают его в локальную среду в формате PFX.

     ![Скачивание сертификата](./media/contoso-migration-rearchitect-container-sql/cert4.png)

1. Теперь они возвращаются к списку сертификатов в Key Vault и копируют отпечаток нового сертификата клиента. Они сохраняют его в текстовом файле.

     ![Отпечаток сертификата клиента](./media/contoso-migration-rearchitect-container-sql/cert5.png)

1. Для развертывания Azure DevOps Services необходимо определить значение сертификата в кодировке Base64. Они делают это на локальной рабочей станции разработчика с помощью PowerShell. Они вставляют выходные данные в текстовый файл для последующего использования.

    ```powershell
    [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx"))
    ```

     ![Значение в кодировке Base64](./media/contoso-migration-rearchitect-container-sql/cert6.png)

1. Наконец, они добавляют новый сертификат в кластер Service Fabric. Для этого на портале они открывают кластер, а затем выберите **Безопасность**.

     ![Добавление сертификата клиента](./media/contoso-migration-rearchitect-container-sql/cert7.png)

1. Они выбирают **Добавить** > **Клиент администратора** и вставляют отпечаток нового сертификата клиента. Затем они выбирают **Добавить**. Это может занять до 15 минут.

     ![Добавление сертификата клиента](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a>Шаг 5. Перенос базы данных с помощью DMA

Теперь администраторы Contoso могут перенести базу данных SmartHotel360 с помощью DMA.

### <a name="install-dma"></a>Установка DMA

1. Они загружают инструмент с [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=53595) к локальной виртуальной машине SQL Server (**SQLVM**).

1. Они запускают установку (DownloadMigrationAssistant.msi) на виртуальной машине.

1. Перед закрытием мастера на странице **Готово** необходимо выбрать **Launch Microsoft Data Migration Assistant** (Запустить помощник по миграции данных Майкрософт).

### <a name="configure-the-firewall"></a>Настройка брандмауэра

Чтобы подключиться к базе данных Azure SQL, администраторы Contoso настраивают правило брандмауэра, разрешающее доступ.

1. В свойствах **брандмауэра и виртуальных сетей** для базы данных специалисты компании разрешают доступ к службам Azure и добавляют правило для клиентского IP-адреса локальной виртуальной машины SQL Server.

1. Создается правило брандмауэра на уровне сервера.

    ![Брандмауэр](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

**Нужна дополнительная помощь?**

[Узнайте о](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) создании правил брандмауэра для Базы данных SQL Azure и управлении ими.

### <a name="migrate"></a>Миграция

Теперь администраторы Contoso переносят базу данных.

1. В канале DMA создайте новый проект (**смарсотелдб**), а затем выберите **Миграция**.

1. Специалисты компании выбирают тип исходного сервера **SQL Server**, а целевого — **База данных SQL Azure**.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

1. В подробностях о миграции они добавляют **SQLVM** в качестве исходного сервера и базу данных **SmartHotel.Registration**.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

1. Они получают ошибку, которая, по всей видимости, связана с проверкой аутентификации. Однако после анализа оказывается, что проблема заключается в наличии точки (.) в имени базы данных. В качестве обходного решения специалисты компании решают подготовить новую базу данных SQL, используя имя **SmartHotel-Registration**. При повторном запуске DMA можно выбрать **смарсотел-Registration**и продолжить работу с мастером.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

1. На вкладке **выбора объектов** они выбирают таблицы базы данных и генерируют скрипт SQL.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

1. После того как DMA создаст сценарий, они выбирают **Deploy schema** (Развернуть схему).

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

1. DMA подтверждает, что развертывание выполнено успешно.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

1. Теперь специалисты компании начинают процесс миграции.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

1. После завершения миграции Contoso может проверить, что база данных запущена в экземпляре SQL Azure.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

1. Специалисты компании удаляют на портале Azure дополнительную базу данных SQL **SmartHotel.Registration**.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)

## <a name="step-6-set-up-azure-devops-services"></a>Шаг 6. Настройка Azure DevOps Services

Компании Contoso необходимо создать инфраструктуру DevOps и конвейеры для приложения. Для этого администраторы Contoso создают проект Azure DevOps, импортируют свой код, а затем — конвейеры сборки и выпуска.

1. В учетной записи Contoso Azure DevOps создайте новый проект (**контососмарсотелреарчитект**), а затем выберите **Git** для управления версиями.
![Новый проект](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

1. Они импортируют репозиторий Git, в котором на данный момент хранится код их приложения. Он хранится в [общедоступном репозитории](https://github.com/Microsoft/SmartHotel360-internal-booking-apps), и вы можете скачать его.

    ![Скачивание кода приложения](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

1. После импорта кода они подключают Visual Studio к репозиторию и клонируют код с помощью Team Explorer.

1. После клонирования репозитория на компьютер для разработки они открывают файл решения для приложения. В этом файле у веб-приложения и службы WCF есть отдельные проекты.

    ![Файл решения](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a>Шаг 7. Преобразование приложения в контейнер

Локальное приложение является традиционным трехуровневым приложением:

- Оно содержит веб-формы и службу WCF, которая подключается к SQL Server.
- Оно использует Entity Framework для интеграции с данными в базе данных SQL, предоставляя их через службу WCF.
- Приложение WebForms взаимодействует со службой WCF.

Администраторы Contoso преобразуют приложение в контейнер с помощью Visual Studio и SDK Tools следующим образом:

1. Используя Visual Studio, они просматривают открытый файл решения (SmartHotel.Registration.sln) в каталоге **SmartHotel360-internal-booking-apps\src\Registration** локального репозитория. Показаны два приложения. Внешний веб-интерфейс SmartHotel.Registration.Web и приложение службы WCF SmartHotel.Registration.WCF.

    ![Контейнер](./media/contoso-migration-rearchitect-container-sql/container2.png)

1. Далее нужно щелкнуть веб-приложение правой кнопкой мыши > **Добавить** > **Container Orchestrator Support** (Поддержка оркестратора контейнеров).

1. В окне **поддержки оркестратора контейнеров** нужно выбрать **Service Fabric**.

    ![Контейнер](./media/contoso-migration-rearchitect-container-sql/container3.png)

1. Они повторяют процесс для приложения SmartHotel.Registration.WCF.

1. Теперь они проверяют, как изменилось решение.

    - Новое приложение — **SmartHotel.RegistrationApplication/** .
    - Оно содержит две службы: **SmartHotel.Registration.WCF** и **SmartHotel.Registration.Web**.

    ![Контейнер](./media/contoso-migration-rearchitect-container-sql/container4.png)

1. С помощью Visual Studio был создан файл Docker и локально извлечены на компьютер разработчика требуемые образы.

    ![Контейнер](./media/contoso-migration-rearchitect-container-sql/container5.png)

1. Файл манифеста (**ServiceManifest.xml**) создается и открывается в Visual Studio. Этот файл сообщает Service Fabric, как настроить контейнер, когда он развернут в Azure.

    ![Контейнер](./media/contoso-migration-rearchitect-container-sql/container6.png)

1. Другой файл манифеста (**ApplicationManifest.xml) содержит приложения конфигурации для контейнеров.

    ![Контейнер](./media/contoso-migration-rearchitect-container-sql/container7.png)

1. Они открывают файл **ApplicationParameters/Cloud.xml** и обновляют строку подключения, чтобы подключить приложение к базе данных Azure SQL. Строку подключения можно найти в базе данных на портале Azure.

    ![Строка подключения](./media/contoso-migration-rearchitect-container-sql/container8.png)

1. Они фиксируют обновленный код и отправляют его в Azure DevOps Services.

    ![Commit](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a>Шаг 8. Конвейеры сборки и выпуска в Azure DevOps Services

Теперь администраторы Contoso настраивают Azure DevOps Services для сборки и выпуска, чтобы реализовать методики DevOps.

1. В Azure DevOps Services они выбирают **Сборка и выпуск** > **Новый конвейер**.

    ![Новый конвейер](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

1. Они выбирают **Azure DevOps Services Git** и соответствующий репозиторий.

    ![Git и репозиторий](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

1. В поле **Выберите шаблон** они выбирают структуру с поддержкой Docker.

     ![Структура и Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)

1. Специалисты компании меняют образы тегов действия для **создания образа** и настраивают задачу на использование подготовленного ACR.

     ![Реестр](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

1. В задаче **Push images** (Отправка образов) они настраивают отправку образа в ACR и включают последний тег.

1. В разделе **Триггеры** они включают непрерывную интеграцию и добавляют главную ветвь.

    ![Триггеры](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

1. Они выбирают **Сохранить и поместить в очередь**, чтобы начать выполнение сборки.

1. После успешной сборки они переходят к конвейеру выпуска. В Azure DevOps Services они выбирают **Выпуски** > **Новый конвейер**.

    ![Конвейер выпуска](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)

1. Они выбирают шаблон **Развертывание Azure Service Fabric** и указывают имя стадии (**SmartHotelSF**).

    ![Среда](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

1. Они указывают имя конвейера (**ContosoSmartHotel360Rearchitect**). Для этапа они выбирают вариант **1 задание, 1 задача**, чтобы настроить развертывание Service Fabric.

    ![Этап и задача](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

1. Теперь они нажимают кнопку **Создать**, чтобы добавить новое подключение к кластеру.

    ![Новое подключение](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

1. В окне **Add Service Fabric service connection** (Добавление подключения к службе Service Fabric) они настраивают подключение и параметры аутентификации, которые Azure DevOps Services будет использовать для развертывания приложения. На портале Azure можно указать расположение конечной точки кластера, и они добавляют префикс **tcp://** .

1. Собранные сведения о сертификате указываются в полях **Отпечаток сертификата сервера** и **Сертификат клиента**.

    ![Сертификат](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

1. Они выбирают конвейер и нажимают **Добавить артефакт**.

     ![Артефакт](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

1. Они выбирают проект и конвейер сборки, используя последнюю версию.

     ![Сборка](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

1. Обратите внимание, что молния на артефакте выбрана.

     ![Состояние артефакта](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

1. Кроме того, обратите внимание, что включен триггер непрерывного развертывания.
   ![Непрерывное развертывание включено](./media/contoso-migration-rearchitect-container-sql/pipeline14.png)

1. Они выбирают **Сохранить** > **Создать выпуск**.

    ![Release](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

1. По завершении развертывания SmartHotel360 будет работать в Service Fabric.

    ![Публикация](./media/contoso-migration-rearchitect-container-sql/publish4.png)

1. Чтобы подключиться к приложению, они направляют трафик по общедоступному IP-адресу подсистемы балансировки нагрузки Azure на узлах Service Fabric.

    ![Публикация](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a>Шаг 9. Расширение приложения и повторная публикация

Теперь, когда приложение SmartHotel360 и база данных запущены в Azure, Contoso хочет расширить приложение.

- Разработчики компании Contoso добавляют прототип нового приложения .NET Core, которое будет выполняться в кластере Service Fabric.
- Приложение будет использоваться для вывода данных тональности из Cosmos DB.
- Эти данные будут представлены в виде твитов, которые обрабатываются с помощью бессерверной функции Azure и API анализа текста Azure Cognitive Services.

### <a name="provision-azure-cosmos-db"></a>Подготовка Azure Cosmos DB

Сначала администраторы Contoso готовят базу данных Cosmos Azure.

1. Специалисты компании создают ресурс Azure Cosmos DB в Azure Marketplace.

    ![Расширение](./media/contoso-migration-rearchitect-container-sql/extend1.png)

1. Они предоставляют имя базы данных (**contososmarthotel**), выбирают API SQL и размещают ресурс в группе рабочих ресурсов в основном регионе "Восточная часть США 2".

    ![Расширение](./media/contoso-migration-rearchitect-container-sql/extend2.png)

1. В разделе о **начале работы** они выбирают **Обозреватель данных** и добавляют новую коллекцию.

1. В разделе **Добавить коллекцию** указываются идентификаторы и устанавливается емкость и пропускная способность.

    ![Расширение](./media/contoso-migration-rearchitect-container-sql/extend3.png)

1. На портале они открывают новую базу данных > **коллекцию** > **документы**, а затем выберите **создать документ**.

1. Далее в окно документа вставляется код JSON, приведенный ниже. Это пример данных в виде одного твита.

    ```json
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500,
            "hashtags": [
                ""
            ]
    }
    ```

    ![Расширение](./media/contoso-migration-rearchitect-container-sql/extend4.png)

1. Определяется конечная точка Cosmos DB и ключ проверки подлинности. Они используются в приложении для подключения к коллекции. В базе данных они выбирают **Ключи** и копируют универсальный код ресурса (URI) и первичный ключ в Блокнот.

    ![Расширение](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a>Обновление приложения тональности

Подготовив базу данных Cosmos DB, администраторы Contoso могут настроить приложение для подключения к ней.

1. В Visual Studio в обозревателе решений нужно открыть файл ApplicationModern\ApplicationParameters\cloud.xml.

    ![Приложение тональности](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

1. Заполняются следующие два параметра:

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Приложение тональности](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a>Повторная публикация приложения

После расширения приложения администраторы Contoso повторно публикуют его в Azure с помощью конвейера.

1. Они фиксируют и отправляют свой код в Azure DevOps Services. При этом запускаются конвейеры сборки и выпуска.

1. По завершении сборки и развертывания SmartHotel360 будет работать в Service Fabric. На консоли управления Service Fabric теперь отображаются три службы.

    ![Повторная публикация](./media/contoso-migration-rearchitect-container-sql/republish3.png)

1. Теперь, поочередно выбирая службы, они видят, что приложение SentimentIntegration запущено и работает.

    ![Повторная публикация](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a>Очистка после миграции

После миграции специалистам компании Contoso необходимо выполнить указанные ниже действия по очистке.

- Удалите локальные виртуальные машины из перечня в vCenter.
- Удалить виртуальные машины из локальных заданий резервного копирования.
- Обновите внутреннюю документацию, чтобы показать новые расположения приложения SmartHotel360. Покажите базу данных как запущенную в Базе данных SQL Azure, а внешний интерфейс как запущенный в Service Fabric.
- Проверить все ресурсы, взаимодействующие с резервными виртуальными машинами, и обновить все соответствующие параметры или документы согласно новой конфигурации.

## <a name="review-the-deployment"></a>Проверка развертывания

Теперь, когда выполняется миграция ресурсов в Azure, компании Contoso необходимо полностью ввести его в эксплуатацию и защитить свою новую инфраструктуру.

### <a name="security"></a>безопасность

- Администраторам Contoso необходимо обеспечить безопасность своей новой базы данных **SmartHotel-Registration**. [Дополнительные сведения](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- В частности, нужно обновить контейнер для использования SSL с сертификатами.
- Необходимо рассмотреть возможность использования Key Vault для защиты секретов для приложений Service Fabric. [Дополнительные сведения](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management)

### <a name="backups"></a>Резервные копии

- Contoso следует рассмотреть требования резервного копирования для базы данных SQL Azure. [Дополнительные сведения](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Администраторам Contoso рекомендуется реализовать группы отработки отказа для обеспечения отказоустойчивости в регионе для базы данных. [Дополнительные сведения](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)
- Они могут использовать георепликацию для номера SKU ценовой категории "Премиум" Реестра контейнеров Azure. [Дополнительные сведения](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication)
- Contoso необходимо рассмотреть развертывание веб-приложения в основном регионе "Восточная часть США 2" и в регионе "Центральная часть США", когда Веб-приложение для контейнеров станет доступно. Администраторы Contoso могут настроить диспетчер трафика для обеспечения отработки отказа в случае региональных сбоев.
- Cosmos DB создает резервные копии автоматически. Чтобы узнать больше, специалисты Contoso [читают описание](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) этого процесса.

### <a name="licensing-and-cost-optimization"></a>Лицензирование и оптимизация затрат

- После развертывания всех ресурсов специалисты Contoso должны назначить теги Azure в соответствии с [планом инфраструктуры](./contoso-migration-infrastructure.md#set-up-tagging).
- Полное лицензирование входит в стоимость служб PaaS, которые использует Contoso. Это будет вычтено из EA.
- Компания будет использовать Управление затратами Azure по лицензии Cloudyn (дочернее подразделение корпорации Майкрософт). Это решение по управлению затратами для нескольких облаков, которое позволяет использовать облака Azure и другие облачные ресурсы, а также управлять ими. Дополнительные сведения об управлении расходами см. [на этой странице](https://docs.microsoft.com/azure/cost-management/overview).

## <a name="conclusion"></a>Заключение

В этой статье специалисты Contoso выполнили рефакторинг приложения SmartHotel360 в Azure путем миграции интерфейсной виртуальной машины приложения в Service Fabric. База данных приложения была перенесена в базу данных Azure SQL.
