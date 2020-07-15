---
title: Миграция баз данных MariaDB в Azure
description: Узнайте, как компания Contoso перенеса свои локальные базы данных MariaDB в Azure.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 84bd6cbef97428aacb81d4d6136439a1c9c1f3f6
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2020
ms.locfileid: "86198812"
---
<!-- TODO: Verify GraphDBMS term -->
<!-- cSpell:ignore ColumnStore GraphDBMS mysqldump Navicat phpMyAdmin -->

# <a name="migrate-mariadb-databases-to-azure"></a>Миграция баз данных MariaDB в Azure

В этой статье показано, как вымышленная компания Contoso планирует и перенеса свою локальную платформу базы данных MariaDB с открытым исходным кодом в Azure.

Contoso использует MariaDB через MySQL из-за множества ядер хранилища, производительности кэша и индекса, поддержки открытого кода с функциями и расширениями, а также поддержкой аналитики ColumnStore. Их цель в переносе — продолжить использовать MariaDB, но не беспокоиться об управлении средой, необходимой для ее поддержки.

## <a name="business-drivers"></a>Бизнес-факторы

Совместными усилиями ИТ-руководство и деловые партнеры определили указанные ниже цели этой миграции.

- **Повышение доступности.** Компания Contoso получила проблемы с доступностью к локальной среде MariaDB, поэтому для бизнеса требуются более надежные приложения, использующие это хранилище данных.

- **Повышение эффективности.** Компании Contoso необходимо удалить ненужные процедуры и упростить процессы для разработчиков и пользователей. Бизнесу требуется, чтобы он был быстрым и не тратить время или деньги, обеспечивая более быстрое выполнение требований клиентов.

- **Повышение гибкости.**  ИТ-отдел компании Contoso должен проявлять большую гибкость в отношении потребностей бизнеса. Он должен иметь возможность реагировать быстрее, чем изменения в Marketplace, чтобы обеспечить успешную работу в глобальной экономике. ИТ-не должныся как или стать заблокированным.

- **Измените.** По мере успешного роста бизнеса ИТ-отдел компании Contoso должен предоставлять системы, способные расти в том же темпе.

## <a name="migration-goals"></a>Цели миграции

Группа Contoso Cloud заблокировала цели для этой миграции и будет использовать их для определения лучшего метода переноса.

| Требования | Сведения |
| --- | --- |
| **Доступность** | В настоящее время внутренний персонал имеет Нежесткое время в среде размещения для экземпляра MariaDB. Компания Contoso хочет получить доступ к 99,99% уровня базы данных. |
| **Масштабируемость** | На локальном узле базы данных недостаточно ресурсов, компании Contoso требуется способ масштабировать свои экземпляры за пределами их текущих ограничений или масштабировать их, если бизнес-среда изменяется для экономии затрат. |
| **Производительность** | Отдел кадров Contoso имеет несколько отчетов, которые они запускают ежедневно, еженедельно и ежемесячно. При выполнении этих отчетов они заметят значительные проблемы с производительностью приложения, ориентированного на сотрудников. Они должны запускать отчеты, не влияя на производительность приложения. |
| **Безопасность** | Компания Contoso должна быть в курсе, что база данных будет доступна только внутренним приложениям, а не видима или недоступна через Интернет. |
| **Мониторинг** | В настоящее время компания Contoso использует средства для мониторинга метрик MariaDB и предоставления уведомлений при возникновении проблем с ЦП, памятью или хранилищем. Они бы хотели иметь такую же возможность в Azure. |
| **Непрерывность бизнес-процессов** | Хранилище данных HR является важной частью ежедневных операций Contoso и, если оно было повреждено или необходимо восстановить, они хотели бы сократить время простоя. |
| **Azure** | Компания Contoso хочет переместить приложение в Azure, не запуская его на виртуальных машинах. Требования Contoso к использованию служб Azure PaaS для уровня данных. |

## <a name="solution-design"></a>Архитектура решения

После фиксации целей и требований компания Contoso проектирует и просматривает решение по развертыванию и определяет процесс миграции, включая средства и службы, которые они будут использовать для миграции.

### <a name="current-application"></a>Текущее приложение

