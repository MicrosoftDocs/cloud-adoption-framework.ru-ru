---
title: Новые возможности платформы внедрения Microsoft Cloud
description: Узнайте о последних обновлениях для платформы внедрения Microsoft Cloud для Azure.
author: JanetCThomas
ms.author: janet
ms.date: 03/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: internal
ms.openlocfilehash: 69e9ac4fc1002042285cb796c03633970fc25221
ms.sourcegitcommit: 36e85ac734b184de3f29884b744ea74c81ccc72b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2021
ms.locfileid: "103439633"
---
<!-- docutune:casing "Getting Started module" "internal Microsoft teams" OneMigrate -->

# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Новые возможности платформы внедрения Microsoft Cloud для Azure

Ниже приведен список недавних изменений, внесенных в облачную платформу внедрения.

Эта инфраструктура разработана совместно с клиентами, партнерами и внутренними группами Майкрософт. Новое и обновленное содержимое освобождается, когда оно становится доступным. Эти выпуски позволяют тестировать, проверять и уточнять рекомендации вместе с нами. Мы рекомендуем вам порекомендовать нам создать облачную платформу внедрения.

## <a name="march-2021"></a>Март 2021 г.

Этот выпуск еще является самым большим обновлением платформы, добавляя ряд новых обширных коллекций руководств, охватывающих всю платформу.

### <a name="adoption-journeys"></a>Пути внедрения

Наиболее примечательный в этом выпуске является добавление путей внедрения, которые предоставляют короткий, потребляемый оверлей или lenses, которые находятся на более глубокой платформе для ускорения работы. В этих сокращенных руководствах показано, как применять рекомендации в облачной инфраструктуре внедрения, [Microsoft Azure Well-Architected Framework](/azure/architecture/framework/), [центр архитектуры Azure](/azure/architecture), [Microsoft Learn](/learn)и других [документация Майкрософт](/) по внедрению конкретных технологических платформ. В таблице ниже приведены ссылки на страницу обзора для каждого из новых путей.

| Journey | Описание |
|--|--|
| [Гибридное &nbsp; и &nbsp; многооблачное](../scenarios/hybrid/index.md) | Руководство по жизненному циклу интеграции гибридных, многооблачных и Объединенных операций в облако внедрения в облаке. |
| [Современные контейнеры](../scenarios/aks/index.md) | Модернизации контейнеров обеспечивает быстрые инновации и переносимость рабочей нагрузки. Сведения о том, как интегрировать контейнеры в облачные пути внедрения. |
| [SAP в Azure](../scenarios/sap/index.md) | В рамках нашего Онемиграте (сценариев миграции) это путешествие между процессами миграции SAP и другими задачами, выполняющими полную миграцию, чтобы обеспечить полное масштабирование SAP в Azure. |

### <a name="cloud-economics"></a>Экономики в облаке

