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
ms.openlocfilehash: 40c0754c9f5085a0735b74b893424428a63fcc3c
ms.sourcegitcommit: b6f2b4f8db6c3b1157299ece1f044cff56895919
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97024404"
---
# <a name="define-your-naming-convention"></a>Определение соглашения об именовании

При действующем соглашении об именовании имена ресурсов составляться из важной информации о каждом ресурсе. Правильно выбранное имя помогает быстро найти тип ресурса, связанную рабочую нагрузку, среду развертывания и регион Azure, где он размещен. Например, ресурс общедоступного IP-адреса для рабочей нагрузки SharePoint, размещенной в регионе "Западная часть США", может быть `pip-sharepoint-prod-westus-001` .

![Компоненты имени ресурса Azure](../../_images/ready/resource-naming.png)

_Схема 1. компоненты имени ресурса Azure._

## <a name="naming-scope"></a>Область именования

Все типы ресурсов Azure имеют область, определяющую уровень, в котором имена ресурсов должны быть уникальными. Ресурс должен иметь уникальное имя в области действия.

Например, виртуальная сеть имеет область группы ресурсов, что означает, что в данной группе ресурсов может быть только одна сеть с именем `vnet-prod-westus-001`. Другие группы ресурсов могут иметь собственную виртуальную сеть с именем `vnet-prod-westus-001` . Подсети ограничены виртуальными сетями, поэтому каждая подсеть в виртуальной сети должна иметь уникальное имя.

Некоторые имена ресурсов, такие как службы PaaS с общедоступными конечными точками или метки DNS виртуальных машин, имеют глобальные области, поэтому они должны быть уникальными на всей платформе Azure.

![Уровни области для имен ресурсов Azure](../../_images/ready/resource-naming-scope.png)

_Схема 2. уровни области для имен ресурсов Azure._

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
| **группа управления;** | Бизнес-единица и/или <br> тип среды | _MG- \<business unit> [- \<environment type> ]_ <br><br> <li> `mg-mktg` <li> `mg-hr` <li> `mg-corp-prod` <li> `mg-fin-client` |
| **Подписка** | Соглашение об учетной записи или предприятии | _\<business&nbsp;unit>-\<subscription&nbsp;type>-\<###>_ <br><br> <li> `mktg-prod-001` <li> `corp-shared-001` <li> `fin-client-001` |
| **Группа ресурсов** | Подписка | _RG — \<app&nbsp;or&nbsp;service&nbsp;name> Тип подписки <&nbsp;> —\<###>_ <br><br> <li> `rg-mktgsharepoint-prod-001` <li> `rg-acctlookupsvc-shared-001` <li> `rg-ad-dir-services-shared-001` |
| **Экземпляр службы управления API** | Глобальный | _apim\<app&nbsp;or&nbsp;service&nbsp;name>_ <br><br> `apim-navigator-prod` |
| **Управляемое удостоверение** | Группа ресурсов | _удостоверения\<app&nbsp;or&nbsp;service&nbsp;name>_ <br><br> <li> `id-appcn-keda-prod-eastus2-001` |

## <a name="example-names-networking"></a>Примеры имен: Сетевые подключения

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Виртуальная сеть** | Группа ресурсов | _региональной\<subscription&nbsp;type>-\<region>-\<###>_ <br><br> <li> `vnet-shared-eastus2-001` <li> `vnet-prod-westus-001` <li> `vnet-client-eastus2-001` |
| **Подсеть** | Виртуальная сеть | _snet-\<subscription>-\<region>-\<###>_ <br><br> <li> `snet-shared-eastus2-001` <li> `snet-prod-westus-001` <li> `snet-client-eastus2-001` |
| **Сетевой интерфейс (NIC)** | Группа ресурсов | _Сетевая карта-< # # >-\<vm&nbsp;name>-\<subscription>-\<###>_ <br><br> <li> `nic-01-dc1-shared-001` <li> `nic-02-vmhadoop1-prod-001` <li> `nic-02-vmtest1-client-001` |
| **Общедоступный IP-адрес** | Группа ресурсов | _показывает\<vm&nbsp;name&nbsp;or&nbsp;app&nbsp;name>-\<environment>-\<region>-\<###>_ <br><br> <li> `pip-dc1-shared-eastus2-001` <li> `pip-hadoop-prod-westus-001` |
| **Подсистема балансировки нагрузки** | Группа ресурсов | _LB\<app&nbsp;name&nbsp;or&nbsp;role>-<environment>-\<###>_ <br><br> <li> `lb-navigator-prod-001` <li> `lb-sharepoint-dev-001` |
| **Группа безопасности сети (NSG)** | Подсеть или сетевая карта | _NSG\<policy&nbsp;name&nbsp;or&nbsp;app&nbsp;name>-\<###>_ <br><br> <li> `nsg-weballow-001` <li> `nsg-rdpallow-001` <li> `nsg-sqlallow-001` <li> `nsg-dnsblocked-001` |
| **Шлюз локальной сети** | Виртуальный шлюз | _лгв —\<subscription&nbsp;type>-\<region>-\<###>_ <br><br> <li> `lgw-shared-eastus2-001` <li> `lgw-prod-westus-001` <li> `lgw-client-eastus2-001` |
| **Шлюз виртуальной сети** | Виртуальная сеть | _ВГВ —\<subscription&nbsp;type>-\<region>-\<###>_ <br><br> <li> `vgw-shared-eastus2-001` <li> `vgw-prod-westus-001` <li> `vgw-client-eastus2-001` |
| **Шлюз виртуальной сети** | Виртуальная сеть | _ВГВ —\<subscription&nbsp;type>-\<region>-\<###>_ <br><br> <li> `vgw-shared-eastus2-001` <li> `vgw-prod-westus-001` <li> `vgw-client-eastus2-001` |
| **Подключение "сеть — сеть"** | Группа ресурсов | _CN- \<local&nbsp;gateway&nbsp;name> -to-\<virtual&nbsp;gateway&nbsp;name>_ <br><br> <li> `cn-lgw-shared-eastus2-001-to-vgw-shared-eastus2-001` <li> `cn-lgw-shared-eastus2-001-to-vgw-shared-westus-001` |
| **VPN-подключение** | Группа ресурсов | _CN- \<subscription1> - \<region1> -to-\<subscription2>-\<region2>-_ <br><br> <li> `cn-shared-eastus2-to-shared-westus` <li> `cn-prod-eastus2-to-prod-westus` |
| **Таблица маршрутов** | Группа ресурсов | _направлены\<route&nbsp;table&nbsp;name>_ <br><br> <li> `route-navigator` <li> `route-sharepoint` |
| **Метка DNS** | Глобальный | _\<DNS&nbsp;A&nbsp;record&nbsp;for&nbsp;VM>.\<region>. cloudapp.azure.com_ <br><br> <li> `dc1.westus.cloudapp.azure.com` <li> `web1.eastus2.cloudapp.azure.com` |

