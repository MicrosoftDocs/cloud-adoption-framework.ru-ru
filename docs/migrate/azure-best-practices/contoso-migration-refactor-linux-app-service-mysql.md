---
title: Рефакторинг приложения Linux в службе приложений Azure, диспетчере трафика и базе данных Azure для MySQL
description: Узнайте, как выполнить рефакторинг приложения службы поддержки Linux в службе приложений Azure и базе данных Azure для MySQL с помощью инфраструктуры внедрения в облако для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4e92222389dea22f22283c2014d89b6ea33008e4
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2020
ms.locfileid: "86192241"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc OSTICKETWEB OSTICKETMYSQL osTicket contosoosticket trafficmanager InnoDB binlog DBHOST DBUSER CNAME -->

# <a name="refactor-a-linux-application-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Рефакторинг приложения Linux в нескольких регионах с помощью службы приложений Azure, диспетчера трафика и базы данных Azure для MySQL

В этой статье показано, как вымышленная компания Contoso предоставляет многоуровневое приложение на [основе лампы](https://wikipedia.org/wiki/LAMP_(software_bundle)) , перенося его из локальной среды в Azure с помощью службы приложений Azure с интеграцией GitHub и базы данных Azure для MySQL.

Остиккет, приложение службы поддержки, используемое в этом примере, предоставляется в виде открытого кода. Если вы хотите использовать его для тестирования, вы можете скачать его из [репозитория остиккет на сайте GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Бизнес-факторы

Группа специалистов по ИТ тесно работала с бизнес-партнерами, чтобы понять, что они хотят достичь:

- **Устраните бизнес-рост.** Компания Contoso растет и переходит на новые рынки. Требуются дополнительные агенты обслуживания клиентов.
- **Измените.** Решение должно создаваться таким образом, чтобы компания Contoso имела возможность добавлять дополнительные агенты обслуживания пользователей по мере расширения бизнеса.
- **Повышение устойчивости.** В прошлом проблемы возникают только с системными, затронутыми внутренними пользователями. С новой бизнес-моделью будут затронуты внешние пользователи, и Contoso потребует, чтобы приложение выполнялось в любое время.

## <a name="migration-goals"></a>Цели миграции

Для определения наилучшего способа миграции команда Contoso по работе в облаке определила ее цели.

- Приложения должны масштабироваться за пределы текущих локальных ресурсов и производительности. Компания Contoso переносит приложение, чтобы воспользоваться преимуществом масштабирования по требованию в Azure.
- Компания Contoso хочет переместить базу кода приложения в конвейер непрерывной доставки. По мере изменения приложений в GitHub компания Contoso хочет развернуть эти изменения без задач для работы персонала.
- Приложение должно быть устойчивым к возможным расширению и отработке отказа. Компания Contoso хочет развернуть приложение в двух разных регионах Azure и настроить автоматическое масштабирование.
- Компании необходимо свести к минимуму задачи администрирования баз данных после переноса приложения в облако.

## <a name="solution-design"></a>Архитектура решения

Определив свои цели и требования, специалисты Contoso начинают разработку и анализ решения развертывания и идентифицируют процесс миграции, включая службы Azure, которые будут использоваться при этой миграции.

## <a name="current-architecture"></a>Текущая архитектура

- Приложение распределено между двумя виртуальными машинами ( `OSTICKETWEB` и `OSTICKETMYSQL` ).
- Виртуальные машины расположены на узле VMware ESXi `contosohost1.contoso.com` (версии 6.5).
- Среда VMware находится под управлением сервера vCenter Server 6.5 (`vcenter.contoso.com`), запущенного на виртуальной машине.
- Компания Contoso использует локальный центр обработки данных (`contoso-datacenter`) с локальным контроллером домена (`contosodc1`).

![Текущая архитектура](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Предлагаемая архитектура

Ниже приведена предлагаемая архитектура.

- Приложение веб-уровня в `OSTICKETWEB` будет перенесено путем создания службы приложений Azure в двух регионах Azure. Служба приложений Azure для Linux будет реализована с помощью контейнера DOCKER 7,0.
- Код приложения будет перемещен на сайт GitHub, а веб-приложение службы приложений Azure будет настроено для непрерывной поставки с GitHub.
- Служба приложений Azure будет развернута как в основном регионе ( `East US 2` ), так и в дополнительном регионе ( `Central US` ).
- Диспетчер трафика будет настроен для обслуживания двух веб-приложений Azure в обоих регионах.
- Диспетчер трафика будет настроен в режиме приоритета для принудительного передачи трафика `East US 2` .
- Если сервер приложений Azure находится в `East US 2` автономном режиме, пользователи могут получить доступ к приложению, для которого выполнена отработка отказа в `Central US` .
- База данных приложения будет перенесена в службу "база данных Azure для MySQL" с помощью Azure Database Migration Service. Будет создана локальная резервная копия локальной базы данных. Затем будет выполнено ее восстановление в Базу данных Azure для MySQL.
- База данных будет находиться в основном регионе ( `East US 2` ) в подсети базы данных () в `PROD-DB-EUS2` рабочей сети ( `VNET-PROD-EUS2` ):
- Так как выполняется перенос рабочей нагрузки, ресурсы Azure для приложения будут находиться в Рабочей группе ресурсов `ContosoRG` .
- Ресурс диспетчера трафика будет развернут в группе ресурсов инфраструктуры Contoso `ContosoInfraRG` .
- После завершения миграции локальные виртуальные машины в центре обработки данных Contoso будут выведены из эксплуатации.

![Архитектура сценария](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Процесс миграции

Порядок миграции в Contoso будет следующим:

1. В качестве первого шага администраторы Contoso настроили инфраструктуру Azure, включая подготовку службы приложений Azure, настройку диспетчера трафика и подготовку экземпляра базы данных Azure для MySQL.
2. После подготовки инфраструктуры Azure она переносит базу данных с помощью Azure Database Migration Service.
3. После запуска базы данных в Azure она находится в частном репозитории GitHub для службы приложений Azure с непрерывной доставкой и загружается с помощью приложения Остиккет.
4. В портал Azure они загружают приложение из GitHub в контейнер DOCKER, в котором выполняется служба приложений Azure.
5. Они изменяют параметры DNS и настраивают автоматическое масштабирование для приложения.

![Процесс миграции](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Службы Azure

| Служба | Описание | Стоимость |
| --- | --- | --- |
| [Служба приложений Azure](https://azure.microsoft.com/services/app-service) | Служба работает и масштабирует приложения, используя Azure PaaS для веб-сайтов. | Ценовая политика основывается на размере необходимых экземпляров и компонентов. [Подробнее](https://azure.microsoft.com/pricing/details/app-service/windows). |
| [Диспетчер трафика](https://azure.microsoft.com/services/traffic-manager) | Подсистема балансировки нагрузки, использующая DNS для перенаправления пользователей в Azure или на внешние веб-сайты и службы. | Ценообразование основано на количестве получаемых запросов DNS и отслеживаемых конечных точек. | [Подробнее](https://azure.microsoft.com/pricing/details/traffic-manager). |
| [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Azure Database Migration Service обеспечивает простой перенос из нескольких источников базы данных в платформы данных Azure с минимальным временем простоя. | Дополнительные сведения о [поддерживаемых регионах](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) см. на странице [цен на Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [База данных Azure для MySQL](https://docs.microsoft.com/azure/mysql) | База данных основана на ядре СУБД MySQL с открытым исходным кодом. Она предоставляет полностью управляемую корпоративную базу данных MySQL для сообщества для разработки и развертывания приложений. | Ценообразование основано на вычислении, хранении и резервном копировании. [Подробнее](https://azure.microsoft.com/pricing/details/mysql). |

## <a name="prerequisites"></a>Предварительные требования

Ниже показано, что необходимо сделать специалистам компании Contoso, чтобы реализовать этот сценарий.

| Требования | Сведения |
| --- | --- |
| **Подписка Azure.** | Специалисты Contoso создали подписки ранее в этой серии статей. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free). <br><br> Если вы создаете бесплатную учетную запись, вы являетесь администратором своей подписки и можете выполнять любые действия. <br><br> Если вы используете существующую подписку, в которой не являетесь администратором, администратор должен назначить вам права владельца или участника. |
| **Инфраструктура Azure** | Contoso настраивает свою инфраструктуру Azure, как описано в статье [Развертывание инфраструктуры Azure для миграции в Contoso](./contoso-migration-infrastructure.md). |

## <a name="scenario-steps"></a>Шаги выполнения сценария

Миграция в Contoso будет осуществляться следующим образом:

> [!div class="checklist"]
>
> - **Шаг 1. подготавливает службу приложений Azure.** Администраторы Contoso подготовят веб-приложения в основном и дополнительном регионах.
> - **Шаг 2. Настройка диспетчера трафика.** Они настраивают диспетчер трафика перед веб-приложениями с целью маршрутизации и балансировки нагрузки трафика.
> - **Шаг 3. Инициализация MySQL.** Они подготавливают в Azure экземпляр Базы данных MySQL для Azure.
> - **Шаг 4. Перенос базы данных.** Они переносят базу данных с помощью Azure Database Migration Service.
> - **Шаг 5. Настройка GitHub.** Они настроили локальный репозиторий GitHub для веб-сайтов и кода приложения.
> - **Шаг 6. Развертывание веб-приложений.** Они развертывают веб-приложения из GitHub.

## <a name="step-1-provision-azure-app-service"></a>Шаг 1. предоставление службы приложений Azure

Администраторы Contoso подготавливают два веб-приложения (по одному в каждом регионе) с помощью Службы приложений Azure.

1. Они создают ресурс веб-приложения ( `osticket-eus2` ) в основном регионе ( `East US 2` ) через Azure Marketplace.
2. Они помещают ресурс в рабочую группу ресурсов `ContosoRG` .

    ![Веб-приложение Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. Они создают новый план службы приложений ( `APP-SVP-EUS2` ) в основном регионе, используя стандартный размер.

     ![Приложение Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Они выбирают ОС Linux с стеком среды выполнения PHP 7,0, который является контейнером DOCKER.

    ![Приложение Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Они создают второе веб-приложение ( `osticket-cus` ) и план службы приложений Azure для `Central US` .

    ![Приложение Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Требуется дополнительная помощь?**

- Сведения о [веб-приложениях службы приложений Azure](https://docs.microsoft.com/azure/app-service/overview).
- Сведения о [службе приложений Azure в Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Шаг 2. Настройка диспетчера трафика

Администраторы Contoso настраивают диспетчер трафика для направления входящих веб-запросов в веб-приложения веб-уровня osTicket.

1. Они создают ресурс диспетчера трафика ( `osticket.trafficmanager.net` ) из Azure Marketplace. Они используют маршрутизацию приоритетов, так что `East US 2` это первичный сайт. Они размещают ресурс в своей группе ресурсов инфраструктуры ( `ContosoInfraRG` ). Обратите внимание на то, что диспетчер трафика является глобальным и не привязан к определенному месту.

    ![Диспетчер трафика](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Теперь специалисты компании настраивают диспетчер трафика с конечными точками. Они добавляют веб-приложение в `East US 2` качестве первичного сайта ( `osticket-eus2` ) и веб-приложение в `Central US` качестве вторичного сайта ( `osticket-cus` ).

    ![Добавление конечных точек в диспетчере трафика](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. После добавления конечных точек они могут контролировать их.

    ![Мониторинг конечных точек в диспетчере трафика](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Требуется дополнительная помощь?**

- Подробнее о [диспетчере трафика](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Узнайте больше о [перенаправлении трафика к приоритетной конечной точке](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Шаг 3. Подготовка Базы данных Azure для MySQL

Администраторы Contoso подготавливают экземпляр базы данных MySQL в основном регионе ( `East US 2` ).

1. Специалисты компании создают Базу данных Azure для ресурса MySQL на портале Azure.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Они добавляют имя `contosoosticket` для базы данных Azure. Они добавляют базу данных в рабочую группу ресурсов `ContosoRG` и указывают для нее учетные данные.
3. В локальной среде используется база данных MySQL 5.7, поэтому для обеспечения совместимости выбрана именно эта версия. Для размера они выбирают значение по умолчанию, соответствующее требованиям компании для базы данных.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. В разделе **Варианты резервирования для архивации** специалисты выбирают **Геоизбыточное**. Этот параметр позволяет восстановить базу данных в дополнительном регионе ( `Central US` ) при возникновении сбоя. Данный параметр можно настроить только при подготовке базы данных.

    ![Избыточность](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Специалисты настраивают безопасность подключения. В базе данных > **Безопасность подключения**, они настроили правила брандмауэра, чтобы разрешить базе данных доступ к службам Azure.

6. Они добавляют IP-адрес клиента локальной рабочей станции в начальный и конечный IP-адреса. Это позволяет веб-приложениям получать доступ к базе данных MySQL, а также к ее клиенту, который выполняет перенос.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Шаг 4. Миграция базы данных

Существует несколько способов перемещения базы данных MySQL. Для каждого варианта требуется создать экземпляр базы данных Azure для MySQL для целевого объекта. После создания можно выполнить миграцию, используя два пути:

- Шаг 4A. Azure Database Migration Service
- Шаг 4b. Резервное копирование и восстановление MySQL Workbench

### <a name="step-4a-migrate-the-database-via-azure-database-migration-service"></a>Шаг 4A. Перенос базы данных с помощью Azure Database Migration Service

Администраторы Contoso переходят базу данных с помощью Azure Database Migration Service, выполнив пошаговое [руководство по миграции](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online). Они могут выполнять миграцию в интерактивном, автономном и гибридном режиме (Предварительная версия) с помощью MySQL 5,6 или 5,7.

> [!NOTE]
> MySQL 8,0 поддерживается в базе данных Azure для MySQL, но средство Database Migration Service еще не поддерживает эту версию.

В качестве сводки необходимо выполнить следующие действия.

- Убедитесь, что выполнены все необходимые условия для миграции.
  - Источник сервера базы данных MySQL должен соответствовать версии, поддерживаемой базой данных Azure для MySQL. База данных Azure для MySQL поддерживает выпуск MySQL Community, подсистему хранилища InnoDB и миграцию на исходном и целевом компьютерах с одинаковыми версиями.
  - Включение двоичного входа в систему `my.ini` (Windows) или `my.cnf` (UNIX). Несоблюдение этого действия приведет к сбою `error in binary logging. Variable binlog_row_image has value 'minimal'. Please change it to 'full'. For more information, see https://go.microsoft.com/fwlink/?linkid=873009` мастера миграции.
  - Пользователь должен иметь `ReplicationAdmin` роль.
  - Перенесите схемы базы данных без внешних ключей и триггеров.
- Создайте виртуальную сеть, которая подключается через ExpressRoute или VPN к локальной сети.
- Создайте Azure Database Migration Service с `Premium` номером SKU, подключенным к виртуальной сети.
- Убедитесь, что Azure Database Migration Service может получить доступ к базе данных MySQL через виртуальную сеть. Это гарантирует, что все входящие порты будут разрешены из Azure в MySQL на уровне виртуальной сети, в сети VPN и на компьютере, на котором размещается MySQL.
- Запустите средство Database Migration Service:
  - Создайте проект миграции на основе **SKU Premium**.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-new-project.png)

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-new-project-02.png)

  - Добавьте источник (локальная база данных).

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-source.png)

  - Выберите целевой объект.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-target.png)

  - Выберите базы данных для миграции.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-databases.png)

  - Настройка дополнительных параметров.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-settings.png)

  - Запустите репликацию и устраните все ошибки.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-monitor.png)

  - Выполните окончательный прямую миграцию.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover.png)

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-complete.png)

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-complete-02.png)

  - Возобновите использование внешних ключей и триггеров.

  - Измените приложения для использования новой базы данных.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-apps.png)

### <a name="step-4b-migrate-the-database-mysql-workbench"></a>Шаг 4b. Миграция базы данных (MySQL Workbench)

1. Специалисты компании проверяют [предварительные условия и загружают MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Специалисты компании устанавливают MySQL Workbench для Windows в соответствии с [инструкциями по установке](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Компьютер, на котором они устанавливаются, должен быть доступен для `OSTICKETMYSQL` виртуальной машины и Azure через Интернет.
3. В MySQL Workbench они создают подключение MySQL к `OSTICKETMYSQL` .

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. База данных экспортируется как `osticket` , в локальный автономный файл.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. После локальной архивации базы данных они создают подключения к Базе данных Azure для экземпляра MySQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Теперь специалисты компании могут импортировать (восстановить) базу данных в экземпляре Azure MySQL из автономного файла. `osticket`Для экземпляра создается новая схема ().

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. После восстановления данные можно запрашивать с помощью MySQL Workbench и отображаться в портал Azure.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Наконец, специалистам необходимо обновить сведения о базе данных в веб-приложениях. В экземпляре MySQL специалисты открывают **Строки подключения**.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. В списке строк они находят и щелкают параметры веб-приложения, чтобы скопировать их.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. Специалисты компании открывают Блокнот, вставляют строку в новый файл и изменяют его в соответствии с базой данных osticket, экземпляром MySQL и параметрами учетных данных.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. Специалисты компании могут проверить имя сервера и имя для входа в разделе **Обзор** в экземпляре MySQL на портале Azure.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Шаг 5. Настройка GitHub

Администраторы Contoso создают новый частный репозиторий GitHub и настраивает подключение к базе данных Остиккет в базе данных Azure для MySQL. Затем они загружают веб-приложение в Службу приложений Azure.

1. Специалисты используют общедоступный репозиторий GitHub программного обеспечения osTicket и создают ветвь для учетной записи Contoso GitHub.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. После разветвления они переходят в `include` папку и найдут `ost-config.php` файл.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Специалисты компании изменяют этот файл, когда он открывается в браузере.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. В редакторе они обновляют сведения о базе данных, специально для `DBHOST` и `DBUSER` .

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Затем они применяют изменения.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Для каждого веб-приложения ( `osticket-eus2` и `osticket-cus` ) они изменяют **параметры приложения** в портал Azure.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Они вводят строку подключения с именем `osticket` и копируют строку из Блокнота в **область значений**. Они выбирают **MySQL** в раскрывающемся списке рядом со строкой и сохраняют параметры.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Шаг 6. Настройка веб-приложений

В качестве заключительного этапа процесса миграции администраторы компании Contoso настраивают веб-приложения и веб-сайты osTicket.

1. В основном веб-приложении ( `osticket-eus2` ) они открывают **вариант развертывания** и устанавливают источник в **GitHub**.

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Специалисты компании выбирают варианты развертывания.

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. После настройки параметров конфигурация имеет состояние ожидания на портале Azure.

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. После обновления конфигурации и загрузки веб-приложения Остиккет из GitHub в контейнер DOCKER, в котором запущена служба приложений Azure, сайт будет отображаться как активный.

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Эти шаги повторяются для дополнительного веб-приложения ( `osticket-cus` ).
6. После настройки сайт становится доступным через профиль диспетчера трафика. DNS-имя — это новое расположение приложения Остиккет. [Подробнее](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Компании Contoso необходимо DNS-имя, которое легко запомнить. Они создают запись псевдонима (CNAME) `osticket.contoso.com` , которая указывает на имя диспетчера трафика в DNS на контроллерах домена.

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. Они настраивают `osticket-eus2` `osticket-cus` веб-приложения и, чтобы разрешить пользовательские имена узлов.

    ![Настройка приложения](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Настройка автомасштабирования

Наконец, они настроили автоматическое масштабирование для приложения. Это гарантирует, что, как агенты используют приложение, экземпляры приложения увеличиваются и уменьшаются в соответствии с потребностями бизнеса.

1. В службе приложений `APP-SRV-EUS2` они открывают **единицу масштабирования**.
2. Они настраивают новый параметр автомасштабирования с одним правилом, увеличивающим количество экземпляров на один, когда процент использования ЦП для текущего экземпляра превышает 70 % в течение 10 минут.

    ![Автомасштабирование](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Они настраивают один и тот же параметр в, `APP-SRV-CUS` чтобы обеспечить применение того же поведения при отработки отказа приложения в дополнительный регион. Единственная разница состоит в том, что они ограничивают количество экземпляров по умолчанию до 1, так как это необходимо только для отработки отказа.

   ![Автомасштабирование](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Очистка после миграции

После завершения миграции приложение Остиккет будет переработано для выполнения в веб-приложении службы приложений Azure с непрерывной поставкой с помощью закрытого репозитория GitHub. Приложение выполняется в двух регионах для повышения устойчивости. После миграции на платформу PaaS база данных Остиккет выполняется в базе данных Azure для MySQL.

Для очистки компания Contoso должна выполнить следующие действия:

- Удалить виртуальную машину VMware из перечня в vCenter.
- Удалить локальные виртуальные машины из локальных заданий резервного копирования.
- Обновить внутренние документы и указать в них новые расположения и IP-адреса.
- Проверить все ресурсы, взаимодействующие с локальными виртуальными машинами, и обновить все соответствующие параметры или документы согласно новой конфигурации.
- Перенастройте мониторинг так, чтобы он указывал на `osticket-trafficmanager.net` URL-адрес, чтобы отслеживать, что приложение работает.

## <a name="review-the-deployment"></a>Проверка развертывания

Теперь, когда приложение работает, компания Contoso должна полностью эксплуатацию и защитить свою новую инфраструктуру.

### <a name="security"></a>Безопасность

Группа безопасности Contoso проверила приложение для определения проблем безопасности. Они определили, что взаимодействие между приложением Остиккет и экземпляром базы данных MySQL не настроено для использования SSL. Поэтому им необходимо будет сделать это, чтобы предотвратить взлом трафика, базы данных. [Подробнее](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).

### <a name="backups"></a>Резервные копии

- Веб-приложения Остиккет не содержат данных о состоянии и, таким же, не нуждаются в резервном копировании.
- Ее специалистам нет необходимости настраивать резервное копирование для базы данных. В службе "База данных Azure для MySQL" для сервера автоматически создаются резервные копии. Они решили использовать для базы данных геоизбыточное хранилище, поэтому она отказоустойчива и готова к внедрению в рабочую среду. Резервные копии можно использовать для восстановления сервера до точки во времени. [Подробнее](https://docs.microsoft.com/azure/mysql/concepts-backup).

### <a name="licensing-and-cost-optimization"></a>Лицензирование и оптимизация затрат

- Проблемы с лицензированием развертывания PaaS отсутствуют.
- Компания Contoso будет использовать службу " [Управление затратами Azure" и выставление счетов](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview) , чтобы гарантировать, что они останутся в бюджетах, установленных по ИТ.