Основываясь на отзывах и полученных занятиях, это первый шаг к обновлению [методологии стратегии](../strategy/index.md) за счет интеграции [облачной программы Microsoft Cloud экономики](https://azure.microsoft.com/overview/cloud-economics/).

Мы обновили введение для каждой категории результатов бизнеса со ссылками на примеры внедрения в облако, демонстрирующие, как Организации достигают соответствующей бизнес-цели. В обновленные введения с демонстрационными примерами внедрения входят:

- [Финансовые показатели](../strategy/business-outcomes/fiscal-outcomes.md)
- [Показатели гибкости](../strategy/business-outcomes/agility-outcomes.md)
- [Показатели всемирного охвата](../strategy/business-outcomes/reach-outcomes.md)
- [Показатели вовлеченности клиентов](../strategy/business-outcomes/engagement-outcomes.md)
- [Показатели производительности](../strategy/business-outcomes/performance-outcomes.md)
- [Цели, связанные с устойчивостью](../strategy/business-outcomes/sustainability.md)

### <a name="enterprise-scale-updates"></a>Обновления корпоративного масштаба

Критическая область проектирования [топологии сети и подключения](../ready/azure-best-practices/define-an-azure-network-topology.md) включает новые статьи, упрощающие рационализацию отдельных компонентов структуры сети. Эти аспекты проектирования теперь включают руководство по [подключению к многооблачным поставщикам](../ready/azure-best-practices/connectivity-to-other-providers.md) , таким как облачная инфраструктура Oracle. Мы также выпустили новый модуль корпоративного масштаба terraform, чтобы продемонстрировать инвестиции корпорации Майкрософт в подходах с открытым исходным кодом к конфигурации зоны размещения Azure.

### <a name="anti-patterns"></a>Защита от шаблонов

Компании часто пропустили важные шаги в своем пути внедрения в облако. Новое руководство по [антишаблонам внедрения в облако](../antipatterns/antipatterns-to-avoid.md) выделяет общие моменты для клиентов, пропущенный шаг и самый быстрый путь к восстановлению. Антишаблоны распределяются по всем методам, но список из 10 лучших доступен в разделе Приступая к работе платформы.

## <a name="january-2021"></a>Январь 2021 г.

Чтобы помочь вам ускорить внедрение и инновации, мы добавили новые сведения об использовании GitHub и обновленных рекомендаций для машинного обучения. Мы опубликовали новую статью и видео, которые помогут вам выбрать наиболее подходящую зону.

| Статья | Описание |
|--|--|
| [Как &nbsp; GitHub &nbsp; ускоряет &nbsp; Внедрение облачных &nbsp; технологий](../scenarios/github-velocity/index.md) | В этой статье описываются преимущества использования GitHub для ускорения внедрения в облако за счет использования ресурсов с открытым кодом, сред совместной разработки, автоматизации и функций безопасности. |
| [Рекомендации по машинному обучению](../innovate/best-practices/machine-learning.md) | Мы обновили и развернули рекомендации для Машинное обучение. В рекомендации входят следующие. <br><br> <li> [Как подходить к операциям машинного обучения](../innovate/best-practices/how-to-approach-mlops.md) и [процессу млопс](../innovate/best-practices/mlops-process.md) <li> [Безопасность машинного обучения](../innovate/best-practices/ml-security.md) <li> [Вывод и развертывание машинного обучения](../innovate/best-practices/ml-deployment-inference.md) <li> [Определение вычислительных экземпляров для модели](../innovate/best-practices/dev-train-comp-instances-for-ml.md) <li> [Настройка рабочих областей машинного обучения](../innovate/best-practices/set-up-ml-workspaces.md) <li> [Надежные средства ИИ и ответственный подход к их использованию](../innovate/best-practices/trusted-ai.md) |
| [Выбор &nbsp; &nbsp; параметра Целевой &nbsp; зоны &nbsp;](../ready/landing-zone/choose-landing-zone-option.md) | Корпорация Майкрософт предлагает два варианта реализации для зон размещения: *Пуск Small, развертывание* и *Масштаб предприятия*. Используйте эту новую статью для просмотра обоих вариантов и выбора правильного подхода к Организации. |

## <a name="december-2020"></a>Декабрь 2020 г.

Мы изменили руководство по стратегии именования и маркировки, а также добавили рекомендации для сценариев миграции Moodle.

| Статья | Описание |
|--|--|
| [Разработка &nbsp; &nbsp; стратегии именования &nbsp; и &nbsp; маркировки &nbsp; для ресурсов Azure](../ready/azure-best-practices/naming-and-tagging.md) | Мы улучшили рекомендации по определению стратегии именования и маркировки. В дополнение к обзору мы разделили это руководство с несколькими статьями, в которых рассматриваются следующие темы: <br><br> <li> [Определение соглашения об именовании](../ready/azure-best-practices/resource-naming.md) <li> [Рекомендуемые сокращения для различных типов ресурсов Azure](../ready/azure-best-practices/resource-abbreviations.md) <li> [Определение стратегии добавления тегов](../ready/azure-best-practices/resource-tagging.md) |
| [Миграция развертывания Moodle в Azure](../scenarios/lamp/moodle/migration-overview.md) | Узнайте, как перенести развертывание Moodle системы управления обучением с открытым исходным кодом из локальной среды в Azure. Действия предназначены для использования портал Azure или Azure CLI развертывания. |

## <a name="october-2020"></a>Октябрь 2020 г.

Обновления за этот месяц включают в себя добавочные улучшения по всей инфраструктуре внедрения облака и поддержке веб-ресурсов.

Наши большие инвестиции посвящены созданию модулей Microsoft Learn для ускорения применения облачной инфраструктуры внедрения. В этом месяце мы выпустили перечисленные ниже модули. Обратите внимание, что модуль начало работы предоставляет наше первое руководство по вертикальной отрасли, представляя розничного клиента (Таилвинд Traders), который будет следовать за всеми основными модулями методологии.

| Модуль | Описание |
|--|--|
| [Модуль обзора](/learn/modules/microsoft-cloud-adoption-framework-for-azure/) | Введение в платформу для начального уровня. |
| [Модуль начало работы](/learn/modules/cloud-adoption-framework-getting-started/) | Ознакомьтесь с руководствами по началу работы, чтобы ускорить применение правильных методологий для преодоления конкретных блокировок. |
| [Целевые зоны Azure](/learn/modules/cloud-adoption-framework-ready/) | Прежде чем приступать к созданию облачной среды, ознакомьтесь с требованиями к эксплуатации и выберите наиболее подходящий продукт целевой зоны Azure, чтобы приступить к работе. |
| [Создание архитектуры корпоративного масштаба](/learn/paths/enterprise-scale-architecture/) | Создавайте целевые зоны в масштабе, следуя набору принципов проектирования корпоративного масштаба, эталонным архитектурам и эталонным реализациям. Четыре модуля для создания одного пути обучения до успешного выполнения. |

Мы также расширили результаты бизнеса, чтобы поделиться несколькими распространенными причинами бизнеса и подходами, которые продолжают покрываться на пост-КОВИД Marketplace.

| Статья | Описание |
|--|--|
| [Примеры результатов устойчивости](../strategy/business-outcomes/sustainability.md) | Узнайте, как облачные вычисления могут помочь в уменьшении излучения выбросов, использовать ресурсы более эффективно и сокращать объем окружающей среды. |
| [Оценка бизнес-результатов с помощью целей и ключевых результатов (Окрс)](../strategy/business-outcomes/okr.md) | Узнайте, как использовать Окрс для измерения результатов бизнеса. |
| [Оценка бизнес-результатов с помощью AppDynamics](../digital-estate/app-dynamics.md) | Понимание производительности приложения и взаимодействие с пользователем — это ключ к измерению результатов бизнеса. Узнайте, как AppDynamics может предоставить бизнес-аналитику для большинства вариантов использования. |
| [Обновление управления затратами: плашечные виртуальные машины](../govern/cost-management/best-practices.md#best-practice-reduce-nonproduction-costs) | Использование плашечных виртуальных машин в непроизводственных средах — это быстро развивающаяся практика для дальнейшего снижения затрат в этих средах. существующие среды. "У меня уже есть рабочая среда. Как применить принципы проектирования корпоративного масштаба?» Новая статья, посвященная переходу на корпоративный масштаб, может помочь. |

| Статья | Описание |
|--|--|
| [Переход с существующих сред Azure на корпоративный масштаб](../ready/enterprise-scale/transition.md) | Эта статья поможет организациям перемещаться по нужному пути на основе существующей среды Azure, переходя на корпоративный масштаб. |
| [Инфраструктура внедрения облачных технологий корпоративного уровня в масштабах предприятия](../ready/enterprise-scale/architecture.md) | Эта статья была обновлена для включения высокоуровневой схемы для архитектуры целевой зоны корпоративного уровня, основанной на топологии концентратора и периферийной сети, и обновлений для описания и перекрестной ссылки на критические области проектирования для архитектуры целевой зоны корпоративного уровня. |

## <a name="august-25-2020"></a>25 августа 2020 г.

Этот выпуск обеспечивает лучшее определение и критерии принятия решений относительно реализаций зоны размещения.

### <a name="operating-model"></a>Операционная модель

Одним из наиболее важных соображений при проектировании и реализации зоны размещения является ваша операционная модель. Способ работы в облаке повлияет на архитектуру и элементы управления, которые необходимо реализовать. Следующие статьи помогут согласовать целевую операционную модель с помощью нескольких моделей, общих в облаке. Затем сопоставьте их с наиболее подходящей реализацией, чтобы приступить к работе.

| Статья | Описание |
|--|--|
| [Сравнение распространенных операционных моделей](../operating-model/compare.md) | Эта статья является основным руководством по сравнению операционных моделей и выбору курса действий. |
| [Общие сведения об облачных операционных моделях](../operating-model/index.md) | Учебник для принятия решений по импорту в отношении вашей операционной модели. |
| [Определение вашей операционной модели с помощью КАФ](../operating-model/define.md) | Инфраструктура внедрения облачных технологий — это пошаговое руководством по созданию среды и внедрению облака в выбранную операционную модель. В этой статье вы узнаете, как различные методологии поддерживают разработку вашей операционной модели. |
| [Условия](../operating-model/terms.md) | Термины, которые, скорее всего, поступают при обсуждении вашей операционной модели с аналогами. Эти термины не так часто используются архитекторами или техническими специалистами, но они будут важны в этих беседах. |

### <a name="azure-landing-zones-additional-implementation-options"></a>Целевые зоны Azure: дополнительные параметры реализации

Параметры концепции и реализации за основными зонами Azure были созданы вместе с ведущими партнерами Майкрософт. Этот выпуск распознает существующую интеллектуальную собственность (IP), которую эти партнеры используют для ускорения внедрения в облако.

| Статья | Описание |
|--|--|
| [Целевые зоны партнеров](../ready/landing-zone/partner-landing-zone.md) | Ознакомьтесь с предложениями по начальной зоне Azure и сравните их с вашими партнерами. |
| [Варианты реализации](../ready/landing-zone/implementation-options.md) | Добавлена возможность добавления параметров целевой зоны партнера в существующие параметры реализации целевой зоны Azure. |
| [Эталонные реализации корпоративного масштаба](../ready/enterprise-scale/implementation.md) | Добавлена эталонная реализация звезды в эталонные реализации корпоративного масштаба. |

> [!NOTE]
> В статьях о новой целевой зоне для партнеров не указывается, как партнер должен определять или реализовывать целевую зону. Вместо этого он предназначен для добавления структуры к сложной беседе, поэтому вы можете лучше понять предложение партнера. Этот список вопросов и минимальных критериев оценки можно также использовать для сравнения предложений от потенциальных партнеров. Они также используются некоторыми участниками для более четкого обмена значениями параметров реализации начальной зоны Azure.

## <a name="july-17-2020"></a>17 июля 2020 г.

В этом выпуске добавляется несколько новых сценариев, чтобы сделать облачное внедрение более подделано действенным.

**Сценарии миграции:**

На новой [странице Обзор сценариев миграции](../scenarios/index.md) на методологии миграции показано, как Azure предоставляет #OneMigrate обещание. Она предоставляет подходы к переносу нескольких сценариев первого и сторонних производителей в Azure. Сюда входят новые сценарии миграции:

| Статья | Описание |
|--|--|
| [Виртуальный рабочий стол Windows](../scenarios/wvd/index.md) | Этот сценарий обеспечивает повышение производительности и ускоряет перенос различных рабочих нагрузок для поддержки взаимодействия с пользователями. |
| [Azure Stack](../scenarios/azure-stack/index.md) | Сведения о развертывании Azure в центре обработки данных с помощью центра Azure Stack. |

**Аналитика в облачной инфраструктуре внедрения:**

Решения аналитики теперь включены в платформу внедрения Microsoft Cloud. В этих новых разделах приводиться рекомендации по включению решений аналитики в процессе внедрения в облако.

| Статья | Описание |
|--|--|
| [Решение аналитики для Teradata, Netezza, Ексадата](../migrate/azure-best-practices/analytics/analytics-solutions-overview.md) | Сведения о переносе устаревших локальных сред, включая Teradata, Netezza и Ексадата, в современные аналитические решения. |
| [Обеспечение высокого уровня доступности Azure Synapse](../migrate/azure-best-practices/analytics/azure-synapse.md) | Узнайте о одном из ключевых преимуществ современной облачной инфраструктуры, встроенной высокой доступности и аварийного восстановления. |
| [Языки определения данных для миграции схемы (DDL)](../migrate/azure-best-practices/analytics/schema-migration-ddl.md) | Сведения об объектах базы данных и связанных с ними процессах при подготовке к переносу существующих данных. |

**AI в облачной инфраструктуре внедрения:**

Решения искусственного интеллекта и рекомендации теперь интегрированы в платформу внедрения Microsoft Cloud. Эти решения искусственного интеллекта могут помочь в ускорении инноваций с прогнозированием потребностей клиентов, автоматизации бизнес-процессов, обнаружении информации, поиске новых способов общения с клиентами и предоставления лучшего опыта в процессе внедрения в облако.

| Статья | Описание |
|--|--|
| [Ответственный подход к использованию ИИ](../strategy/responsible-ai.md) | Узнайте о принципах искусственного интеллекта, которые следует учитывать при реализации решений ИСКУССТВЕНного интеллекта, а также о том, как установить ответственную стратегию ии. |
| [Руководство по инновациям Azure: инновации и искусственный интеллект](../innovate/innovation-guide/predict.md) | Узнайте о том, как можно внедрять инновации с помощью искусственного интеллекта и найти лучшее решение на основе ваших потребностей в реализации. |
| [ИИ на платформе Cloud Adoption Framework](../innovate/ai/index.md) | Ознакомьтесь с рекомендуемой платформой, включающей средства, программы и содержимое (рекомендации, шаблоны конфигурации и руководство по архитектуре), чтобы упростить внедрение облачных методик и методик ИИ в большом масштабе. |
| [MLOps с использованием Машинного обучения Azure](../manage/mlops-machine-learning.md) | Ознакомьтесь с рекомендациями по операциям машинного обучения (Млопс). |
| [Инновации с использованием ИИ](../innovate/best-practices/predict.md) | Узнайте о решениях искусственного интеллекта (машинное обучение, приложения и агенты AI, интеллектуальный анализ знаний) и рекомендации, которые могут ускорить цифровое Invention. |

## <a name="june-15-2020"></a>15 июня 2020 г.

Правильная настройка облачной среды часто является первым и наиболее распространенным техническим блоком во время внедрения облака. В этом выпуске основное внимание уделяется рекомендациям, которые ускоряют развертывание облачных сред. Чтобы преодолеть этот распространенный блок, в облачной инфраструктуре внедрения появились начальные **зоны Azure**.

| Статья | Описание |
|--|--|
| [Целевые зоны Azure](../ready/landing-zone/index.md) | Целевые зоны Azure создают общий набор областей проектирования и параметров реализации для ускорения создания среды и согласования с планом внедрения облака и облачной операционной моделью. В этой новой статье более четко определены целевые зоны Azure. |
| [Целевые зоны Azure: области проектирования](../ready/landing-zone/design-areas.md) | Все целевые зоны Azure имеют общий набор из 8 областей проектирования. Перед развертыванием любой из основных зон Azure клиенты должны учитывать каждую из этих архитектур, чтобы принимать критически важные решения. |
| [Целевые зоны Azure: параметры реализации](../ready/landing-zone/implementation-options.md) | Выберите оптимальный вариант реализации целевой зоны Azure в зависимости от плана внедрения в облако и облачной рабочей модели. |

Существующие определения схем КАФ и модули КАФ terraform обеспечивают отправную точку для реализации целевой зоны Azure. Однако некоторым клиентам требуется более широкий вариант реализации, который может удовлетворить требования планов внедрения в облако корпоративного уровня. В этом выпуске добавляется **КАФ корпоративного масштаба** в параметры реализации зоны размещения Azure, чтобы заполнять ее. Ниже перечислены некоторые из статей, которые помогут вам начать работу с архитектурой КАФ Enterprise и эталонными реализациями.

| Статья | Описание |
|--|--|
| [Обзор корпоративного масштаба](../ready/enterprise-scale/index.md) | Общие сведения о корпоративном масштабировании |
| [Реализация КАФных зон корпоративного масштаба](../ready/enterprise-scale/implementation.md) | Варианты быстрой реализации и примеры GitHub |
| [Архитектура корпоративного уровня](../ready/enterprise-scale/architecture.md) | Общие сведения об архитектуре, основанной на масштабах предприятия |
| [Принципы проектирования масштаба предприятия](../ready/enterprise-scale/design-principles.md) | Изучите принципы архитектурного проектирования, которые помогут принять решения во время реализации, чтобы определить, соответствует ли этот подход вашей облачной операционной модели. |
| [Рекомендации по проектированию корпоративного масштаба](../ready/enterprise-scale/design-guidelines.md) | Оцените рекомендации корпоративного масштаба для выполнения общих областей проектирования основных зон Azure. |
| [Рекомендации по реализации](../ready/enterprise-scale/implementation-guidelines.md) | Ознакомьтесь с действиями, необходимыми для реализации корпоративного масштаба перед развертыванием. |

Партнеры являются важным аспектом успешного внедрения в облако. В рамках руководства по облачной инфраструктуре внедрения мы добавили ссылки для демонстрации важной роли, которую играют партнеры, и о том, как клиенты могут лучше привлекать партнеров. Список проверенных партнеров КАФ см. в разделе [предложения партнеров, предоставляемые](https://aka.ms/adopt/partneroffers) [специалистами по разработке Azure (MSP)](https://www.microsoft.com/azure/partners/azureexpertmsp?filters=all)или [Опытные специалисты для опытных специалистов](https://www.microsoft.com/azure/partners/advspec)по каф.

## <a name="may-15-2020"></a>15 мая 2020 г.

На основе отзывов мы создали новое содержимое, чтобы приступить к работе с облачной инфраструктурой внедрения. Новые руководства по началу работы позволяют перемещаться по платформе в зависимости от того, что нужно сделать. Также мы создадим новую целевую страницу, чтобы упростить поиск руководства, средств, изучения модулей и программ, которые поддерживают успешный процесс внедрения в облако.

| Статья | Описание |
|--|--|
| [Cloud Adoption Framework для Azure](../index.yml) | Целевая страница облачной инфраструктуры внедрения была изменена, чтобы упростить поиск руководства, средств, изучения модулей и программ, которые поддерживают успешный процесс внедрения в облако. |
| [Начало работы с Cloud Adoption Framework](./index.md) | Выберите Руководство по началу работы, которое соответствует целям внедрения в облаке. Эти распространенные сценарии предполагают использование Microsoft Cloud Adoption Framework для Azure. |
| [Понимание и документирование решений по выравниванию в базовых принципах](./cloud-concepts.md) | Узнайте о начальных решениях, которые должна понимать каждая группа, участвующая в принятии решений по внедрению в облако. |
| [Понимать и выровняйте иерархию портфеля](../reference/fundamental-concepts/hosting-hierarchy.md) | Узнайте, как иерархия портфеля показывает, как все ваши рабочие нагрузки и вспомогательные службы объединяются вместе. |
| [Как продукты Azure поддерживают иерархию портфеля?](../reference/fundamental-concepts/hierarchy-azure-tools.md) | Узнайте о средствах и решениях Azure, поддерживающих иерархию портфеля. |
| [Управление бизнес-согласованием](../organize/index.md) | Устанавливайте хорошо укомплектованные организационные структуры, которые эффективно работают в облачной модели. |

## <a name="april-14-2020"></a>14 апреля 2020 г.

Мы включили все средства и шаблоны для внедрения в облако в одном месте, чтобы их было проще найти.

| Статья | Описание |
|--|--|
| [Средства и шаблоны](../reference/tools-templates.md) | Найдите средства, шаблоны и оценки, которые помогут ускорить процесс внедрения в облако. |

## <a name="april-4-2020"></a>4 апреля 2020 г.

Продолжение итерации методологии миграции и готовой методологии для более тесного согласования с клиентами, партнерами и внутренними программами Майкрософт.

**Миграция обновлений методологии:**

| Статья | Описание |
|--|--|
| [Методика миграции](../migrate/index.md) | Эти изменения упрощают этапы миграции (Оценка рабочих нагрузок, развертывание рабочих нагрузок и рабочих нагрузок выпуска). Изменения также удаляют сведения о невыполненной работе миграции. Удаление этих сведений и создание ссылок на методологии плана, готовности и внедрения вместо этого обеспечивает гибкость для различных облачных приложений по внедрению, чтобы лучше согласовать их с методологией. |

**Обновления методологии готовности:**

| Статья | Описание |
|--|--|
| [Рефакторинг целевых зон](../ready/landing-zone/refactor.md) | **Новая статья:** В этой статье демонстрируется теория, посвященная началу работы с исходным шаблоном, с помощью деревьев принятия решений и рефакторинга для расширения целевой зоны и перехода к будущему состоянию готовности к выпуску Enterprise. |
| [Расширение целевой зоны](../ready/considerations/index.md) | **Новая статья:** Сборка в разделе параллельных итераций статьи рефакторинга показывает, как различные типы расширения целевой зоны внедряют общие принципы в поддерживающую платформу. Исходное содержимое этого обзора перемещено в узел [основные рекомендации по зонам](../ready/considerations/basic-considerations.md) в содержании. |
| [Разработка на основе тестирования (TDD) для целевых зон](../ready/considerations/test-driven-development.md) | **Новая статья:** Подход к рефакторингу значительно улучшен благодаря внедрению цикла разработки на основе тестирования для разработки и рефакторинга целевой зоны. |
| [TDD для целевой зоны в Azure](../ready/considerations/azure-test-driven-development.md) | **Новая статья:** Средства управления Azure предоставляют многофункциональную платформу для циклов TDD, а также для красных и зеленых тестов. |
| [Повышение безопасности целевых зон](../ready/considerations/landing-zone-security.md) | **Новая статья:** Общие сведения о рекомендациях в этом разделе, связанных с циклом TDD. |
| [Оптимизация операций с целевыми зонами](../ready/considerations/landing-zone-operations.md) | **Новая статья:** Список рекомендаций в статье Управление методологией с переходом к этому модульному подходу для улучшения операций, надежности и производительности. |
| [Оптимизация управления целевыми зонами](../ready/considerations/landing-zone-governance.md) | **Новая статья:** Список рекомендаций по управлению методологией с переходом к этому модульному подходу для улучшения управления, затрат и масштабирования. |
| [Начало работы с корпоративным масштабированием](../ready/enterprise-scale/index.md) | **Новая статья:** В этом примере демонстрируется подход, демонстрирующий различия в процессе, когда клиент начинается с шаблонов целевой зоны КАФ корпоративного масштаба. Эта статья поможет клиентам понять квалификаторы, которые будут поддерживать это решение. |

## <a name="march-27-2020"></a>27 марта 2020 г.

Мы добавили рекомендации по первоначальным подпискам, которые следует создать при внедрении Azure.

**Обновления руководства по подписке:**

| Статья | Описание |
|--|--|
| [Создание первоначальных подписок Azure](../ready/azure-best-practices/initial-subscriptions.md) | **Новая статья:** Создайте начальные и непроизводственные подписки и решите, следует ли создавать подписки "песочницы", а также подписку, которая будет содержать общие службы. |
| [Создание дополнительных подписок для масштабирования среды Azure](../ready/azure-best-practices/scale-subscriptions.md) | Сведения о причинах создания дополнительных подписок, перемещения ресурсов между подписками и советов по созданию новых подписок. |
| [Организация нескольких подписок Azure и управление ими](../ready/azure-best-practices/organize-subscriptions.md) | Создайте иерархию групп управления, чтобы упростить организацию и управление подписками Azure, а затем управлять ими. |

## <a name="march-20-2020"></a>20 марта 2020 г.

Мы добавили рекомендации, которые включают в себя средства, программы и содержимое, упорядоченное по персонажам, для успешного развертывания приложений на Kubernetes, от подтверждения концепции до рабочей среды, а также масштабирования и оптимизации.

**Kubernetes**

| Статья | Описание |
|--|--|
| [Разработка и развертывание приложений](../innovate/kubernetes/application-development.md) | **Новая статья:** Содержит контрольные списки, ресурсы и рекомендации по планированию разработки приложений, настройке конвейеров CI/CD и реализации обеспечения надежности сайта для Kubernetes. |
| [Проектирование и эксплуатация кластеров](../innovate/kubernetes/cluster-design-operations.md) | **Новая статья:** Содержит контрольные списки, ресурсы и рекомендации по настройке кластера, проектированию сети, масштабируемости в будущем, обеспечению непрерывности бизнес-процессов и аварийному восстановлению для Kubernetes. |
| [Безопасность кластеров и приложений](../innovate/kubernetes/cluster-application-security.md) | **Новая статья:** Содержит контрольные списки, ресурсы и рекомендации по планированию безопасности Kubernetes, производству и масштабированию. |

## <a name="march-2-2020"></a>2 марта 2020 г.

<!-- docutune:casing "Strategy, Plan, Ready, and Migrate" -->

В ответ на отзыв о непрерывности процесса миграции с помощью нескольких разделов инфраструктуры внедрения облачных решений, включая стратегию, планирование, готовность и миграцию, мы внесли следующие изменения. Эти обновления предназначены для того, чтобы облегчить понимание процесса планирования и внедрения при продолжении перехода.

**Обновления методологии стратегии:**

| Статья | Описание |
|--|--|
| [Выравнивание портфеля](../strategy/balance-the-portfolio.md) | Эта статья была перемещена ранее в методологии стратегии. Это позволяет понять процесс обработки идей ранее в жизненном цикле. |
| [Балансировка &nbsp; конкурирующих &nbsp; приоритетов](../strategy/balance-competing-priorities.md) | **Новая статья:** Описывает балансировку приоритетов между методологиями, чтобы помочь Вам проинформировать стратегию. |

**Обновления методологии плана:**

| Статья | Описание |
|--|--|
| [Рекомендации по оценке &nbsp; &nbsp;](../plan/contoso-migration-assessment.md) | Эта статья перемещена в новый раздел «рекомендации» методологии плана. Это позволяет получить представление о ходе оценки локальных сред, предшествующих жизненному циклу. |

**Обновления методологии готовности:**

| Статья | Описание |
|--|--|
| [Что &nbsp; такое &nbsp; &nbsp; Главная &nbsp; зона?](../ready/landing-zone/index.md) | **Новая статья:** Определяет термин "Главная зона". |
| Первая зона размещения | **Новая статья:** Раскрывает сравнение различных зон размещения. |
| [Целевая зона миграции КАФ](../ready/landing-zone/migrate-landing-zone.md) | Отделить определение схемы от выбора первой целевой зоны. |
| [Модули CAF Terraform](../ready/landing-zone/terraform-landing-zone.md) | Перемещен в раздел "Главная зона" методологии готовности для повышения terraform в диалоге "Целевая зона". |

**Миграция обновлений методологии:**

| Статья | Описание |
|--|--|
| [Обзор](../migrate/azure-migration-guide/index.md) | Добавлено более четкое описание и меньше шагов. |
| [Оценка](../migrate/azure-migration-guide/assess.md) | Добавлен раздел «несложные предположения», демонстрирующий работу этого уровня оценки с подходом к добавочной оценке, упомянутым в методологии плана. |
| [Классификация во время процессов оценки](../migrate/migration-considerations/assess/classify.md) | **Новая статья:** Описывает важность классификации каждого ресурса и рабочей нагрузки до миграции. |
| [анализа](../migrate/azure-migration-guide/migrate.md) | Добавлена ссылка на Унификлауд в средствах сторонних поставщиков в ответ на Конференции на конференциях уровня 1. |
| [Тестирование, &nbsp; Оптимизация &nbsp; и &nbsp; продвижение](../migrate/azure-migration-guide/optimize-and-transform.md) | Название этой статьи соответствует другим предложениям по улучшению процесса. |
| [Обзор оценки](../migrate/migration-considerations/assess/index.md) | Обновлено, чтобы продемонстрировать, что оценка на этом этапе посвящена оценке технического соответствия конкретной рабочей нагрузки и связанных ресурсов. |
| [Контрольный список планирования](../migrate/migration-considerations/prerequisites/planning-checklist.md) | Обновлено, чтобы уточнить важность операций при планировании миграции, чтобы обеспечить хорошо управляемую рабочую нагрузку после миграции. |

<!-- docutune:ignoreNextStep -->