## <a name="example-names-compute-and-web"></a>Примеры имен: COMPUTE и Web

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Виртуальная машина** | Группа ресурсов | _машину\<policy name or app name>\<###>_ <br><br> <li> `vmnavigator001` <li> `vmsharepoint001` <li> `vmsqlnode001` <li> `vmhadoop001` |
| **Учетная запись хранения виртуальных машин** | Глобальный | _stvm\<performance type>\<app name or prod name>\<region>\<###>_ <br><br> <li> `stvmstcoreeastus2001` <li> `stvmpmcoreeastus2001` <li> `stvmstplmeastus2001` <li> `stvmsthadoopeastus2001` |
| **Веб-приложение** | Глобальный | _App- \<app name> - \<environment> - \<###> . azurewebsites.NET_ <br><br> <li> `app-navigator-prod-001.azurewebsites.net` <li> `app-accountlookup-dev-001.azurewebsites.net` |
| **Приложение-функция** | Глобальный | _Func- \<app name> - \<environment> - \<###> . azurewebsites.NET_ <br><br> <li> `func-navigator-prod-001.azurewebsites.net` <li> `func-accountlookup-dev-001.azurewebsites.net` |
| **облачная служба** | Глобальный | _возможно \<app name> - \<environment> - \<###> , cloudapp.NET}_ <br><br> <li> `cld-navigator-prod-001.azurewebsites.net` <li> `cld-accountlookup-dev-001.azurewebsites.net` |
| **Пространство имен концентраторов уведомлений** | Глобальный | _нтфнс —\<app name>-\<environment>_ <br><br> <li> `ntfns-navigator-prod` <li> `ntfns-emissions-dev` |
| **Концентратор уведомлений** | Пространство имен концентраторов уведомлений | _NTF\<app name>-\<environment>_ <br><br> <li> `ntf-navigator-prod` <li> `ntf-emissions-dev` |

## <a name="example-names-databases"></a>Примеры имен: базы данных

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **сервер Базы данных SQL Azure;** | Глобальный | _SQL\<app name>-\<environment>_ <br><br> <li> `sql-navigator-prod` <li> `sql-emissions-dev` |
| **База данных SQL Azure** | База данных SQL Azure | _sqldb-\<database name>-\<environment>_ <br><br> <li> `sqldb-users-prod` <li> `sqldb-users-dev` |
| **База данных Azure Cosmos DB** | Глобальный | _Cosmos\<app name>-\<environment>_ <br><br> <li> `cosmos-navigator-prod` <li> `cosmos-emissions-dev` |
| **Кэш Azure для экземпляра Redis** | Глобальный | _Redis\<app name>-\<environment>_ <br><br> <li> `redis-navigator-prod` <li> `redis-emissions-dev` |
| **База данных MySQL** | Глобальный | _MySQL\<app name>-\<environment>_ <br><br> <li> `mysql-navigator-prod` <li> `mysql-emissions-dev` |
| **База данных PostgreSQL** | Глобальный | _psql\<app name>-\<environment>_ <br><br> <li> `psql-navigator-prod` <li> `psql-emissions-dev` |
| **Хранилище данных SQL Azure** | Глобальный | _sqldw-\<app name>-\<environment>_ <br><br> <li> `sqldw-navigator-prod` <li> `sqldw-emissions-dev` |
| **SQL Server Stretch Database** | База данных SQL Azure | _sqlstrdb-\<app name>-\<environment>_ <br><br> <li> `sqlstrdb-navigator-prod` <li> `sqlstrdb-emissions-dev` |

