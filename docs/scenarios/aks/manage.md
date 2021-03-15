---
title: Управление решениями современных контейнеров
description: Описание влияния сценария на управление операциями
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e8c6d6074e075b6804038269dfb5f570dbe7488c
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102112880"
---
# <a name="manage-modern-container-solutions-clusters"></a>Управление кластерами современных решений контейнеров

[Инфраструктура внедрения облаков предоставляет основную методику для определения процессов управления операциями](../../manage/index.md) для облака в независимом смысле. Его руководство помогает установить базовые показатели управления операциями и другие специализированные уровни операций. Это руководство по-прежнему может применяться для организаций с сочетанием инфраструктуры как услуги (IaaS), платформы как услуги (PaaS) и контейнерными рабочими нагрузками. В этой статье описано, что необходимо интегрировать с существующими операциями для подготовки к управлению контейнерами. Здесь также описываются преимущества интеграции службы Azure Kubernetes Service (AKS) в стратегию управления контейнерами.

## <a name="business-alignment-for-operations-management-needs"></a>Бизнес-выравнивание для нужд управления операциями

Контейнеры удаляют зависимости на нескольких уровнях инфраструктуры, что позволяет улучшить возможности управления операциями. Чтобы реализовать эти операционные улучшения, может потребоваться пересмотреть общую стратегию управления облаком, начиная с выравнивания бизнеса.

Чтобы установить правильные методики управления операциями, необходимо понять, как контейнеры будут использоваться в планах внедрения в облаке, и какие преимущества вы хотите реализовать из этой смены в контейнерные рабочие нагрузки.

- Будет ли вы управлять несколькими технологическими решениями, такими как контейнеры, IaaS и PaaS, на облачной платформе?
- Будут ли централизованные команды поддерживать операции и управлять контейнером или платформой AKS? Переходит ли этот отчет к индивидуальным командам рабочей нагрузки?
- Будут ли централизованные команды поддерживать операции и управлять рабочими нагрузками, выполняемыми в каждом контейнере или модуле? Переходит ли этот отчет к индивидуальным командам рабочей нагрузки?
- Вы используете контейнеры для критически важных рабочих нагрузок?
- Вы используете контейнеры для менее критических или служебных рабочих нагрузок, чтобы снизить затраты?
- Насколько важна производительность и надежность отдельных рабочих нагрузок?
- Являются ли приложения в контейнерах без состояния? Нужно ли сохранять состояние для защиты и восстановления рабочих нагрузок в контейнерах?

На этих основных вопросах вы узнаете, как лучше всего интегрировать контейнеры и AKS в стратегию управления операциями.

## <a name="operations-baseline"></a>Базовые показатели операций

Реализация базового плана операций обеспечивает централизованный доступ к средствам, необходимым для работы со всеми ресурсами в облачной среде и управления ими. Если у вас нет базового плана операций для неконтейнерных ресурсов, можно реализовать [базовый план операций, определенный в методологии управления](../../manage/azure-server-management/index.md).

Базовый план операций должен включать средства и конфигурации, обеспечивающие видимость, мониторинг, операционное соответствие, оптимизацию, защиту и восстановление.

![Базовый план Operations Management](../../_images/manage/management-baseline.png)

Базовый план операций, описанный в статьях выше, не обеспечивает поддержку для контейнеров или платформы AKS. Тем не менее, он предоставляет основу для поддержки контейнеров, таких как Azure Monitor, Azure Backup и другие средства.

Если большая часть портфеля в облаке размещена в контейнерах, рассмотрите возможность включения специализированных операций платформы в следующий раздел в базовый план операций.

## <a name="platform-operations"></a>Операции платформы

Если эта реализация не является первым или только развернутой в облаке, у вас должен быть базовый план операций. В этом разделе указаны некоторые средства, которые можно включить для управления контейнером или развертыванием AKS.

### <a name="inventory-and-visibility"></a>Инвентаризация и визуальный контроль

Мониторинг контейнеров и кластеров AKS использует средства, панели мониторинга и оповещения, входящие в базовый план операций. Однако может потребоваться дополнительная настройка для получения данных из контейнеров в средства мониторинга операций, например [Azure Monitor для контейнеров](/azure/azure-monitor/containers/container-insights-overview?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json). Ознакомьтесь с [обзором Azure Monitor для контейнеров](/azure/azure-monitor/containers/container-insights-overview?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json) , чтобы собрать данные, необходимые для добавления контейнеров и операций платформы AKS в базовый план операций.

