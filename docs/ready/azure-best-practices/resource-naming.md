---
title: Определение соглашения об именовании
description: Сведения о том, как переименовывать ресурсы и активы Azure, а также ознакомиться с примерами имен ресурсов и активов в Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: internal, readiness, fasttrack-edit
ms.openlocfilehash: 5250b4b3876516bbc3239477435cc08adc59494e
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102115753"
---
# <a name="define-your-naming-convention"></a>Определение соглашения об именовании

При действующем соглашении об именовании имена ресурсов составляться из важной информации о каждом ресурсе. Правильно выбранное имя помогает быстро найти тип ресурса, связанную рабочую нагрузку, среду развертывания и регион Azure, где он размещен. Например, ресурс общедоступного IP-адреса для рабочей нагрузки SharePoint, размещенной в регионе "Западная часть США", может быть `pip-sharepoint-prod-westus-001` .

![Компоненты имени ресурса Azure](../../_images/ready/resource-naming.png)

*Схема 1. компоненты имени ресурса Azure.*

## <a name="naming-scope"></a>Область именования

Все типы ресурсов Azure имеют область, определяющую уровень, в котором имена ресурсов должны быть уникальными. Ресурс должен иметь уникальное имя в области действия.

Например, виртуальная сеть имеет область группы ресурсов, что означает, что в данной группе ресурсов может быть только одна сеть с именем `vnet-prod-westus-001`. Другие группы ресурсов могут иметь собственную виртуальную сеть с именем `vnet-prod-westus-001` . Подсети ограничены виртуальными сетями, поэтому каждая подсеть в виртуальной сети должна иметь уникальное имя.

Некоторые имена ресурсов, такие как службы PaaS с общедоступными конечными точками или метки DNS виртуальных машин, имеют глобальные области, поэтому они должны быть уникальными на всей платформе Azure.

![Уровни области для имен ресурсов Azure](../../_images/ready/resource-naming-scope.png)

*Схема 2. уровни области для имен ресурсов Azure.*

Имена ресурсов имеют ограничения по длине. Балансировка контекста, внедренного в имя с его областью и ограничением длины, важна при разработке соглашений об именовании. Дополнительные сведения см. в статье [правила именования и ограничения для ресурсов Azure](/azure/azure-resource-manager/management/resource-name-rules).

### <a name="recommended-naming-components"></a>Рекомендуемые компоненты именования

При создании соглашения об именовании необходимо определить ключевые фрагменты информации, которые необходимо отразить в имени ресурса. К разным типам ресурсов относятся разные сведения. В следующем списке приведены примеры информации, полезной при создании имен ресурсов.

Сократите длину компонентов именования, чтобы избежать превышения ограничений по длине имени ресурса.

| Компонент именования | Описание |
|--|--|--|
| **Тип ресурса** | Сокращение, представляющее тип ресурса или актива Azure. Этот компонент часто используется в качестве префикса или суффикса в имени. Дополнительные сведения см. в статье [Рекомендуемые сокращения для типов ресурсов Azure](./resource-abbreviations.md). Примеры: `rg`, `vm` |
| **Подразделение** | Подразделение высшего уровня компании, которому принадлежит подписка или рабочая нагрузка, к которой принадлежит ресурс. В небольших организациях этот компонент может представлять собой единый корпоративный организационный элемент верхнего уровня. Примеры: `fin` , `mktg` , `product` , `it` , `corp` |
| **Название приложения или службы** | Имя приложения, рабочей нагрузки или службы, частью которой является ресурс. Примеры: `navigator` , `emissions` , `sharepoint` , `hadoop` |
| **Тип подписки** | Краткое описание назначения подписки, содержащей ресурс. Часто разбивается по типу среды развертывания или конкретным рабочим нагрузкам. Примеры: `prod` , `shared` , `client` |
| **&nbsp;Среда развертывания** | Этап жизненного цикла разработки для рабочей нагрузки, поддерживаемой ресурсом. Примеры: `prod` , `dev` , `qa` , `stage` , `test` |
| **Регион** | Регион Azure, в котором развернут ресурс. Примеры: `westus` , `eastus2` , `westeu` , `usva` , `ustx` |

## <a name="example-names-for-common-azure-resource-types"></a>Примеры имен для общих типов ресурсов Azure

В следующем разделе приведены примеры имен распространенных типов ресурсов Azure в облачном развертывании Enterprise.

