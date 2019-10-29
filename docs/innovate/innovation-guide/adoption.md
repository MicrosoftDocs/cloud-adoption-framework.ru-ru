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
ms.openlocfilehash: ec17c66fa92abc292a19a8e74c215111d8638a05
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769369"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Руководство по инновациям Azure. Подготовка к сбору отзывов клиентов

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Подготовка к сбору отзывов клиентов

::: zone-end

Внедрение, вовлечение и удержание пользователей вместе являются ключом к успешной инновации. Почему?

Создание инновационного решения — это не предоставление пользователю того, что он хочет или о чем думает. Речь идет о формировании гипотезы, которую можно протестировать и улучшить. Это тестирование бывает двух типов: количественное (обратная связь для тестирования), которое означает действия, которые мы ожидаем увидеть; качественное (обратная связь клиентов), которое сообщает о том, что эти метрики означают для клиента. Вместе они формируют последующие гипотезу и улучшения решения. Эти циклы обратной связи являются основой [процесса "создание — оценка — обучение"](../considerations/adoption.md), который лежит в основе этой методологии.

Прежде чем интегрировать циклы обратной связи, необходимо обязательно иметь общий репозиторий для решения. Централизованный репозиторий предоставит возможность осуществлять запись всех отзывов о проекте и реагировать на них.  [GitHub](https://github.com/) является хранилищем для программного обеспечения с открытым исходным кодом. Это также одна из наиболее часто используемых платформ для размещения репозитория исходного кода для коммерческих приложений. В статье по [созданию репозиториев GitHub](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) содержатся сведения по началу работы с репозиторием.

Каждый из следующих инструментов в Azure интегрируется с (или совместим с) проектами, размещенными в GitHub:

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Количественная обратная связь для веб-приложений](#tab/Quantitative-Apps)

Application Insights — это инструмент отслеживания, который позволяет получать количественную обратную связь об использовании приложения практически в режиме реального времени. Эта обратная связь может помочь протестировать и проверить текущую гипотезу, чтобы сформировать следующую функцию или пользовательскую историю в списке невыполненной работы.

### <a name="action"></a>Действие

Чтобы просмотреть количественные данные о приложениях, выполните следующие действия:

1. Выберите **App Insights**.
2. Если приложение не отображается в списке, щелкните ссылку **Добавить +** и следуйте инструкциям, чтобы начать настройку App Insights.
3. Если нужное приложение есть в списке, выберите его.
4. В области **Обзор** представлена некоторая статистика о приложении. Перейдя по ссылке **Панель мониторинга приложения**, вы сможете создать настраиваемую панель мониторинга, чтобы просмотреть данные, которые более актуальны для вашей гипотезы.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to App Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы просмотреть данные о приложениях, перейдите на [портал Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Подробнее

- [Запуск мониторинга веб-приложения ASP.NET](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Использование Azure Application Insights для анализа информации о том, как пользователи используют приложение](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Создание настраиваемых панелей мониторинга ключевых показателей эффективности с помощью Azure Application Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Количественная обратная связь для интерфейсов API](#tab/Quantitative-APIs)

Связанная экономика меняет способ внедрения инноваций на предприятиях.  Рынки и отрасли попадают под влияние быстрее, чем когда-либо. Сбои в работе могут быть представлены в различных формах, и предприятия должны справляться с **дилеммой инноватора**: как наладить темп изменений, не осуществляя влияние на текущую деловую активность.

Предприятия используют интерфейсы API извне, чтобы изменить способ взаимодействия с клиентами и их партнерами. Изнутри они используют API-интерфейсы для беспроблемного подключения отдельных частей бизнеса. Экономика API действует в четырех стандартных блоках: социальном, мобильном, аналитическом и облачном. Приложения и службы можно быстро и экономически выгодно связать между собой для создания расширенных предлагаемых преимуществ.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Действие

Чтобы записать количественные данные об интерфейсах API, выполните следующие действия:

1. Выберите **Служба управления API**.
2. Выберите нужный API из списка.
3. В разделе **Мониторинг** выберите **Параметры диагностики**.

Чтобы просмотреть количественные данные об API, выполните следующие действия:

1. Выберите **Служба управления API**.
2. Выберите нужный API из списка.
3. В разделе **Мониторинг** выберите **Приложение**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы открыть Службу управления API, перейдите на [портал Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Подробнее

Эта статья поможет вам использовать [Azure Monitor для получения отзывов об API](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor).

## <a name="qualitative-feedbacktabqualitative"></a>[Качественная обратная связь](#tab/Qualitative)

В очереди невыполненной работы (или на доске) обратная связь записывается в виде пользовательских историй. Кроме того, здесь связанная работа отслеживается как действенные задачи. Azure Boards могут быть интегрированы непосредственно в GitHub. Это обеспечивает беспроблемное взаимодействие между управлением обратной связью и любым исходным кодом.

::: zone target="docs"

### <a name="action"></a>Действие

Для Azure Board и Azure Pipelines требуется портал, отдельный от GitHub и Azure.
Чтобы начать работу с любым из этих инструментов, перейдите к [DevOps Azure](https://dev.azure.com/).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Действие

Чтобы создать проект DevOps, выполните следующие действия:

1. Перейдите к **проекту Azure DevOps**.
2. Щелкните **Создать проект DevOps**.
3. Выберите **среду выполнения, платформу и службу**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Project" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Подробнее

По следующим ссылкам содержатся сведения, которые помогут выполнить централизацию отзывов и управление ими с помощью Azure Boards и GitHub:

- [Сведения о начале работы с Azure Boards](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)
- [Сведения об использовании Azure Boards и GitHub](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Закрытие цикла с помощью конвейеров](#tab/pipelines)

Выполнение действий в ответ на обратную связь не всегда приводит к тому, что клиент запрашивает функцию. Но каждая точка данных должна приводить к некоторым изменениям. Это изменение может заключаться в том, как вы думаете о вещах. Это также может быть совершенно другое техническое изменение, отличающееся от того, что было запрошено. В любом случае конвейеры развертывания и такие инструменты, как Azure Pipelines, позволяют быстро публиковать эти изменения, поэтому ими можно быстро делиться с клиентом.

Чтобы увидеть любые активные развертывания, связанные с приложениями, размещенными в Azure, выполните следующие действия.

### <a name="action"></a>Действие

Чтобы просмотреть текущие развертывания в конвейере, выполните следующие действия:

1. Перейдите к **Службе приложений**.
2. Выберите нужное приложение из списка.
3. В разделе **Развертывание** в области служб приложений выберите **Центр развертывания**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Чтобы просмотреть свои приложения в Службе приложений, перейдите на [портал Azure](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Подробнее

Ниже приведены дополнительные статьи, которые помогут создать конвейеры развертывания.

- [Create your first pipeline](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2) (Создание первого конвейера)
- [GitHub Release task](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops) (Задача выпуска GitHub)