После настройки Azure Monitor для сбора данных в контейнерах можно отслеживать следующие области в рамках процессов централизованного управления:

- Выявление кластеров, работающих в различных регионах, в идеале, связанных с записью в дереве служб, и выявление ключевых фактов в этих кластерах
  - Выявление пула узлов кластера, сети и топологий хранилища этих кластеров
  - Выявление версии AKS и образа узла соотношением.
- Указание использования ресурсов узла кластера (процесс, память и хранилище)
- Выявление контейнеров, выполняющихся на узлах, и их вклада в использование узла
- Изучите поведение кластеров в среднем и максимальных нагрузках. Эта информация может помочь определить потребности в емкости, а также максимальную нагрузку, которую может выдержать кластер.
- Настройте оповещения для упреждающего уведомления или записи, когда загрузка ЦП и памяти на узлах или контейнерах превышает пороговые значения или когда состояние работоспособности возникает в кластере в свертке работоспособности инфраструктуры или узлов.
- Использование [запросов](/azure/azure-monitor/containers/container-insights-log-search) для создания общего набора предупреждений, панелей мониторинга и подробных подробных сведений о выполнении анализа

Эти данные также будут поддерживать группы операций рабочей нагрузки, предоставляя подробные сведения о рабочих нагрузках, выполняемых на контейнерной платформе:

- Просмотреть данные об использовании ресурсов рабочих нагрузок на узле, не относящихся к стандартным процессам, поддерживающим pod.
- Интеграция с [Prometheus](/azure/azure-monitor/containers/container-insights-prometheus-integration) для просмотра метрик приложения.
- Мониторинг рабочих нагрузок контейнера, развернутых в локальной среде AKS Engine и подсистеме AKS на Azure Stack.
- Мониторинг рабочих нагрузок контейнера, развернутых в Azure Red Hat OpenShift.
- Мониторинг рабочих нагрузок контейнера, развернутых в службе Arc Azure Kubernetes (Предварительная версия).

### <a name="operations-compliance"></a>Соответствие операций

Установка исправлений, Настройка и изменение размера происходят на нескольких разных уровнях в контейнерной среде. Операторы могут находиться в разных группах, в зависимости от того, какой подход требуется для работы. Чтобы обеспечить соответствие операций, оператор будет отслеживать использование, изменять размер ресурсов для балансировки производительности и затрат, а также исправлять базовые системы для снижения риска и потери конфигурации. Каждая из них — это задачи, которые центральные ИТ организации обычно доставляют в рамках базовых показателей операций для решений IaaS и PaaS.

В кластерной среде Azure эти задачи выполняются на нескольких уровнях: кластер AKS, образ узла и ОС узла. Все эти задачи становятся более зависимыми от понимания и работы рабочих нагрузок, выполняемых в кластерах или пулах отдельных узлов. Следующие инструкции помогут оценить, что и если вы хотите сделать для работы с средами контейнера.

- Если размер и установка исправлений кластера AKS, образ узла или ОС узла доставляются в рамках конвейера развертывания для приложения или зависят от архитектуры или конфигурации приложения, то лучше переместиться в эксплуатацию для группы рабочей нагрузки, чтобы получить детализированный контроль. Так как рабочие нагрузки часто зависят от функций оркестрации, это наиболее распространенный шаблон, так как непредвиденное изменение AKS версии или изменение образа узла может быть разрушительным для рабочей нагрузки или ее средств выполнения.
- Для менее распространенных централизованных кластеров, поддерживающих портфель рабочих нагрузок и различных приложений, Группа централизованных операций может по-прежнему отвечать за задачи обеспечения соответствия требованиям, приведенные ниже руководства помогут доставлять эти задачи в кластерах. Выполнение этих задач на регулярной основе не влечет за собой операции, связанные с платформой. В Центральных средах существует существенный риск, и тщательное тестирование обновлений в подготовительной среде, четко и придерживается запланированного обслуживания и планы на непредвиденные случаи для несоответствующих рабочих нагрузок. Одно из неудачных обновлений может быть единственной точкой отказа, и одна из задач, которая не может обновиться, может привести к прекращению поддержки кластера. Планирование и Управление кластерами клиентов с помощью комплексной экспертизы.

Для обоих типов кластера следуйте указаниям по обновлению, образам узлов и обновлениям ОС узла, приведенным ниже:

- [Обновление кластера AKS](/azure/aks/upgrade-cluster?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json)
- [Обновление образа узла](/azure/aks/node-image-upgrade?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json)
- [Обновления ОС узла процесса](/azure/aks/node-updates-kured?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json)
- [Руководство по установке исправлений и обновлению](/azure/architecture/operator-guides/aks/aks-upgrade-practices?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json)

### <a name="protect-and-recover"></a>Защита и восстановление

Узлы AKS являются временными, и поэтому резервное копирование не выполняется так, чтобы их можно было восстановить отдельно. Восстановление после инцидента может привести к повторному развертыванию рабочих нагрузок в новом пуле узлов или в целом новом кластере в зависимости от области инцидента.

- Выберите Добавление [соглашения об уровне обслуживания "время работы" в кластер](/azure/aks/uptime-sla).
- Для более высоких соглашений об уровне обслуживания Вы также можете рассмотреть рекомендации по [многорегиону BCDR](/azure/aks/operator-best-practices-multi-region?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json) , чтобы обеспечить дополнительную защиту.
- Так как кластеры не должны содержать состояние, восстановление внешнего состояния обрабатывается с помощью существующих руководств по базовым показателям операций. Если вы передали в кластере состояние, убедитесь, что следующие [Операторы рекомендованы для хранения](/azure/aks/operator-best-practices-storage?bc=/azure/cloud-adoption-framework/_bread/toc.json&toc=/azure/cloud-adoption-framework/toc.json), и получите стратегию [резервного копирования и восстановления этих данных](/azure/aks/operator-best-practices-storage#secure-and-back-up-your-data) для конкретной рабочей нагрузки. Использование таких средств, как [велеро](https://github.com/vmware-tanzu/velero) , является примером операций, связанных с платформой, которые расширяют базовые показатели операций.
  - Если портфель приложений непоследовательно применяет состояние, рекомендуется, чтобы Центральная группа эксплуатации не пыталась поддерживать оба решения. Вместо этого следует стандартизировать цепочки инструментов требуемого состояния для всех контейнеров, но не переменять ответственность за альтернативные решения по восстановлению для групп операций рабочей нагрузки. Такой подход обеспечивает свободу разработки для разработчиков, сокращает затраты на центральную стоимость и предоставляет стимулы к снижению затрат для групп рабочей нагрузки, чтобы обеспечить соответствие стандарту.

## <a name="workload-operations"></a>Операции рабочих нагрузок

В разделе операции платформы выше показан общий диалог при управлении кластерами AKS. Являются ли Kubernetes кластерами платформой технологии для централизованного управления? Или они являются средством рабочей нагрузки, которым должны управлять группы, владеющие каждой рабочей нагрузкой? Этот вопрос отличается для разных организаций. Константа, наблюдаемая в большинстве организаций, заключается в том, что контейнеры и AKS предназначены для предоставления группам рабочей нагрузки большей гибкости в том, как они хотят работать с каждой рабочей нагрузкой, и предоставляют определенные функции для этих рабочих нагрузок, чтобы использовать их в своей архитектуре, чтобы помочь владельцам и клиентам приложения.

Операции рабочей нагрузки могут создаваться на основе существующих базовых планов операций и операций, зависящих от платформы. Вы также можете безопасно управлять кластером AKS, используя полностью децентрализованные операции рабочей нагрузки. В любом случае, если вам нужно повысить эффективность операций, чтобы сосредоточиться на конкретных результатах конкретной рабочей нагрузки, можно использовать [платформу Azure Well-Architected Framework](/azure/architecture/framework/) и [Microsoft Azure Well-Architected проверки](https://aka.ms/architecture/review) , чтобы получить конкретные сведения о типах рабочих процессов и средствах, используемых для рабочей нагрузки.

## <a name="next-step-your-next-migration-iteration"></a>Следующий шаг: Следующая итерация миграции

После завершения миграции современных контейнеров группа по внедрению в облако может начать следующую миграцию для конкретного сценария. Кроме того, если есть дополнительные платформы для переноса, эту серию статей можно использовать повторно, чтобы попытаться выполнить миграцию или развертывание современных контейнеров.

- [Стратегия для современных контейнеров](./strategy.md)
- [Планирование современных контейнеров](./plan.md)
- [Проверка среды или начальных зон Azure](./ready.md)
- [Перенос рабочих нагрузок в современные контейнеры](./migrate.md)
- [Внедрять новые решения на основе современных контейнеров](/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
- [Управление решениями современных контейнеров](./govern.md)
- [Управление решениями современных контейнеров](./manage.md)