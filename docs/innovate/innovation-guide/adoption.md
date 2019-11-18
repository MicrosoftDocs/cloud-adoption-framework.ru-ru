---
title: Руководство по инновациям Azure. Подготовка к сбору отзывов клиентов
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Подготовка к сбору отзывов клиентов
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: a6eb791e22d834f51face8819133c0ada6774952
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752943"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Руководство по инновациям Azure. Подготовка к сбору отзывов клиентов

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Подготовка к сбору отзывов клиентов

::: zone-end

Внедрение, вовлечение и удержание пользователей вместе — залог успешной инновации. Почему?

Создание инновационного решения — это не просто предоставление пользователю того, что он хочет или о чем думает. Речь идет о формировании гипотезы, которую можно протестировать и улучшить. Это тестирование бывает двух типов:

- **количественное (обратная связь для тестирования):** означает действия, которые мы ожидаем увидеть;
- **качественное (обратная связь клиентов):** сообщает о том, что эти метрики означают для клиента.

Чтобы интегрировать циклы обратной связи, нужен общий репозиторий для решения. Централизованный репозиторий обеспечит возможность записывать все отзывы о проекте и реагировать на них. [GitHub](https://github.com) является хранилищем для программного обеспечения с открытым исходным кодом. Это также одна из наиболее часто используемых платформ для размещения репозитория исходного кода для коммерческих приложений. В статье по [созданию репозиториев GitHub](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) содержатся сведения по началу работы с репозиторием.

Каждый из приведенных ниже инструментов в Azure интегрируется с проектами, размещенными в GitHub, или совместим с ними.

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Количественная обратная связь для веб-приложений](#tab/Quantitative-Apps)

Application Insights — это инструмент отслеживания, который обеспечивает количественную обратную связь об использовании приложения практически в реальном времени. Эти данные помогут протестировать и проверить текущую гипотезу, чтобы сформировать следующую функцию или пользовательскую историю в списке невыполненной работы.

### <a name="action"></a>Действие

Чтобы просмотреть количественные данные о приложениях, выполните следующие действия:

1. Перейти в **Application Insights**.
   - Если приложение не отображается в списке, нажмите **Добавить** и следуйте инструкциям, чтобы начать настройку Application Insights.
   - Если нужное приложение есть в списке, выберите его.
1. В области **Обзор** представлена некоторая статистика о приложении. Выберите **Панель мониторинга приложения**, чтобы создать настраиваемую панель мониторинга и просмотреть данные, которые более актуальны для вашей гипотезы.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to Application Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы просмотреть данные о приложениях, откройте [портал Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Подробнее

- [Запуск мониторинга веб-приложения ASP.NET](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Начало работы с Azure Monitor Application Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Создание настраиваемых панелей мониторинга ключевых показателей эффективности с помощью Azure Application Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Количественная обратная связь для интерфейсов API](#tab/Quantitative-APIs)

Связанная экономика меняет способ внедрения инноваций на предприятиях. Рынки и отрасли попадают под влияние быстрее, чем когда-либо. Сбои в работе могут быть представлены в различных формах, и предприятия должны справляться с _дилеммой новатора_: как наладить темп изменений, не влияя на текущую деловую активность.

Предприятия используют интерфейсы API извне, чтобы изменить способ взаимодействия со своими клиентами и партнерами. Внутри они используют API-интерфейсы для беспроблемного подключения отдельных частей бизнеса. Экономика API действует в четырех стандартных блоках: социальном, мобильном, аналитическом и облачном. Приложения и службы можно быстро и экономически выгодно связать между собой для создания расширенных предлагаемых преимуществ.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Чтобы записать количественные данные об интерфейсах API, выполните следующие действия:

1. Щелкните **Службы управления API**.
2. Выберите нужный API из списка.
3. В разделе **Мониторинг** выберите **Параметры диагностики**.

Чтобы просмотреть количественные данные об API, выполните следующие действия:

1. Щелкните **Службы управления API**.
2. Выберите нужный API из списка.
3. В разделе **Мониторинг** выберите **Приложение**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы открыть службы управления API, перейдите на [портал Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Подробнее

- [Сбор отзывов об API-интерфейсах при помощи Azure Monitor](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor)

## <a name="qualitative-feedbacktabqualitative"></a>[Качественная обратная связь](#tab/Qualitative)

В очереди невыполненной работы (или на доске) обратная связь записывается в виде пользовательских историй. Кроме того, здесь связанная работа отслеживается как практические задачи. Инструменты Azure Boards можно интегрировать непосредственно в GitHub. Это обеспечивает беспроблемное взаимодействие между управлением обратной связью и любым исходным кодом.

::: zone target="docs"

### <a name="action"></a>Действие

Для Azure Boards и Azure Pipelines нужен портал, отдельный от GitHub и Azure.
Чтобы начать работу с любым из этих инструментов, перейдите к [DevOps Azure](https://dev.azure.com).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Действие

Чтобы создать проект DevOps, выполните следующие действия:

1. Откройте **Azure DevOps Projects**.
2. Нажмите **Создать проект DevOps**.
3. Выберите пункт **Среда выполнения, платформа и служба**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Projects" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Подробнее

Эти статьи помогут вам централизовать и контролировать отзывы, используя Azure Boards вместе с GitHub.

- [Сведения о начале работы с Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/?view=azure-devops)
- [Сведения об использовании Azure Boards и GitHub](https://docs.microsoft.com/azure/devops/boards/github?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Закрытие цикла с помощью конвейеров](#tab/pipelines)

Реакцией на отзывы не всегда будет добавление функции, запрашиваемой клиентом. Но каждая точка данных должна приводить к некоторым изменениям. Это изменение может касаться вашего образа мышления. Это также может быть совершенно другое техническое изменение, отличающееся от запрошенного. В любом случае конвейеры развертывания и такие инструменты, как Azure Pipelines, позволяют быстро публиковать эти изменения, поэтому ими можно быстро делиться с клиентом.

### <a name="action"></a>Действие

Чтобы просмотреть текущие развертывания в конвейере, выполните следующие действия:

1. Щелкните **Службы приложений**.
2. Выберите нужное приложение из списка.
3. В разделе **Развертывание** выберите **Центр развертывания** в области служб приложений.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы просмотреть свои приложения в Службе приложений, перейдите на [портал Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Подробнее

Приступите к созданию своих конвейеров развертывания:

- [Create your first pipeline](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2) (Создание первого конвейера)
- [Задачи выпуска GitHub](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
