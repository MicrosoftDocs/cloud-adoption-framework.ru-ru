---
title: Решения аналитики для Teradata
description: Используйте инфраструктуру внедрения в облаке для Azure, чтобы узнать о аналитических решениях с помощью Teradata.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 85dc03afc7ea0d8c931c24009beb220d03b108e5
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452146"
---
<!-- cSpell:ignore DATEADD DATEDIFF Attunity Teradata Inmon NUSI Informatica Talend BTEQ FASTEXPORT QUALIFY ORC Parquet "Parallel Data Transporter" "Attunity Replicate" -->

# <a name="analytics-solutions-for-teradata"></a>Решения аналитики для Teradata

Существующие пользователи систем хранилища данных Teradata теперь ищут преимущества новейших сред (например, Cloud, IaaS, PaaS) и делегирования задач, таких как обслуживание инфраструктуры и разработка платформ, поставщику облачных услуг.

Хотя существует сходство между Teradata и Azure синапсе Analytics в том, что оба являются базами данных SQL, предназначенными для использования методов массовой параллельной обработки (MPP) для достижения высокой производительности запросов на больших объемах данных, существуют также некоторые базовые отличия в подходе:

- Устаревшие системы Teradata обычно устанавливаются локально, используя собственное оборудование, в то время как Azure синапсе Analytics использует облачное хранилище и ресурсы для вычислений.
- Обновление конфигурации Teradata — это основная задача, включающая дополнительное физическое оборудование и потенциально длительную перенастройку базы данных. Так как ресурсы хранения и вычислительных ресурсов являются отдельными в среде Azure, эти ресурсы можно легко масштабировать (в направлении вперед и вниз) независимо от возможности эластичной масштабируемости.
- Аналитика Azure синапсе может быть приостановлена или изменена по мере необходимости, чтобы сократить использование ресурсов и, следовательно, стоимость.

Чтобы максимально увеличить эти преимущества, необходимо перенести существующие (или новые) данные и приложения на платформу Azure синапсе Analytics, а во многих организациях это будет включать перенос существующего хранилища данных из устаревших локальных платформ, таких как Teradata. На высоком уровне базовый процесс будет включать следующие шаги:

<!-- markdownlint-disable MD033 -->

| Подготовка | Миграция | Действия после перемещения |
|---|---|---|
| <li> Определение области действия для переноса <li> Создание инвентаризации данных и процессов для миграции <li> Определение изменений модели данных (если они есть) <li> Указание соответствующих инструментов и компонентов Azure (и сторонних поставщиков), которые будут использоваться <li> Заблаговременное обучение персонала на новой платформе <li> Настройка целевой платформы Azure |  <li> Запустить небольшое и простое <li> Автоматизируйте, где это возможно <li> Использование встроенных средств и функций Azure для сокращения усилий при миграции <li> Миграция метаданных для таблиц и представлений <li> Перенос исторических данных для обслуживания <li> Миграция и реструктуризация хранимых процедур и бизнес-процессов <li> Миграция или рефакторинг процессов добавочной загрузки ETL/ELT |  <li> Мониторинг и документирование всех этапов процесса <li> Использование интерфейса для создания шаблона для будущих миграций <li> Повторное проектирование модели данных при необходимости с использованием новой платформы производительность и масштабируемость <li> Тестирование приложений и средств запросов <li> Производительность и оптимизация производительности запросов |

## <a name="migration-scope"></a>Область миграции

### <a name="choose-the-workload-for-the-initial-migration"></a>Выбор рабочей нагрузки для первоначальной миграции

Устаревшие среды Teradata обычно развиваются с течением времени, чтобы охватывать несколько областей субъектов и смешанных рабочих нагрузок. При принятии решения о начале работы над проектом начальной миграции следует выбрать область, которая будет иметь следующие возможности:

- Вы можете доказать жизнеспособность перехода на Azure синапсе Analytics, быстро предоставляя преимущества новой среды.
- Разрешите внутренним техническим сотрудникам получить соответствующее представление о задействованных процессах и средствах, которые можно использовать при миграции других областей.
- Создайте шаблон для дальнейших упражнений по миграции, которые относятся к исходной среде Teradata и текущим средствам и процессам, которые уже используются.

