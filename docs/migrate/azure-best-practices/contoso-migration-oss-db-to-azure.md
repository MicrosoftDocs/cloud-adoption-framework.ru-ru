---
title: Перенос баз данных с открытым кодом в Azure
description: Узнайте, как компания Contoso перенеса свои локальные базы данных с открытым исходным кодом в Azure.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: d8b68e25f7cd52fc02037d64b79b282c816e41ec
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2020
ms.locfileid: "86198747"
---
# <a name="migrate-open-source-databases-to-azure"></a>Перенос баз данных с открытым кодом в Azure

В этой статье показано, как вымышленная компания Contoso оценивает, планирует и переносит свои различные локальные базы данных с открытым исходным кодом в Azure.

Компании Contoso требуется провести техническую и финансовую оценку, чтобы определить, можно ли выполнить перенос своих локальных рабочих нагрузок в облако Azure. В частности, команда компании Contoso хочет оценить совместимость компьютеров и баз данных для миграции. Кроме того, он хочет оценить емкость и затраты на выполнение ресурсов Contoso в Azure.

## <a name="business-drivers"></a>Бизнес-факторы

В компании Contoso возникают различные проблемы с поддержанием всех версий рабочих нагрузок базы данных с открытым исходным кодом, которые существуют в их сети. После совещания с последними инвесторами финансовый директор и CTO решили переместить все эти рабочие нагрузки в Azure. Это позволит им переходить от структурированной модели затрат к модели с гибкими операционными издержками.

Группа специалистов по ИТ тесно работала с бизнес-партнерами для понимания бизнес-и технических требований:

- **Повышение безопасности.** Компания Contoso должна иметь возможность более своевременно отслеживать и защищать все ресурсы данных. Они также хотели бы получить более централизованную настройку системы отчетности для шаблонов доступа к базе данных.

- **Оптимизация ресурсов вычислений:** Компания Contoso развернула большую локальную серверную инфраструктуру. Они имеют несколько SQL Server экземпляров, которые используют, но не используют базовые ЦП, память и диск, выделенные эффективно.

- **Повышение эффективности:** Компании Contoso необходимо удалить ненужные процедуры и упростить процессы для разработчиков и пользователей. Бизнесу требуется, чтобы он был быстрым и не тратить время или деньги, обеспечивая более быстрое выполнение требований клиентов. Администрирование базы данных должно быть уменьшено и/или свернуто после миграции.

- **Повышение гибкости:** Компания Contoso должна быть в большей мере реагировать на потребности бизнеса. Он должен иметь возможность реагировать быстрее, чем изменения в Marketplace, чтобы обеспечить успешную работу в глобальной экономике. ИТ-не должныся как или стать заблокированным.

- **Масштаб:** По мере успешного развития бизнеса компания Contoso должна предоставить системы, которые могут расти в одном темпе.

- **Затраты:** Владельцы предприятий и приложений хотят, чтобы они не заработали с высокими затратами на облако, когда планируется запускать приложения локально.

## <a name="migration-goals"></a>Цели миграции

Группа разработчиков Contoso Cloud прикрепляет цели для различных миграций. Эти цели использовались для определения лучших методов переноса.

| Требования | Сведения |
| --- | --- |
| **Производительность** | После миграции приложения в Azure должны иметь те же возможности производительности, что и приложения в локальной среде компании Contoso. Переход в облако не означает, что производительность приложения менее важна. |
| **Совместимость** | Contoso необходимо понимать совместимость своих приложений и баз данных с Azure. Contoso также должен понимать возможности размещения Azure. |
| **Источники данных** | Все базы данных будут перемещены в Azure без исключений. На основе анализа базы данных и приложений используемых функций SQL они будут перенесены в PaaS или IaaS. Все базы данных должны перемещаться. |
| **Приложения** | Приложения должны быть перемещены в облако везде, где это возможно. Если они не могут переместиться, им будет разрешено подключаться к перенесенной базе данных через сеть Azure только с помощью частных подключений. |
| **Затраты** | Компании необходимо получить сведения не только о параметрах миграции, но и о стоимости инфраструктуры после перехода в облако. |
| **Управление** | Группы управления ресурсами должны быть созданы для различных отделов и групп ресурсов для управления всеми переносимыми базами данных. Все ресурсы должны быть помечены сведениями о отделе для требований к возмещению. |
| **Ограничения** | Изначально не все филиалы, которые запускают приложения, будут иметь прямую ссылку ExpressRoute на Azure, поэтому этим офисам потребуется подключиться через шлюзы виртуальной сети. |

## <a name="solution-design"></a>Архитектура решения