В MariaDB размещаются данные о сотрудниках, используемые для всех аспектов отдела кадров компании. В качестве внешнего интерфейса для обработки запросов сотрудников отдела кадров используется приложение [на основе лампы](https://wikipedia.org/wiki/LAMP_(software_bundle)) . Компания Contoso имеет 100 000 сотрудников по всему миру, поэтому время работы очень важно для баз данных.

### <a name="proposed-solution"></a>Предлагаемое решение

- Оцените среды для совместимости с миграцией.
- Используйте общие средства с открытым кодом для переноса баз данных в экземпляр базы данных Azure для MariaDB.
- Измените все приложения и процессы, чтобы они использовали новый экземпляр базы данных Azure для MariaDB.

### <a name="database-considerations"></a>Рекомендации по базе данных

В рамках процесса разработки решения компания Contoso проверила возможности в Azure для размещения своих баз данных MariaDB. Следующие рекомендации помогли вам решить, как использовать Azure.

- Как и в случае с Azure SQL, база данных Azure для MariaDB позволяет создавать [правила брандмауэра](https://docs.microsoft.com/azure/mariadb/concepts-firewall-rules).
- Базу данных Azure для MariaDB можно использовать с [виртуальной сетью Azure](https://docs.microsoft.com/azure/mariadb/concepts-data-access-security-vnet) , чтобы запретить доступ к экземпляру
- База данных Azure для MariaDB имеет необходимые сертификаты соответствия требованиям и конфиденциальности, которые должны соответствовать компании Contoso для аудиторов.
- Производительность отчетов и обработки приложений будет улучшена с помощью считывания реплик.
- Возможность предоставлять доступ к службе только внутреннему сетевому трафику (без общего доступа) с помощью [частной ссылки](https://docs.microsoft.com/azure/mariadb/concepts-data-access-security-private-link).
- Они решили не переходить в базу данных Azure для MySQL, так как они могут использовать модель базы данных MariaDB ColumnStore и Графдбмс в будущем.
- [Пропускная способность и задержка](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) от приложения к базе данных достаточно достаточны в зависимости от выбранного шлюза (ExpressRoute или VPN-подключение типа "сеть — сеть").

### <a name="solution-review"></a>Проверка решения

Contoso оценивает предлагаемый дизайн, составляя список плюсов и минусов.

| Рассматриваемый вопрос | Сведения |
| --- | --- |
| **Преимущества** | Служба "база данных Azure для MariaDB" предлагает соглашение об уровне обслуживания с финансовыми гарантиями на 99,99% для обеспечения [высокого уровня доступности](https://docs.microsoft.com/azure/mariadb/concepts-high-availability). <br><br> Azure предлагает возможность увеличения или уменьшения масштаба в течение пиковых нагрузок в каждом квартале. Компания Contoso может сэкономить еще больше покупок [зарезервированной емкости](https://docs.microsoft.com/azure/mariadb/concept-reserved-pricing). <br><br> Azure предоставляет возможности восстановления на момент времени и геовосстановление для базы данных Azure для MariaDB. <br><br> |
| **Недостатки** | Компания Contoso ограничена версиями выпуска MariaDB, которые поддерживаются в Azure, в настоящее время 10,2 и 10,3. <br><br> В базе данных Azure для MariaDB есть некоторые [ограничения](https://docs.microsoft.com/azure/mariadb/concepts-limits) , например масштабирование хранилища. |

## <a name="proposed-architecture"></a>Предлагаемая архитектура

![Архитектура сценария ](./media/contoso-migration-mariadb-to-azure/architecture.png)
 _рис. 1. Архитектура сценария._

### <a name="migration-process"></a>Процесс миграции

#### <a name="preparation"></a>Подготовка

Прежде чем можно будет перенести базы данных MariaDB, необходимо убедиться, что эти экземпляры соответствуют всем предварительным требованиям Azure для успешной миграции.

Поддерживаемые версии:

- MariaDB использует схему именования x. y. z. X — основной номер версии, y — дополнительный номер версии, а z — версия исправления.
- Сейчас Azure поддерживает 10.2.25 и 10.3.16.
- Azure автоматически управляет обновлениями для обновлений исправлений. Например, 10.2.21 в 10.2.23. Дополнительные и основные обновления версий не поддерживаются. Например, обновление с версии MariaDB 10.2 до MariaDB 10.3 не поддерживается. Если вы хотите выполнить обновление с 10,2 до 10,3, сделайте дамп базы данных и восстановите его на сервере, созданном с использованием целевой версии подсистемы.

Сеть:

Contoso потребуется настроить подключение шлюза виртуальной сети из локальной среды к виртуальной сети, где находится их база данных MariaDB. Это позволит локальному приложению получать доступ к базе данных через шлюз при обновлении строк подключения.

  ![Процесс миграции ](./media/contoso-migration-mariadb-to-azure/migration-process.png) _рис. 2. процесс миграции._

#### <a name="migration"></a>Миграция

Так как MariaDB очень похожа на MySQL, они могут использовать одни и те же общие служебные программы и средства, такие как MySQL Workbench, mysqldump, Toad или Navicat, для подключения и переноса данных в базу данных Azure для MariaDB.

Для переноса баз данных компания Contoso использовала следующие шаги.

- Определите локальную версию MariaDB, выполнив следующие команды и просматривая выходные данные. В большинстве случаев ваша версия не имеет большого значения в плане схемы и дампа данных. Если вы используете функции на уровне приложения, следует убедиться, что эти приложения совместимы с целевой версией в Azure.

  ```cmd
    mysql -h localhost -u root -P
  ```

  ![Процесс миграции ](./media/contoso-migration-mariadb-to-azure/mariadb_version.png)
   _рис. 4. Определение локальной версии MariaDB._

- Создайте новый экземпляр MariaDB в Azure:

  - Откройте [портал Azure](https://portal.azure.com).
  - Выберите **Добавить ресурс**.
  - Найдите `MariaDB`.

    ![Процесс миграции ](./media/contoso-migration-mariadb-to-azure/azure-mariadb-create.png)
     _рис. 4. новый экземпляр MariaDB в Azure._

  - Нажмите кнопку **Создать**.
  - Выберите подписку и группу ресурсов.
  - Выберите имя и расположение сервера.
  - Выберите целевую версию (10,2 или 10,3).
  - Выберите ресурсы для вычислений и хранилища.
  - Введите имя пользователя и пароль администратора.
  - Выберите **Просмотр и создание**.

    ![Процесс миграции ](./media/contoso-migration-mariadb-to-azure/azure_mariadb_create.png)
     _рис. 5. Проверка и создание._

  - Нажмите кнопку **Создать**.
  - Запишите имя узла, имя пользователя и пароль сервера.
  - Выберите **Безопасность подключения**.
  - Выберите **Добавить IP-адрес клиента** (IP-адрес, с которого будет восстанавливаться база данных).
  - Щелкните **Сохранить**.

- Выполните следующие команды, чтобы экспортировать базу данных с именем `Employees` . Повторите эти действия для каждой базы данных:

    ```cmd
    mysqldump -h localhost -u root -p -–skip-triggers -–single-transaction –-extended-insert -–order-by-primary -–disable-keys Employees > Employees.sql
    ```

- восстановить базу данных. Замените конечной точкой для экземпляра базы данных Azure для MariaDB и имени пользователя.

  ```cmd
  mysql -h {name}.mariadb.database.azure.com -u user@{name} -p –ssl
  create database employees;
  use database employees;
  source employees.sql;
  ```

- С помощью phpMyAdmin или аналогичного средства (MySQL Workbench, Toad и Navicat) Проверьте восстановление, установив счетчики записей в каждой таблице.
- Обновите все строки подключения приложения, чтобы они указывали на перенесенную базу данных.
- Протестируйте все приложения для правильной работы

## <a name="clean-up-after-migration"></a>Очистка после миграции

После проверенной успешной миграции Contoso необходимо выполнить резервное копирование и сохранить локальные файлы резервной копии базы данных для хранения. Снимите с учета локальный сервер MariaDB.

## <a name="review-the-deployment"></a>Проверка развертывания

Теперь, когда выполняется миграция ресурсов в Azure, компании Contoso необходимо полностью ввести его в эксплуатацию и защитить свою новую инфраструктуру.

### <a name="security"></a>Безопасность

- Contoso необходимо убедиться, что новые базы данных Azure для экземпляра MariaDB и базы данных защищены. [Подробнее](https://docs.microsoft.com/azure/mariadb/concepts-security).
- Компания Contoso должна проверить [правила брандмауэра](https://docs.microsoft.com/azure/mariadb/concepts-firewall-rules) и конфигурации виртуальной сети, чтобы убедиться, что подключения ограничены только приложениями, которые им требуются.
- Настройте любые исходящие требования IP-адресов, чтобы разрешить подключения к [IP-адресам шлюза](https://docs.microsoft.com/azure/mariadb/concepts-connectivity-architecture)MariaDB.
- Обновите все приложения, чтобы они [затребовали SSL](https://docs.microsoft.com/azure/mariadb/concepts-ssl-connection-security) -соединения с базами данных.
- Настройте [частную ссылку](https://docs.microsoft.com/azure/mariadb/concepts-data-access-security-private-link) , чтобы весь трафик базы данных хранился в Azure и локальной сети.
- Включите [Azure Advanced Threat protection (ATP)](https://docs.microsoft.com/azure/mariadb/concepts-data-access-and-security-threat-protection).
- Настройте Log Analytics для отслеживания и оповещения о записях безопасности и журналах, представляющих интерес.

### <a name="backups"></a>Резервные копии

Убедитесь, что резервное копирование базы данных Azure для MariaDB выполняется с помощью геовосстановления. Это позволяет использовать резервные копии в парном регионе в случае регионального сбоя.

> [!IMPORTANT]
> Убедитесь, что ресурс "база данных Azure для MariaDB" имеет [блокировку ресурсов](https://docs.microsoft.com/azure/azure-resource-manager/management/lock-resources) , чтобы предотвратить удаление. Удаленные серверы нельзя восстановить.

### <a name="licensing-and-cost-optimization"></a>Лицензирование и оптимизация затрат

- Базу данных Azure для MariaDB можно масштабировать вверх или вниз, поэтому важно следить за производительностью сервера и баз данных, чтобы обеспечить соответствие вашим потребностям, а также снизить затраты.
- Ресурсы ЦП и хранилища связаны с затратами. Для выбора доступны несколько ценовых категорий. Убедитесь, что для рабочих нагрузок данных выбран соответствующий ценовой план.
- Счета за каждую реплику чтения выставляются на основе выбранных вычислений и хранилища.
- Используйте зарезервированную емкость, чтобы сэкономить на затратах.

## <a name="conclusion"></a>Заключение

В этой статье компания Contoso перенеса свои базы данных MariaDB в экземпляр базы данных Azure для MariaDB.