Хорошим кандидатом на первоначальную миграцию из среды Teradata, которая позволила бы упомянутые выше элементы, обычно является реализация рабочей нагрузки бизнес-аналитики (то есть не рабочей нагрузки OLTP) с моделью данных, которая может быть перенесена с минимальными изменениями — обычно схемой «звезда» или «снежинка».

В плане размера важно, чтобы объем данных, который должен быть перенесен в начальном упражнении, был достаточно большим, чтобы продемонстрировать возможности и преимущества среды Azure синапсе Analytics, сохранив время, как правило, в диапазоне 1-10 ТБ.

Один из возможных подходов к первоначальному проекту миграции, который позволит свести к минимуму риск и сократить время реализации начального проекта, заключается в ограничении области миграции на только киоски данных (например, часть базы данных OLAP в хранилище Teradata). Этот подход, по определению, ограничивает область миграции и обычно может быть достигнут в течение короткого промежутка времени, и поэтому может быть хорошей отправной точкой. Однако этот подход не будет решать такие более обширные темы, как миграция ETL и миграция исторических данных в рамках первоначального проекта миграции. Они должны быть решены на последующих стадиях проекта, так как перенесенный слой киоска данных заполнен данными и процессами, необходимыми для их построения.

## <a name="lift-and-shift-as-is-versus-a-phased-approach-incorporating-changes"></a>Приближение и сдвиг как есть по сравнению с поэтапным подходом, включающим изменения

Независимо от драйверов и области предполагаемой миграции, в общем случае существует два типа миграции:

### <a name="lift-and-shift"></a>Методика lift-and-shift

В этом случае существующая модель данных (например, схема "звезда") переносится в новую платформу Azure синапсе Analytics без изменений. Здесь основное внимание уделяется минимизации риска и времени, затрачиваемого на миграцию, уменьшая объем работ, которые необходимо выполнить для достижения преимуществ перехода в облачную среду Azure.

Это хорошо подходит для существующих сред Teradata, в которых предполагается перенос одного киоска данных, или если данные уже находятся в хорошо спроектированной схеме «звезда» или «снежинка» или, возможно, существуют временные давления для перехода на более современные среды.

### <a name="phased-approach-incorporating-modifications"></a>Поэтапный подход с включением изменений

В случаях, когда хранилище прежних версий было изменено в течение длительного времени, может потребоваться повторное проектирование для поддержания требуемых уровней производительности или поддержки новых данных (например, потоков IoT). Переход на Azure синапсе Analytics для получения преимуществ масштабируемой облачной среды может рассматриваться как часть процесса повторной разработки. Это может быть изменение базовой модели данных (например, перемещение из модели Inmon в хранилище данных).

Рекомендуется сначала переместить существующую модель данных "как есть" в среду Azure (при необходимости используйте экземпляр виртуальной машины Teradata в Azure, как описано ниже), чтобы использовать производительность и гибкость среды Azure для применения изменений повторного проектирования, используя возможности Azure, в которых можно вносить изменения, не затрагивая существующую исходную систему.

## <a name="using-a-vm-teradata-instance-as-part-of-a-migration"></a>Использование экземпляра виртуальной машины Teradata в процессе миграции

Одним из необязательных подходов к выполнению миграции из локальной среды Teradata является использование среды Azure, обеспечивающей экономичное облачное хранилище и масштабируемость эластичных баз данных для создания экземпляра Teradata в виртуальной машине Azure, совместно размещенной с целевой средой Azure синапсе Analytics.

При таком подходе для эффективного перемещения подмножества таблиц Teradata, которые должны быть перенесены в экземпляр виртуальной машины, в среде Azure можно использовать стандартные служебные программы Teradata, такие как транспорт параллельных данных Teradata (или средства репликации данных сторонних разработчиков, такие как Attunity Replication), а затем выполнять все задачи миграции. Такой подход имеет несколько преимуществ.

- После начальной репликации данных задачи миграции не затрагивают исходную систему.
- Привычные интерфейсы, средства и служебные программы Teradata доступны в среде Azure.
- В среде Azure не существует потенциальных проблем с доступностью пропускной способности сети между локальной исходной системой и облачной целевой системой.
- Такие средства, как фабрика данных Azure, могут эффективно вызывать такие служебные программы, как "параллельный транспорт Teradata" для быстрого и простого переноса данных.
- Процесс миграции полностью управляется и контролируется в среде Azure.

## <a name="use-azure-data-factory-to-implement-a-metadata-driven-migration"></a>Использование фабрики данных Azure для реализации миграции на основе метаданных

