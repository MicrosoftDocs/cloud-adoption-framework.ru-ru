---
title: Руководство по инновациям Azure. Привлечение клиентов через приложения
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как внедрять инновации, привлекая клиентов через приложения с помощью Azure.
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 3d8d8007125a0ffa6268132f1d608123c25c9c22
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058544"
---
::: zone target="docs"

# <a name="azure-innovation-guide-engage-customers-through-apps"></a>Руководство по инновациям Azure. Привлечение клиентов через приложения

::: zone-end

::: zone target="chromeless"

# <a name="engage-customers-through-apps"></a>Привлечение клиентов через приложения

::: zone-end

Инновации включают как модернизацию существующих приложений, размещенных в локальной среде, так и создание ориентированных на облако приложений с помощью контейнеров или бессерверных технологий. Azure предоставляет службы PaaS, такие как Служба приложений Azure, позволяющие легко модернизировать существующие приложения API и веб-приложения, написанные на .NET, .NET Core, Java, Node.js, Ruby, Python или PHP, для развертывания в Azure.

Модель контейнеров с открытым стандартом позволяет создавать микрослужбы или контейнеризировать существующие приложения и развертывать их в Azure. Это легко сделать благодаря управляемым службам, таким как "Служба Azure Kubernetes", "Экземпляры контейнеров Azure" и "Веб-приложение для контейнеров". Бессерверные технологии, такие как Функции Azure и Azure Logic Apps, используют модель потребления (с оплатой только за используемые ресурсы) и позволяют вам сосредоточиться на разработке приложения вместо развертывания инфраструктуры и управления ею.

<!-- markdownlint-disable MD025 -->

# <a name="deliver-value-fastertabdelivervaluefaster"></a>[Оперативное повышение рентабельности](#tab/DeliverValueFaster)

Одно из преимуществ облачных решений — возможность оперативно собирать отзывы и быстрее предоставлять полезные решения своим пользователям. Независимо от того, является этот пользователь внешним клиентом или пользователем в вашей компании, чем быстрее вы сможете получить отзывы о своих приложениях, тем лучше.

## <a name="azure-app-service"></a>Служба приложений Azure

Служба приложений Azure предоставляет среду размещения для приложений, что устраняет нагрузку в контексте управления инфраструктурой и исправления ОС. Она обеспечивает автоматизацию масштабирования в соответствии с потребностями пользователей и с учетом ограничений для сохранения уровня затрат.

Служба приложений Azure обеспечивает первоклассную поддержку таких языков, как ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP и Python. Если вам нужно разместить другой стек среды выполнения, компонент "Веб-приложение для контейнеров" позволяет быстро и легко разместить контейнер Docker в среде Службы приложений Azure, тем самым размещая пользовательский стек кода вне серверной бизнес-среды.

### <a name="action"></a>Действие

Чтобы настроить или отслеживать развертывания Службы приложений Azure, выполните следующие действия:

1. Щелкните **Службы приложений**.
2. Настройка новой службы: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими серверами: Выберите нужное приложение из списка размещенных приложений.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Службы Azure Cognitive Services позволяют внедрить расширенную аналитику непосредственно в приложение с помощью набора API-интерфейсов, благодаря которым можно использовать поддерживаемые корпорацией Майкрософт алгоритмы искусственного интеллекта и машинного обучения.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Чтобы настроить или отслеживать развертывания Azure Cognitive Services, сделайте следующее:

1. Перейдите к **Cognitive Services**.
2. Настройка новой службы: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими серверами: Выберите нужную службу в списке размещенных служб.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-bot-service"></a>Служба Azure Bot

Служба Azure Bot расширяет возможности стандартного приложения, добавляя естественный интерфейс для ботов, использующий ИИ и машинное обучение, что позволяет по-новому общаться с клиентами.

### <a name="action"></a>Действие

Чтобы настроить или отслеживать развертывания служб Azure Bot, выполните следующие действия:

1. Щелкните **Службы ботов**.
2. Настройка новой службы: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими серверами: Выберите нужный бот в списке размещенных служб.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FbotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-devops"></a>Azure DevOps