> [!NOTE]
> В некоторых из этих примеров имен используется схема заполнения, состоящих из трех цифр ( `###` ), например `mktg-prod-001` .
>
> Заполнение повышает удобочитаемость и сортировку ресурсов, когда эти ресурсы управляются в базе данных управления конфигурацией (CMDB), средстве управления ИТ-активами или традиционных средствах учета. Когда развернутый ресурс управляется централизованно как часть более крупного склада или портфеля ИТ-ресурсов, подход к заполнению соответствует интерфейсам, которые используются системами для управления наименованиями инвентаризации.
>
> К сожалению, традиционный подход к заполнению ресурсов может оказаться проблематичным при подходе "инфраструктура как код", который может выполнять итерацию по ресурсам на основе незаполненного числа. Этот подход часто встречается в задачах развертывания или автоматизированного управления конфигурацией. Эти сценарии должны будут построчно выставить заполнение и преобразовывать заполненное число в вещественное число, что снижает время разработки и выполнения скриптов.
>
> Выберите подход, который подходит для вашей организации. Заполнение, показанное здесь, иллюстрирует важность использования единообразного подхода к нумерации запасов, а не того, какой подход является главным. Прежде чем выбрать схему нумерации (с заполнением или без нее), оцените, что будет повлиять на долгосрочные операции: решения по управлению CMDB/Asset или управление инвентаризацией на основе кода. Затем Поддерживайте согласованность с параметром заполнения, который наилучшим образом соответствует рабочим потребностям.

<!-- cspell:ignore cloudapp azurewebsites servicebus -->

<!-- cspell:ignoreRegExp [a-z]+-[a-z]+ -->
<!-- cspell:ignoreRegExp `[a-z]+` -->
<!-- cspell:ignoreRegExp [a-z]+\d+ -->
<!-- cspell:ignoreRegExp _[a-z]+[\\-] -->

## <a name="example-names-general"></a>Примеры имен: общие

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **группа управления;** | Бизнес-единица и/или <br> тип среды | *MG- \<business unit> [- \<environment type> ]* <br><br> <li> `mg-mktg` <li> `mg-hr` <li> `mg-corp-prod` <li> `mg-fin-client` |
| **Подписка** | Соглашение об учетной записи или предприятии | *\<business&nbsp;unit>-\<subscription&nbsp;type>-\<###>* <br><br> <li> `mktg-prod-001` <li> `corp-shared-001` <li> `fin-client-001` |
| **Группа ресурсов** | Подписка | *RG — \<app&nbsp;or&nbsp;service&nbsp;name> Тип подписки <&nbsp;> —\<###>* <br><br> <li> `rg-mktgsharepoint-prod-001` <li> `rg-acctlookupsvc-shared-001` <li> `rg-ad-dir-services-shared-001` |
| **Экземпляр службы управления API** | Global | *apim\<app&nbsp;or&nbsp;service&nbsp;name>* <br><br> `apim-navigator-prod` |
| **Управляемое удостоверение** | Группа ресурсов | *удостоверения\<app&nbsp;or&nbsp;service&nbsp;name>* <br><br> <li> `id-appcn-keda-prod-eastus2-001` |

## <a name="example-names-networking"></a>Примеры имен: Сетевые подключения

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Виртуальная сеть** | Группа ресурсов | *региональной\<subscription&nbsp;type>-\<region>-\<###>* <br><br> <li> `vnet-shared-eastus2-001` <li> `vnet-prod-westus-001` <li> `vnet-client-eastus2-001` |
| **Подсеть** | Виртуальная сеть | *snet-\<subscription>-\<region>-\<###>* <br><br> <li> `snet-shared-eastus2-001` <li> `snet-prod-westus-001` <li> `snet-client-eastus2-001` |
| **Сетевой интерфейс (NIC)** | Группа ресурсов | *Сетевая карта-< # # >-\<vm&nbsp;name>-\<subscription>-\<###>* <br><br> <li> `nic-01-dc1-shared-001` <li> `nic-02-vmhadoop1-prod-001` <li> `nic-02-vmtest1-client-001` |
| **Общедоступный IP-адрес** | Группа ресурсов | *показывает\<vm&nbsp;name&nbsp;or&nbsp;app&nbsp;name>-\<environment>-\<region>-\<###>* <br><br> <li> `pip-dc1-shared-eastus2-001` <li> `pip-hadoop-prod-westus-001` |
| **Подсистема балансировки нагрузки** | Группа ресурсов | *LB\<app&nbsp;name&nbsp;or&nbsp;role>-<environment>-\<###>* <br><br> <li> `lb-navigator-prod-001` <li> `lb-sharepoint-dev-001` |
| **Группа безопасности сети (NSG)** | Подсеть или сетевая карта | *NSG\<policy&nbsp;name&nbsp;or&nbsp;app&nbsp;name>-\<###>* <br><br> <li> `nsg-weballow-001` <li> `nsg-rdpallow-001` <li> `nsg-sqlallow-001` <li> `nsg-dnsblocked-001` |
| **Шлюз локальной сети** | Виртуальный шлюз | *лгв —\<subscription&nbsp;type>-\<region>-\<###>* <br><br> <li> `lgw-shared-eastus2-001` <li> `lgw-prod-westus-001` <li> `lgw-client-eastus2-001` |
| **Шлюз виртуальной сети** | Виртуальная сеть | *ВГВ —\<subscription&nbsp;type>-\<region>-\<###>* <br><br> <li> `vgw-shared-eastus2-001` <li> `vgw-prod-westus-001` <li> `vgw-client-eastus2-001` |
| **Подключение "сеть — сеть"** | Группа ресурсов | *CN- \<local&nbsp;gateway&nbsp;name> -to-\<virtual&nbsp;gateway&nbsp;name>* <br><br> <li> `cn-lgw-shared-eastus2-001-to-vgw-shared-eastus2-001` <li> `cn-lgw-shared-eastus2-001-to-vgw-shared-westus-001` |
| **VPN-подключение** | Группа ресурсов | *CN- \<subscription1> - \<region1> -to-\<subscription2>-\<region2>-* <br><br> <li> `cn-shared-eastus2-to-shared-westus` <li> `cn-prod-eastus2-to-prod-westus` |
| **Таблица маршрутов** | Группа ресурсов | *направлены\<route&nbsp;table&nbsp;name>* <br><br> <li> `route-navigator` <li> `route-sharepoint` |
| **Метка DNS** | Global | *\<DNS&nbsp;A&nbsp;record&nbsp;for&nbsp;VM>.\<region>. cloudapp.azure.com* <br><br> <li> `dc1.westus.cloudapp.azure.com` <li> `web1.eastus2.cloudapp.azure.com` |