Это имеет смысл автоматизировать и управлять процессом миграции, используя возможности среды Azure. Такой подход также уменьшает влияние на существующую среду Teradata (которая, возможно, уже работает близко к полной емкости).

Фабрика данных Azure — это облачная служба интеграции данных, которая позволяет создавать управляемые данными рабочие процессы в облаке для оркестрации и автоматизации перемещения и преобразования данных. С помощью фабрики данных Azure можно создавать и включать в расписание управляемые данными рабочие процессы (конвейеры), которые могут принимать данные из разнородных хранилищ данных, обрабатывать и преобразовывать эти данные с помощью служб вычислений (например, Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics и машинного обучения Azure),

Создавая метаданные для перечисления таблиц данных для переноса и их расположения, можно использовать средства фабрики данных Azure для управления частями процесса миграции и их автоматизации.

## <a name="design-differences-between-teradata-and-azure-synapse-analytics"></a>Различия в проектировании для Teradata и Azure синапсе Analytics

### <a name="separate-databases-versus-schemas"></a>Отдельные базы данных и схемы

В среде Teradata можно определить несколько отдельных баз данных для отдельных частей общей среды, например, может существовать отдельная база данных для приема данных и промежуточных таблиц, база данных для базовых таблиц хранилища и другая база данных для киосков данных (иногда называемых семантическим слоем). Такие процессы, как конвейеры ETL/ELT, могут реализовывать межбазовые подключения между базами данных и перемещать данные между этими отдельными базами данных.

Среда Azure синапсе Analytics имеет одну базу данных, а схемы используются для разделения таблиц на логически разделенные группы. Поэтому рекомендуется использовать ряд схем в целевой службе Azure синапсе Analytics, чтобы имитировать отдельные базы данных, которые будут перенесены из среды Teradata. Если схемы уже используются в среде Teradata, то может потребоваться использовать новое соглашение об именовании для перемещения существующих таблиц и представлений Teradata в новую среду (например, объединить существующую схему и имена таблиц Teradata в новое имя таблицы Azure синапсе Analytics и использовать имена схем в новой среде для сохранения исходных имен баз данных). Другим вариантом является использование представлений SQL в базовых таблицах для поддержки логических структур, но некоторые потенциальные недостатки этого подхода:

- Представления в Azure синапсе Analytics доступны только для чтения, поэтому любые обновления данных должны выполняться в базовых таблицах.
- Возможно, слой (или уровни) существующих представлений уже существует, а добавление дополнительного уровня представлений может повлиять на производительность.

### <a name="table-considerations"></a>Рекомендации по таблицам

При переносе таблиц между различными технологиями обычно это необработанные данные вместе с метаданными, которые его физически перемещаются между двумя средами. Другие элементы базы данных из исходной системы (например, индексы) не переносятся, так как эти элементы могут не потребоваться, или они могут быть реализованы по-разному в новой целевой среде.

Однако важно понимать, где в исходной среде используются такие оптимизации производительности, как индексы, так как эти сведения могут быть полезны для определения того, где можно добавить оптимизацию производительности в новую целевую среду. Например, если в исходной среде Teradata была создана Нуси, она может указывать на то, что в рамках перенесенной аналитики Azure синапсе должен быть создан некластеризованный индекс, но другие методы оптимизации производительности (например, репликация таблиц) могут оказаться более применимыми, чем создание индексов, аналогичное простому.

### <a name="high-availability-for-the-database"></a>Высокий уровень доступности для базы данных

Teradata поддерживает репликацию данных между узлами с помощью `FALLBACK` параметра, где строки таблицы, расположенные физически на данном узле, реплицируются на другой узел в системе. Такой подход гарантирует, что данные не будут потеряны, если произошел сбой узла и предоставляет базу для сценариев отработки отказа.

Цель архитектуры высокого уровня доступности в базе данных SQL Azure — гарантировать, что ваша база данных будет работать в 99,99% времени, не беспокоясь о влиянии операций обслуживания и простоев. Azure автоматически обрабатывает критически важные задачи обслуживания, такие как исправления, резервные копии, обновления Windows и SQL, а также незапланированные события, такие как оборудование, программное обеспечение или сбои сети.