В процессе реализации инноваций вы, в конечном итоге, откроете для себя DevOps. Корпорация Майкрософт долго работала над локальным продуктом, известным как Team Foundation Server (TFS). В процессе внедрения инноваций мы разработали Azure DevOps — облачную службу, которая предоставляет средства создания и выпуска, поддерживающие множество языков и назначений для выпусков. Дополнительные сведения см. на странице [Azure DevOps](https://docs.microsoft.com/azure/devops).

## <a name="visual-studio-app-center"></a>Центр приложений Visual Studio

Так как мобильные приложения продолжают набирать популярность, одновременно растет потребность в платформе, которая может обеспечить автоматическое тестирование на реальных устройствах различных конфигураций. Центр приложений Visual Studio — это не только место для тестирования приложений в iOS, Android, Windows и macOS. Он также предоставляет платформу мониторинга, которая может использовать Azure Application Insights для быстрого и легкого анализа телеметрии. Дополнительные сведения см. в [обзоре Центра приложений Visual Studio](https://docs.microsoft.com/appcenter).

Центр приложений Visual Studio также предоставляет службу уведомлений, в которой один вызов может отправлять уведомления в приложение на разных платформах, не обращаясь к каждой службе уведомлений по отдельности. Дополнительные сведения см. в статье об использовании [push-уведомлений в Центре приложений Visual Studio](https://docs.microsoft.com/appcenter/push).

### <a name="learn-more"></a>Подробнее

- [Обзор Службы приложений Azure](https://docs.microsoft.com/azure/app-service/overview)
- [Развертывание в Azure с помощью Docker](https://docs.microsoft.com/azure/app-service/containers/quickstart-docker)
- [Общие сведения о Функциях Azure](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [Azure для разработчиков .NET и .NET Core](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)
- [Azure для разработчиков Python](https://docs.microsoft.com/azure/python)
- [Azure для разработчиков облачных решений Java](https://docs.microsoft.com/azure/java/?view=azure-java-stable)
- [Создание веб-приложения PHP в Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-php)
- [Документация по пакету SDK для JavaScript](https://docs.microsoft.com/azure/javascript)
- [Документация по пакету Azure SDK для Go](https://docs.microsoft.com/azure/go)
- [Решения DevOps](https://azure.microsoft.com/solutions/devops)

# <a name="create-cloud-native-appstabcloudnative"></a>[Создание приложений, ориентированных на облако](#tab/CloudNative)

<!-- markdownlint-disable MD026 -->

## <a name="what-are-cloud-native-applications"></a>Что такое ориентированные на облако приложения?

Ориентированные на облако приложения разработаны с нуля и оптимизированы для работы в облаке. Они слабо связаны и основаны на архитектуре микрослужб, используют управляемые службы, доступны для отслеживания, а также обеспечивают надежность и быстрый выход на рынок за счет непрерывной поставки. Обычно они переносимы и могут работать в динамических средах, таких как общедоступные, частные и гибридные облака. Ориентированные на облако приложения обычно создаются с помощью одного или нескольких из перечисленных ниже подходов.

- Микрослужбы
- Бессерверные приложения
- Контейнеры

## <a name="microservices"></a>Микрослужбы

Микрослужбы — это стиль архитектуры программного обеспечения, в котором приложения состоят из небольших независимых модулей, обменивающихся данными друг с другом при помощи четко определенных контрактов API. Эти служебные модули представляют собой полностью несвязанные строительные блоки, которые достаточно малы для реализации единой функциональности. Микрослужбы помогают в следующих ситуациях:

- создание служб независимо друг от друга;
- масштабирование служб автономно;
- использование наиболее подходящих подходов к развертыванию и языкам программирования;
- изолирование точек сбоя;
- оперативное повышение рентабельности.

### <a name="azure-kubernetes-service-aks"></a>Служба Azure Kubernetes (AKS)

Полностью управляемую службу Kubernetes можно использовать для обработки, обновления и масштабирования кластерных ресурсов по требованию. Служба AKS упрощает развертывание контейнерных приложений и управление ими. Она предоставляет бессерверную платформу Kubernetes со встроенными возможностями непрерывной интеграции и непрерывной поставки,а также функции безопасности и управления корпоративного уровня. Обеспечьте совместную работу специалистов по разработке и эксплуатации на единой платформе, позволяющей оперативно и уверенно создавать, доставлять и масштабировать приложения.

#### <a name="action"></a>Действие

Чтобы настроить или отслеживать службу Azure Kubernetes, сделайте следующее:

1. Откройте **Службы Azure Kubernetes**.
2. Настройка новой службы: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими серверами: Выберите нужную службу Kubernetes из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FmanagedClusters]" submitText="Go to Azure Kubernetes services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="event-based-solutions"></a>Решения на основе событий

### <a name="azure-functions"></a>Функции Azure

Решение "Функции Azure" предоставляет платформу для запуска небольших фрагментов кода или функций в облаке. Функции помогут при выполнении рефакторинга кода в архитектуру микрослужб.

Среда выполнения Функций Azure поддерживает множество языков, включая C#, Java, JavaScript и Python. Дополнительные сведения см. в статье о [поддерживаемых языках в решении "Функции Azure"](https://docs.microsoft.com/azure/azure-functions/supported-languages).

Еще одним преимуществом функций является возможность их запуска различными действиями и событиями, например триггерами HTTP, триггерами-таймерами и триггерами из других служб Azure, таких как хранилище BLOB-объектов, Сетка событий и служебная шина. См. дополнительные сведения о [триггерах и привязках в решении "Функции Azure"](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

#### <a name="action"></a>Действие

Чтобы настроить или отслеживать развертывания Функций Azure, выполните следующие действия:

1. Щелкните **Приложение-функция**.
2. Настройка нового приложения: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление имеющимися приложениями: Выберите нужное приложение из списка приложений-функций.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="serverless-solutions"></a>Бессерверные решения

Создавайте ориентированные на облако приложения без подготовки и контроля инфраструктуры, используя полностью управляемую платформу, где масштабирование, доступность и производительность контролируются автоматически. К преимуществам бессерверных решений Azure относятся:

- повышение скорости разработки;
- повышение производительности команды;
- улучшение организационного воздействия.

### <a name="azure-logic-apps"></a>Azure Logic Apps

Интегрируйте данные и приложения вместо написания сложного связующего кода между разнородными системами. Визуально создавайте бессерверные рабочие процессы с помощью Azure Logic Apps и используйте собственные API-интерфейсы, бессерверные функции или готовые соединители программного обеспечения как услуги (SaaS), включая Salesforce, Microsoft Office 365 и Dropbox.

#### <a name="action"></a>Действие

Чтобы настроить или отслеживать Azure Logic Apps, сделайте следующее:

1. Щелкните **Logic Apps**.
2. Настройка нового приложения: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление имеющимися приложениями: Выберите нужное приложение логики из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2Fworkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-api-management"></a>Управление бессерверными API

Публикуйте, защищайте, преобразуйте, обслуживайте и отслеживайте API-интерфейсы с помощью службы управления API-интерфейсами Azure — полностью управляемой службы, которая предлагает модель использования, разработанную и реализованную для естественного соответствия бессерверным приложениям.

#### <a name="action"></a>Действие

Чтобы настроить или отслеживать службы управления API, выполните следующие действия:

1. Щелкните **Службы управления API**.
2. Настройка новой службы: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими серверами: Выберите нужную службу из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="containers"></a>Контейнеры

Для модернизации вашего портфеля приложений Azure предоставляет различные службы контейнеров, позволяющие переносить имеющиеся приложения в контейнеры, а также создавать облачные приложения для микрослужб, чтобы быстрее предоставлять преимущества пользователям. Разрабатывайте, обновляйте и развертывайте помещенные в контейнеры приложения с помощью комплексных средств разработки и CI/CD. Управляйте контейнерами в масштабе с помощью полностью управляемой службы оркестрации контейнеров Kubernetes, которая интегрируется с Azure Active Directory. На любой стадии модернизации можно ускорить разработку контейнерных приложений при одновременном соблюдении требований к безопасности.

### <a name="azure-container-instances"></a>Экземпляры контейнеров Azure

Запускайте контейнеры Docker по запросу в управляемой бессерверной среде Azure. Экземпляры контейнеров Azure — это решение, которое подойдет для любого сценария. Службу можно использовать в изолированных контейнерах без оркестрации. Благодаря запуску рабочих нагрузок в службе "Экземпляры контейнеров" можно сосредоточиться на разработке и проектировании своих приложений вместо управления инфраструктурой для их запуска.

### <a name="action"></a>Действие

Чтобы настроить или отслеживать экземпляры контейнеров, выполните следующие действия:

1. Щелкните **Экземпляры контейнеров**.
2. Чтобы настроить новый экземпляр контейнера, сделайте следующее: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими экземплярами контейнеров: Выберите нужный экземпляр контейнера из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FcontainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-red-hat-openshift"></a>Azure Red Hat OpenShift

Azure Red Hat OpenShift обеспечивает гибкие возможности для самостоятельного развертывания полностью управляемых кластеров OpenShift. Поддерживайте соответствие требованиям, сосредоточившись на разработке своего приложения. За исправление, обновление и мониторинг главного узла, а также узлов инфраструктуры и приложения будут отвечать Майкрософт и Red Hat. Выберите собственные решения для реестра, сети, хранилища или CI/CD. Вы можете сразу же приступить к работе благодаря встроенным решениям для автоматизированного управления исходным кодом, создания контейнеров и приложений, развертывания, масштабирования, управления работоспособностью и многих других задач.

**Щелкните [Azure Red Hat OpenShift](https://docs.microsoft.com/azure/openshift/intro-openshift)** .

# <a name="isolate-points-of-failuretabisolatepointsoffailure"></a>[Изолирование точек сбоя](#tab/IsolatePointsOfFailure)

Когда первоначальное тестирование будет подходить к концу, проанализируйте способы изоляции и удаления точек сбоя. Благодаря распределенному характеру облачной платформы Azure можно спроектировать приложение, позволяющее избежать сбоев, одновременно улучшив его производительность.

## <a name="azure-front-door-service"></a>Azure Front Door Service

Azure Front Door Service обеспечивает масштабируемую, безопасную точку входа, с помощью которой можно предоставлять приложения по всему миру. В этой службе сочетаются оптимизация трафика для лучшей производительности и мгновенная глобальная отработка отказа. Вместо диспетчера трафика стоит использовать Azure Front Door Service, если вам необходимо устанавливать подключения по протоколу TLS (разгрузка SSL) или обрабатывать HTTP- или HTTPS-запросы на прикладном уровне.

### <a name="action"></a>Действие

Чтобы настроить или отслеживать экземпляры службы Front Door, сделайте следующее:

1. Щелкните **Front Door**.
2. Настройка нового экземпляра службы Front Door: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими экземплярами службы Front Door: Выберите нужный экземпляр службы Front Door из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ffrontdoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="traffic-manager"></a>Диспетчер трафика

Диспетчер трафика обеспечивает балансировку нагрузки на основе DNS, которую можно маршрутизировать в соответствии с различными правилами. Эта возможность помогает обеспечить устойчивость в случае сбоя развернутых служб. Диспетчер трафика также можно использовать для маршрутизации на основе сбоев и маршрутизации на основе производительности, предоставляя лучшие возможности с учетом географического расположения.

### <a name="action"></a>Действие

Чтобы настроить или отслеживать профили диспетчера трафика, выполните следующие действия:

1. Щелкните **Профили диспетчера трафика**.
2. Настройка нового профиля: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими профилями: Выберите нужный профиль из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ftrafficmanagerprofiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-content-delivery-network"></a>Сеть доставки содержимого Azure

Azure предлагает распределенную сеть доставки содержимого (CDN), которая позволяет своевременно предоставлять ресурсы, кэшируя их рядом с расположением пользователей. Такое кэширование позволяет повысить удобство работы пользователей. Кроме того, оно предотвращает проблемы во время скачивания контента, вызванные сбоями сети между конечной точкой CDN и центром обработки данных, в котором размещено приложение. Сеть доставки содержимого также могут использовать приложения, размещенные не в Azure.

### <a name="action"></a>Действие

Чтобы настроить или отслеживать профили сетей доставки содержимого, сделайте следующее:

1. Щелкните **Профили CDN**.
2. Настройка нового профиля: Нажмите кнопку **Добавить** и следуйте инструкциям на экране.
3. Управление существующими профилями: Выберите нужный профиль из списка.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.cdn%2Fprofiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Подробнее

- [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
- [Диспетчер трафика](https://docs.microsoft.com/azure/traffic-manager)
- [Сеть доставки содержимого](https://docs.microsoft.com/azure/cdn)