## <a name="example-names-compute-and-web"></a>Примеры имен: COMPUTE и Web

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Виртуальная машина** | Группа ресурсов | *машину\<policy name or app name>\<###>* <br><br> <li> `vmnavigator001` <li> `vmsharepoint001` <li> `vmsqlnode001` <li> `vmhadoop001` |
| **Учетная запись хранения виртуальных машин** | Global | *stvm\<performance type>\<app name or prod name>\<region>\<###>* <br><br> <li> `stvmstcoreeastus2001` <li> `stvmpmcoreeastus2001` <li> `stvmstplmeastus2001` <li> `stvmsthadoopeastus2001` |
| **Веб-приложение** | Global | *App- \<app name> - \<environment> - \<###> . azurewebsites.NET* <br><br> <li> `app-navigator-prod-001.azurewebsites.net` <li> `app-accountlookup-dev-001.azurewebsites.net` |
| **Приложение-функция** | Global | *Func- \<app name> - \<environment> - \<###> . azurewebsites.NET* <br><br> <li> `func-navigator-prod-001.azurewebsites.net` <li> `func-accountlookup-dev-001.azurewebsites.net` |
| **облачная служба** | Global | *возможно \<app name> - \<environment> - \<###> , cloudapp.NET}* <br><br> <li> `cld-navigator-prod-001.azurewebsites.net` <li> `cld-accountlookup-dev-001.azurewebsites.net` |
| **Пространство имен концентраторов уведомлений** | Global | *нтфнс —\<app name>-\<environment>* <br><br> <li> `ntfns-navigator-prod` <li> `ntfns-emissions-dev` |
| **Концентратор уведомлений** | Пространство имен концентраторов уведомлений | *NTF\<app name>-\<environment>* <br><br> <li> `ntf-navigator-prod` <li> `ntf-emissions-dev` |

## <a name="example-names-databases"></a>Примеры имен: базы данных

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **сервер Базы данных SQL Azure;** | Global | *SQL\<app name>-\<environment>* <br><br> <li> `sql-navigator-prod` <li> `sql-emissions-dev` |
| **База данных SQL Azure** | База данных SQL Azure | *sqldb-\<database name>-\<environment>* <br><br> <li> `sqldb-users-prod` <li> `sqldb-users-dev` |
| **База данных Azure Cosmos DB** | Global | *Cosmos\<app name>-\<environment>* <br><br> <li> `cosmos-navigator-prod` <li> `cosmos-emissions-dev` |
| **Кэш Azure для экземпляра Redis** | Global | *Redis\<app name>-\<environment>* <br><br> <li> `redis-navigator-prod` <li> `redis-emissions-dev` |
| **База данных MySQL** | Global | *MySQL\<app name>-\<environment>* <br><br> <li> `mysql-navigator-prod` <li> `mysql-emissions-dev` |
| **База данных PostgreSQL** | Global | *psql\<app name>-\<environment>* <br><br> <li> `psql-navigator-prod` <li> `psql-emissions-dev` |
| **Хранилище данных SQL Azure** | Global | *sqldw-\<app name>-\<environment>* <br><br> <li> `sqldw-navigator-prod` <li> `sqldw-emissions-dev` |
| **SQL Server Stretch Database** | База данных SQL Azure | *sqlstrdb-\<app name>-\<environment>* <br><br> <li> `sqlstrdb-navigator-prod` <li> `sqlstrdb-emissions-dev` |