Хранилище данных в Azure синапсе Analytics автоматически создается из резервных копий с помощью моментальных снимков. Эти моментальные снимки являются встроенной функцией службы, которая создает точки восстановления. Ее не нужно включать специально. Точки автоматического восстановления в настоящее время не могут быть удалены пользователями, если служба использует эти точки для поддержки восстановления в соответствии с соглашением об уровне обслуживания.

Хранилище данных SQL Azure создает моментальные снимки хранилища данных в течение дня, создавая точки восстановления, доступные в течение семи дней. Этот срок нельзя изменить. Хранилище данных SQL Azure поддерживает целевую точку восстановления в 8 часов (RPO). Вы можете восстановить хранилище данных в основном регионе до любого из моментальных снимков, доступных за последние семь дней. Другие определяемые пользователем параметры доступны, если требуются более детализированные резервные копии.

### <a name="unsupported-teradata-table-types"></a>Неподдерживаемые типы таблиц Teradata

Teradata включает поддержку специальных табличных типов для временных рядов и временных данных. Синтаксис и некоторые функции для этих табличных типов не поддерживаются напрямую в Azure синапсе Analytics, но данные могут быть перенесены в стандартную таблицу с соответствующими типами данных, индексированием или секционированием по столбцу даты и времени.

Teradata реализует функциональность временного запроса посредством перезаписи запросов для добавления дополнительных фильтров в пределах временного запроса, чтобы ограничить применимый диапазон дат. Если эта функция в настоящее время используется в исходной среде Teradata и должна быть перенесена, то эту дополнительную фильтрацию необходимо добавить в соответствующие временные запросы.

Среда Azure также включает определенные функции для сложной аналитики в данных временных рядов, которые называются "аналитика временных рядов". Это предназначено для приложений анализа данных IoT и может быть более подходящим для этого варианта использования. Дополнительные сведения см. в статье служба " [аналитика временных рядов Azure](https://azure.microsoft.com/services/time-series-insights/)".

### <a name="teradata-data-type-mapping"></a>Сопоставление типов данных Teradata

Некоторые типы данных Teradata не поддерживаются напрямую в Azure синапсе Analytics. В следующей таблице показаны эти типы данных вместе с рекомендуемым подходом к их обработке. В таблице тип столбца Teradata — это тип, хранящийся в системном каталоге (например, в `DBC.ColumnsV` ).

Используйте метаданные из таблиц каталога Teradata, чтобы определить, требуется ли миграция любого из этих типов данных и разрешить это в плане миграции. Например, запрос SQL, подобный приведенному ниже, можно использовать для поиска любых вхождений неподдерживаемых типов данных, требующих внимания.

Существуют сторонние поставщики, предлагающие средства и службы для автоматизации миграции, включая сопоставление типов данных, как описано выше. Кроме того, если средство ETL стороннего производителя, например Informatica или Таленд, уже используется в среде Teradata, они могут реализовать все необходимые преобразования данных.

## <a name="sql-dml-syntax-differences"></a>Отличия синтаксиса SQL DML

Существует несколько отличий синтаксиса языка обработки данных SQL (DML) между Teradata SQL и Azure синапсе Analytics, которые следует учитывать при переносе:

- **Квалификация:** Teradata поддерживает `QUALIFY` оператор. Пример.

  `SELECT col1 FROM tab1 WHERE col1='XYZ'`

  Сторонние средства и службы могут автоматизировать задачи сопоставления данных:

  `QUALIFY ROW_NUMBER() OVER (PARTITION by col1 ORDER BY col1) = 1;`

  Это можно сделать в Azure синапсе следующим образом:

  `SELECT * FROM (SELECT col1, ROW_NUMBER() OVER (PARTITION by col1 ORDER BY col1) rn FROM tab1 WHERE c1='XYZ' ) WHERE rn = 1;`

- **Арифметические операции с датами:** В Azure синапсе имеются следующие операторы:

  - `DATEADD`и `DATEDIFF` , которые могут использоваться в `DATE` полях или `DATETIME` . Teradata поддерживает прямое вычитание по датам, например:

    `SELECT DATE1 - DATE2 FROM ...`

  - `LIKE ANY`синтаксис, например:

    `SELECT * FROM CUSTOMER WHERE POSTCODE LIKE ANY ('CV1%', 'CV2%', CV3%') ;`.

    Эквивалент в синтаксисе Azure синапсе:

    `SELECT * FROM CUSTOMER WHERE (POSTCODE LIKE 'CV1%') OR (POSTCODE LIKE 'CV2%') OR (POSTCODE LIKE 'CV3%') ;`