Компания Contoso уже выполнила [оценку миграции](https://docs.microsoft.com/azure/cloud-adoption-framework/plan/contoso-migration-assessment) своего цифрового пространства с помощью функции " [Миграция Azure](https://docs.microsoft.com/azure/migrate/migrate-services-overview) " с [сопоставление служб](https://docs.microsoft.com/azure/azure-monitor/insights/service-map) .

![Процесс миграции ](./media/contoso-migration-oss-db-to-azure/migration-process.png)
 _рис. 1. процесс миграции._

### <a name="solution-review"></a>Проверка решения

Contoso оценивает предлагаемый дизайн, составляя список плюсов и минусов.

| Рассматриваемый вопрос | Сведения |
| --- | --- |
| **Преимущества** | Azure предоставит единую область прозрачности для рабочих нагрузок базы данных. <br><br> Расходы будут отслеживаться с помощью службы управления затратами Azure и выставления счетов. <br><br> Оплата за подразделение обеспечивает простую выплату за API-интерфейсы выставления счетов Azure. <br><br> Обслуживание сервера и программного обеспечения будет сокращено до сред, основанных на IaaS. |
| **Недостатки** | В связи с требованиями виртуальных машин на основе IaaS все равно придется управлять программным обеспечением на этих компьютерах. |

### <a name="budget-and-management"></a>Бюджет и управление

Перед миграцией необходима необходимая структура Azure для поддержки аспектов администрирования и выставления счетов в решении.

Для требований к управлению было создано несколько [групп управления](https://docs.microsoft.com/azure/governance/management-groups/overview) для поддержки организационной структуры.

В соответствии с требованиями к выставлению счетов каждый ресурс Azure [помечается](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources) с помощью соответствующих тегов выставления счетов.

### <a name="migration-process"></a>Процесс миграции

Миграция данных соответствует стандартному и повторяемому шаблону. Это включает следующие шаги, основанные на [рекомендациях корпорации Майкрософт](https://datamigration.microsoft.com/):

- Перед миграцией:
  - **Обнаружение:** Ресурсы базы данных инвентаризации и стек приложений.
  - **Оценка:** Оценка рабочих нагрузок и исправление рекомендаций.
  - **Преобразовать:** Преобразование исходной схемы для работы в целевом объекте.
- Миграция.
  - **Миграция:** Перенесите исходную схему, исходные данные и объекты в целевой объект.
  - **Данные синхронизации:** Синхронизация данных (для минимального времени простоя).
  - **Прямую миграцию:** Вырежьте источник на целевой объект.
- После миграции:
  - **Исправлять приложения:** Итеративное внесение и необходимые изменения в приложения.
  - **Выполнение тестов:** Итеративное выполнение функциональных и тестовых тестов производительности.
  - **Оптимизировать:** На основе тестов устраните проблемы с производительностью и повторите проверку, чтобы подтвердить повышение производительности.
  - **Снятие с учета ресурсов:** В старых виртуальных машинах и средах размещения выполняется резервное копирование и прекращение использования.

#### <a name="step-1-discovery"></a>Шаг 1. Обнаружение

Компания Contoso использовала миграцию Azure с Сопоставление служб для выявления зависимостей в среде Contoso. Служба "миграция Azure" автоматически обнаружила компоненты приложений в системах Windows и Linux и сопоставила взаимодействие между службами. С помощью Сопоставление служб функции службы "миграция Azure" отображаются подключения между серверами Contoso, процессами, задержкой входящего и исходящего подключения, а также портами в архитектуре, подключенной по протоколу TCP. Contoso требовалось только для установки [Microsoft Monitoring Agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) и [Microsoft dependency Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows).

С помощью миграции Azure компания Contoso обнаружила более 300 экземпляров баз данных, которые необходимо перенести. Из этих экземпляров примерно 40% могут быть перемещены в службы на основе PaaS. Из оставшихся 60 процентов они должны быть перемещены на подход на основе IaaS с помощью виртуальной машины, на которой работает соответствующее программное обеспечение базы данных.

#### <a name="step-2-application-assessment"></a>Шаг 2. Оценка приложения

Результаты оценки показали Contoso, что они используют в первую очередь приложения Java, PHP и Node.js. Они определили следующее:

- 100 приложения Java
- О 50 Node.js приложений
- О 25 приложениях PHP

#### <a name="step-3-database-assessment"></a>Шаг 3. Оценка базы данных

По мере инвентаризации баз данных каждый тип базы данных был проверен для определения метода переноса в Azure. Следующие рекомендации были выполнены при миграции базы данных.

| Тип базы данных | Сведения | целевого объекта | Руководство по миграции |
| --- | --- | --- | --- |
| **MySQL** | До миграции все поддерживаемые версии обновляются до поддерживаемой версии | База данных Azure для MySQL (PaaS) | [Программ](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)
| **PostgreSQL** | До миграции все поддерживаемые версии обновляются до поддерживаемой версии | База данных Azure для PostgreSQL (PaaS) | [Программ](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online) |
| **MariaDB** | До миграции все поддерживаемые версии обновляются до поддерживаемой версии | База данных Azure для MySQL (PaaS) | [Программ](https://datamigration.microsoft.com/scenario/mariadb-to-azuremariadb?step=1) |

#### <a name="step-4-migration-planning"></a>Шаг 4. Планирование миграции

Из-за большого количества баз данных компания Contoso настраивает Office для управления проектами, чтобы контролировать каждый экземпляр миграции базы данных. [Ответственность и обязанности](https://docs.microsoft.com/azure/cloud-adoption-framework/migrate/migration-considerations/assess/) были назначены каждой группе бизнеса и приложений.

Contoso также выполнил [проверку готовности рабочей нагрузки](https://docs.microsoft.com/azure/cloud-adoption-framework/migrate/migration-considerations/assess/evaluate). Эта проверка проверила компоненты инфраструктуры, базы данных и сети.

#### <a name="step-5-test-migrations"></a>Шаг 5. Тестирование миграции

Первая часть подготовки к миграции включала в себя тестовую миграцию каждой базы данных в среды перед установкой. Чтобы сэкономить время, они записывали все операции для миграции и записывают временные показатели для каждого из них. Чтобы ускорить миграцию, они обнаружили, какие операции миграции могут выполняться параллельно.

Все процедуры отката были обнаружены для каждой рабочей нагрузки базы данных в случае непредвиденных сбоев.

Для рабочих нагрузок на основе IaaS необходимо заранее настроить все необходимое программное обеспечение стороннего производителя.

После выполнения тестовой миграции компания Contoso могла использовать различные [средства оценки стоимости](https://docs.microsoft.com/azure/cloud-adoption-framework/migrate/migration-considerations/assess/estimate) Azure, чтобы получить более точную картину будущих эксплуатационных расходов на их миграцию.

#### <a name="step-6-migration"></a>Шаг 6. Миграция

Для рабочей миграции компания Contoso определила временные кадры для всех миграций баз данных и что может быть достаточно для выполнения в выходном окне (полночь с 00:00 до полуночи воскресенье) с минимальным временем простоя бизнеса.

### <a name="cleanup-after-migration"></a>Очистка после миграции

Contoso определил окно архива для всех рабочих нагрузок базы данных. По истечении срока действия этого окна ресурсы будут освобождены из локальной инфраструктуры. Сюда входят удаление рабочих данных с локальных серверов и прекращение использования сервера размещения после истечения срока действия последней рабочей нагрузки.

### <a name="review-the-deployment"></a>Проверка развертывания

Теперь, когда выполняется миграция ресурсов в Azure, компании Contoso необходимо полностью ввести его в эксплуатацию и защитить свою новую инфраструктуру.

#### <a name="security"></a>Безопасность

- Компания Contoso должна обеспечить безопасность своих новых рабочих нагрузок базы данных Azure. [Подробнее](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Компания Contoso должна проверить конфигурацию брандмауэра и виртуальной сети.
- Настройте частную ссылку, чтобы весь трафик базы данных хранился в Azure и локальной сети.
- Включите Azure Advanced Threat protection.

#### <a name="backups"></a>Резервные копии

Убедитесь, что резервное копирование баз данных Azure выполняется с помощью геовосстановления. Это позволяет использовать резервные копии в парном регионе в случае регионального сбоя.

> [!IMPORTANT]
>Убедитесь, что ресурс Azure имеет [блокировку ресурсов](https://docs.microsoft.com/azure/azure-resource-manager/management/lock-resources) , чтобы предотвратить удаление. Удаленные серверы можно восстановить.

#### <a name="licensing-and-cost-optimization"></a>Лицензирование и оптимизация затрат

- Многие рабочие нагрузки базы данных Azure можно масштабировать вверх или вниз, и производительность сервера и базы данных важна, чтобы обеспечить соответствие требованиям, предъявляемым к минимуму затрат.
- Ресурсы ЦП и хранилища связаны с затратами. Для выбора доступны несколько ценовых категорий. Убедитесь, что для рабочих нагрузок данных выбран соответствующий ценовой план.
- Счета за каждую реплику чтения выставляются на основе выбранных вычислений и хранилища.
- Используйте зарезервированную емкость, чтобы снизить затраты.

## <a name="conclusion"></a>Заключение

В этой статье компания Contoso оценивает, планирует и переносит свои базы данных с открытым исходным кодом в решения Azure PaaS и IaaS.