## <a name="example-names-storage"></a>Примеры имен: хранилище

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Учетная запись хранения (общее использование)** | Глобальный | _день\<storage name>\<###>_ <br><br> <li> `stnavigatordata001` <li> `stemissionsoutput001` |
| **Учетная запись хранения (журналы диагностики)** | Глобальный | _стдиаг\<first 2 letters of subscription name and number>\<region>\<###>_ <br><br> <li> `stdiagsh001eastus2001` <li> `stdiagsh001westus001` |
| **StorSimple Azure** | Глобальный | _ssimp\<app name>-\<environment>_ <br><br> <li> `ssimpnavigatorprod` <li> `ssimpemissionsdev` |
| **Реестр контейнеров Azure** | Глобальный | _ACR\<app name>\<environment>\<###>_ <br><br> <li> `acrnavigatorprod001` |

## <a name="example-names-ai-and-machine-learning"></a>Примеры имен: AI и машинное обучение

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Когнитивный поиск Azure** | Глобальный | _srch-\<app name>-\<environment>_ <br><br> <li> `srch-navigator-prod` <li> `srch-emissions-dev` |
| **Azure Cognitive Services** | Группа ресурсов | _шестеренки\<app name>-\<environment>_ <br><br> <li> `cog-navigator-prod` <li> `cog-emissions-dev` |
| **Рабочая область машинного обучения Azure** | Группа ресурсов | _МЛВ —\<app name>-\<environment>_ <br><br> <li> `mlw-navigator-prod` <li> `mlw-emissions-dev` |

## <a name="example-names-analytics-and-iot"></a>Примеры имен: аналитика и IoT

| Тип ресурса | Область | Формат и примеры |
|--|--|--|
| **Фабрика данных Azure**. | Глобальный | _файлах\<app name>\<environment>_ <br><br> <li> `adf-navigator-prod` <li> `adf-emissions-dev` |
| **Azure Stream Analytics** | Группа ресурсов | _ASA\<app name>-\<environment>_ <br><br> <li> `asa-navigator-prod` <li> `asa-emissions-dev` |
| **Учетная запись Data Lake Analytics** | Глобальный | _dla\<app name>\<environment>_ <br><br> <li> `dlanavigatorprod` <li> `dlanavigatorprod` |
| **Учетная запись Data Lake Storage** | Глобальный | _распространения\<app name>\<environment>_ <br><br> <li> `dlsnavigatorprod` <li> `dlsemissionsdev` |
| **Концентратор событий** | Глобальный | _evh-\<app name>-\<environment>_ <br><br> <li> `evh-navigator-prod` <li> `evh-emissions-dev` |
| **Кластер HDInsight — HBase** | Глобальный | _HBase\<app name>-\<environment>_ <br><br> <li> `hbase-navigator-prod` <li> `hbase-emissions-dev` |
| **HDInsight — кластер Hadoop** | Глобальный | _Hadoop\<app name>-\<environment>_ <br><br> <li> `hadoop-navigator-prod` <li> `hadoop-emissions-dev` |
| **HDInsight — кластер Spark** | Глобальный | _Spark\<app name>-\<environment>_ <br><br> <li> `spark-navigator-prod` <li> `spark-emissions-dev` |
| **Центр Интернета вещей** | Глобальный | _IOT\<app name>-\<environment>_ <br><br> <li> `iot-navigator-prod` <li> `iot-emissions-dev` |
| **Что такое Power BI Embedded в Azure?** | Глобальный | _PBI\<app name>-\<environment>_ <br><br> <li> `pbi-navigator-prod` <li> `pbi-emissions-dev` |

## <a name="example-names-integration"></a>Примеры имен: интеграция

| Тип ресурса | Область | Формат и примеры|
|--|--|--|
| **Служебная шина** | Глобальный | _SB- \<app name> - \<environment> . servicebus.Windows.NET_ <br><br> <li> `sb-navigator-prod` <li> `sb-emissions-dev` |
| **Очередь служебной шины** | Cлужебная шина | _sbq-\<query descriptor>_ <br><br> <li> `sbq-messagequery` |
| **Раздел служебной шины** | Cлужебная шина | _SBT\<query descriptor>_ <br><br> <li> `sbt-messagequery` |

## <a name="next-steps"></a>Дальнейшие действия

Ознакомьтесь с рекомендуемыми сокращениями, которые следует использовать для различных типов ресурсов Azure при именовании ресурсов и активов.

> [!div class="nextstepaction"]
> [Рекомендуемые сокращения для типов ресурсов Azure](./resource-abbreviations.md)