- В зависимости от параметров системы, сравнение символов в Teradata может быть не зависящим от регистра по умолчанию. В Azure синапсе эти сравнения всегда зависят от регистра.

## <a name="functions-stored-procedures-triggers-and-sequences"></a>Функции, хранимые процедуры, триггеры и последовательности

При миграции из устаревшей среды хранилища данных, такой как Teradata, часто бывают элементы, отличные от простых таблиц и представлений, которые необходимо перенести в новую целевую среду. Примерами таких функций являются функции, хранимые процедуры, триггеры и последовательности.

В рамках этапа подготовки необходимо создать инвентаризацию этих объектов, которые должны быть перенесены, и метод их обработки с соответствующим выделением ресурсов, назначенных в плане проекта.

Средства в среде Azure могут заменить функциональность, реализованную в виде функций или хранимых процедур, в среде Teradata. В этом случае, как правило, более эффективно использовать встроенные средства Azure вместо перекодирования функций Teradata.

Дополнительные сведения о каждом из этих элементов см. ниже.

### <a name="functions"></a>Функции

В большинстве случаев с большинством продуктов баз данных Teradata поддерживает системные функции, а также определяемые пользователем функции в реализации SQL. При переходе на другую платформу баз данных, например Azure синапсе, общие системные функции общедоступны и могут быть перенесены без изменений. Некоторые системные функции могут иметь немного другой синтаксис, но в этом случае необходимо автоматизировать все необходимые изменения.

Для системных функций, в которых нет эквивалента, или для произвольных определяемых пользователем функций, их может потребоваться перекодировать с помощью языков, доступных в целевой среде. Azure синапсе использует популярный язык Transact-SQL для реализации определяемых пользователем функций.

### <a name="stored-procedures"></a>Хранимые процедуры

Большинство современных продуктов баз данных позволяют хранить процедуры в базе данных. Teradata предоставляет язык СПЛ для этой цели. Хранимая процедура обычно содержит инструкции SQL и определенную логику и может возвращать данные или состояние.

SQL Azure хранилище данных также поддерживает хранимые процедуры с помощью T-SQL, поэтому при наличии хранимых процедур для переноса их необходимо соответствующим образом перекодировать.

### <a name="triggers"></a>Триггеры

Создание триггеров не поддерживается в Azure синапсе, но может быть реализовано в фабрике данных Azure.

### <a name="sequences"></a>Последовательности

Последовательности синапсе для Azure обрабатываются аналогичным образом для Teradata, посредством использования `IDENTITY` столбцов или кода SQL для создания следующего порядкового номера в ряде.

## <a name="extracting-metadata-and-data-from-a-teradata-environment"></a>Извлечение метаданных и данных из среды Teradata

### <a name="data-definition-language-ddl-generation"></a>Создание языка описания данных (DDL)

Можно изменить существующие `CREATE TABLE` данные Teradata и `CREATE VIEW` Scripts, чтобы создать эквивалентные определения (с измененными типами данных, как описано выше). Как правило, это подразумевает удаление дополнительных предложений, относящихся к Teradata (например, `FALLBACK` ).

Однако все сведения, указывающие текущие определения таблиц и представлений в существующей среде Teradata, поддерживаются в таблицах системных каталогов. Это лучший источник этих сведений, так как он гарантирует актуальность и полноту данных. Возможно, документация, обслуживаемая пользователем, не синхронизирована с текущими определениями таблиц.

Эти сведения можно получить с помощью представлений в каталоге, например `DBC.ColumnsV` , и можно использовать для создания эквивалентных `CREATE TABLE` инструкций DDL для эквивалентных таблиц в Azure синапсе.  

Средства миграции и извлечения, используемые сторонними производителями, также используют сведения о каталоге для достижения того же результата.

### <a name="data-extraction-from-teradata"></a>Извлечение данных из Teradata

Перенос необработанных данных в существующие таблицы Teradata с помощью стандартных служебных программ Teradata, таких как `BTEQ` и `FASTEXPORT` . Как правило, во время миграции важно как можно более эффективно извлекать данные, а рекомендуемый подход к использованию последних версий Teradata — использовать параллельный транспорт Teradata, который будет использовать несколько параллельных `FASTEXPORT` потоков для достижения лучшей пропускной способности.