## <a name="example-names-storage"></a>Примеры имен: хранилище

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Учетная запись хранения (общее использование)** | Global | *st\<storage name>\<###>* <br><br> <li> `stnavigatordata001` <li> `stemissionsoutput001` |
| **Учетная запись хранения (журналы диагностики)** | Global | *стдиаг\<first 2 letters of subscription name and number>\<region>\<###>* <br><br> <li> `stdiagsh001eastus2001` <li> `stdiagsh001westus001` |
| **StorSimple Azure** | Global | *ssimp\<app name>-\<environment>* <br><br> <li> `ssimpnavigatorprod` <li> `ssimpemissionsdev` |
| **Реестр контейнеров Azure** | Global | *ACR\<app name>\<environment>\<###>* <br><br> <li> `acrnavigatorprod001` |

## <a name="example-names-ai-and-machine-learning"></a>Примеры имен: AI и машинное обучение

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Когнитивный поиск Azure** | Global | *srch-\<app name>-\<environment>* <br><br> <li> `srch-navigator-prod` <li> `srch-emissions-dev` |
| **Azure Cognitive Services** | Группа ресурсов | *шестеренки\<app name>-\<environment>* <br><br> <li> `cog-navigator-prod` <li> `cog-emissions-dev` |
| **Рабочая область машинного обучения Azure** | Группа ресурсов | *МЛВ —\<app name>-\<environment>* <br><br> <li> `mlw-navigator-prod` <li> `mlw-emissions-dev` |

## <a name="example-names-analytics-and-iot"></a>Примеры имен: аналитика и IoT

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Фабрика данных Azure**. | Global | *файлах\<app name>\<environment>* <br><br> <li> `adf-navigator-prod` <li> `adf-emissions-dev` |
| **Azure Stream Analytics** | Группа ресурсов | *ASA\<app name>-\<environment>* <br><br> <li> `asa-navigator-prod` <li> `asa-emissions-dev` |
| **Учетная запись Data Lake Analytics** | Global | *dla\<app name>\<environment>* <br><br> <li> `dlanavigatorprod` <li> `dlanavigatorprod` |
| **Учетная запись Data Lake Storage** | Global | *распространения\<app name>\<environment>* <br><br> <li> `dlsnavigatorprod` <li> `dlsemissionsdev` |
| **Концентратор событий** | Global | *evh-\<app name>-\<environment>* <br><br> <li> `evh-navigator-prod` <li> `evh-emissions-dev` |
| **Кластер HDInsight — HBase** | Global | *HBase\<app name>-\<environment>* <br><br> <li> `hbase-navigator-prod` <li> `hbase-emissions-dev` |
| **HDInsight — кластер Hadoop** | Global | *Hadoop\<app name>-\<environment>* <br><br> <li> `hadoop-navigator-prod` <li> `hadoop-emissions-dev` |
| **HDInsight — кластер Spark** | Global | *Spark\<app name>-\<environment>* <br><br> <li> `spark-navigator-prod` <li> `spark-emissions-dev` |
| **Центр Интернета вещей** | Global | *IOT\<app name>-\<environment>* <br><br> <li> `iot-navigator-prod` <li> `iot-emissions-dev` |
| **Что такое Power BI Embedded в Azure?** | Global | *PBI\<app name>-\<environment>* <br><br> <li> `pbi-navigator-prod` <li> `pbi-emissions-dev` |

## <a name="example-names-integration"></a>Примеры имен: интеграция

| Тип ресурса | Область | Формат и примеры|
|--|--|--|
| **Служебная шина** | Global | *SB- \<app name> - \<environment> . servicebus.Windows.NET* <br><br> <li> `sb-navigator-prod` <li> `sb-emissions-dev` |
| **Очередь служебной шины** | Служебная шина | *sbq-\<query descriptor>* <br><br> <li> `sbq-messagequery` |
| **Раздел служебной шины** | Служебная шина | *SBT\<query descriptor>* <br><br> <li> `sbt-messagequery` |

## <a name="next-steps"></a>Дальнейшие действия

Ознакомьтесь с рекомендуемыми сокращениями, которые следует использовать для различных типов ресурсов Azure при именовании ресурсов и активов.

> [!div class="nextstepaction"]
> [Рекомендуемые сокращения для типов ресурсов Azure](./resource-abbreviations.md)