Параллельный транспорт Teradata можно вызывать непосредственно из фабрики данных Azure. Это рекомендуемый подход к управлению процессом переноса данных (это справедливо, если экземпляр Teradata находится в локальной среде или копируется на виртуальную машину в окружении Azure, как описано выше).  
Рекомендуемые форматы данных для извлеченных данных — это текстовые файлы с разделителями-запятыми или схожими, а также оптимизированные (ORC) или Parquet файлы в столбцах.

Более подробные сведения о процессе переноса данных и ETL из среды Teradata см. в соответствующем разделе документа 2,1. Перенос данных ETL и загрузка из Teradata.

## <a name="performance-recommendations-for-teradata-migrations"></a>Рекомендации по производительности для миграции Teradata

Различия в подходе к настройке производительности

### <a name="data-distribution-options"></a>Параметры распространения данных

Azure включает спецификацию методов распределения данных для отдельных таблиц. Цель состоит в том, чтобы уменьшить объем данных, которые должны быть перемещены между узлами обработки при выполнении запроса.  

Для больших таблиц, связанных с большими таблицами, хэш-распределение одной или обеих таблиц в соединяемых столбцах гарантирует, что обработка соединения может выполняться локально, так как объединяемые строки данных уже будут размещены на одном и том же узле обработки.

Другой способ достижения локальных соединений для небольшой таблицы — соединений больших таблиц (обычно таблица измерений к таблице фактов в модели схемы «звезда») состоит в том, чтобы реплицировать таблицу измерения меньшего размера на все узлы, таким образом гарантируя, что любое значение ключа объединения в таблице большего размера будет иметь локальную доступную строку измерения. Затраты на репликацию таблиц измерений относительно низкие, если таблицы не велики. В этом случае лучше подходит подход к распространению хэш-кода, как описано выше.

### <a name="data-indexing"></a>Индексирование данных

Azure синапсе предоставляет ряд вариантов индексирования, но они отличаются в работе и использовании с теми, которые реализованы в Teradata. Дополнительные сведения о различных вариантах индексации см. в разделе [Проектирование таблиц в пуле синапсе Azure](https://docs.microsoft.com/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-overview).

Однако существующие индексы в исходной среде Teradata могут быть полезны для указания того, как данные в настоящее время используются и предоставляют сведения о кандидатах на индексирование в среде Azure синапсе.

### <a name="data-partitioning"></a>Секционирование данных

В таблицах фактов корпоративного хранилища данных может содержаться множество миллиардов строк и секционирования — это способ оптимизации обслуживания и выполнения запросов к этим таблицам путем разбиения их на отдельные части для уменьшения объема обрабатываемых данных. Спецификация секционирования для таблицы определена в `CREATE TABLE` инструкции.

Для секционирования можно использовать только одно поле на таблицу, и это поле даты, которое будет использоваться для фильтрации нескольких запросов по датам или диапазонам дат. Можно изменить секционирование таблицы после начальной загрузки при необходимости путем повторного создания таблицы с новым распределением с помощью `CREATE TABLE AS SELECT` инструкции. Подробное описание секционирования в Azure синапсе см. в разделе [секционирование таблиц в пуле СИНАПСЕ SQL](https://docs.microsoft.com/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition).

### <a name="data-table-statistics"></a>Статистика таблицы данных

Убедитесь, что статистика по таблицам данных актуальна. Это можно сделать, создав на `COLLECT STATISTICS` шаге задания ETL/ELT или включив автоматическую сбор статистики для таблицы.

### <a name="polybase-for-data-loading"></a>Polybase для загрузки данных

Polybase — наиболее эффективный метод загрузки больших объемов данных в хранилище, так как он может использовать параллельную загрузку потоков.

### <a name="use-resource-classes-for-workload-management"></a>Использование классов ресурсов для управления рабочей нагрузкой

Azure синапсе Analytics использует классы ресурсов для управления рабочими нагрузками. Как правило, крупные классы ресурсов обеспечивают лучшую производительность отдельных запросов, а небольшие классы ресурсов обеспечивают более высокие уровни параллелизма. Использование можно отслеживать с помощью динамических административных представлений, чтобы обеспечить эффективное использование соответствующих ресурсов.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о реализации миграции Teradata см. в учетная запись Майкрософт представителя по локальным предложениям миграции.