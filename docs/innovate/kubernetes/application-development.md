---
title: Разработка и развертывание приложений
description: Узнайте об использовании Kubernetes в облачной инфраструктуре внедрения для разработки и архитектуры приложений.
author: sabbour
ms.author: asabbour
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5ebf8106cee793e674070e88c8c4f36e77858079
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2020
ms.locfileid: "89604238"
---
<!-- cSpell:ignore autoscaler Istio Linkerd -->

# <a name="application-development-and-deployment"></a>Разработка и развертывание приложений

Изучите шаблоны и методики разработки приложений, настройте Azure Pipelines и реализуйте рекомендации по проектированию надежности сайта (выполняются).

## <a name="plan-train-and-proof"></a>Планирование, обучение и подтверждение

По мере того как вы приступите к работе, контрольный список и приведенные ниже ресурсы помогут вам спланировать разработку и развертывание приложений. Вы должны иметь возможность ответить на следующие вопросы:

> [!div class="checklist"]
>
> - Вы подготовили среду разработки и рабочий процесс настройки?
> - Как вы будете структурировать папку проекта для поддержки разработки приложений Kubernetes?
> - Определены ли требования к состоянию, конфигурации и хранению приложения?

<!-- docutune:casing "AAD Pod Identity" -->

> [!div class="tdCol2BreakAll"]
>
> | Контрольный список | Ресурсы |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Подготовьте среду разработки.** Настройте среду с помощью средств, необходимых для создания контейнеров и настройки рабочего процесса разработки. | [Работа с DOCKER в Visual Studio Code](https://code.visualstudio.com/docs/azure/docker) <br> [Работа с Kubernetes в Visual Studio Code](https://code.visualstudio.com/docs/azure/kubernetes) <br> [Введение в Azure Dev Spaces](/azure/dev-spaces/about) |
> | **Контейнеризовать приложение.** Ознакомьтесь с комплексными возможностями разработки Kubernetes, включая формирование шаблонов приложений, рабочие процессы внутреннего цикла, платформы управления приложениями, конвейеры CI/CD, объединение журналов, мониторинг и метрики приложений. | [Контейнеризовать приложения с помощью DOCKER и Kubernetes (электронная книга)](https://azure.microsoft.com/resources/containerize-your-apps-with-docker-and-kubernetes) <br> [Комплексный опыт разработки Kubernetes в Azure (веб-семинар)](https://info.microsoft.com/AU-AzureApp-WBNR-FY20-11Nov-12-ContainerizeYourApplicationswithKubernetesonAzure-SRDEM10557_LP02OnDemandRegistration-ForminBody.html) |
> | **Ознакомьтесь с общими сценариями Kubernetes.** Kubernetes часто рассматривается как платформа для доставки микрослужб, но она становится намного более широкой платформой. Просмотрите это видео, чтобы узнать о стандартных сценариях Kubernetes, таких как пакетная аналитика и рабочий процесс.    | [Распространенные &nbsp; сценарии &nbsp; &nbsp; использования &nbsp; Kubernetes &nbsp; (видео)](https://www.youtube.com/watch?v=zd8vYhrFXp4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=7) |
> | **Подготовьте приложение к Kubernetes.** Подготовьте структуру файловой системы приложения для Kubernetes и упорядочите ее для еженедельных или ежедневных выпусков. Узнайте, как процесс развертывания Kubernetes обеспечивает надежное обновление без простоя. | [Проектирование и макет проекта для успешных приложений Kubernetes (веб-семинар)](https://info.microsoft.com/ww-OnDemandRegistration-successful-kubernetes-applications-webinar.html) <br> [Как работают развертывания Kubernetes (видео)](https://www.youtube.com/watch?v=mNK14yXIZF4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=3) <br> [Пройдите по AKS семинару](https://aka.ms/learn/aksworkshop) |
> | **Управление хранилищем приложений.** Изучите требования к производительности и методы доступа для модулей Pod, чтобы предоставить соответствующие варианты хранения. Также следует продумать методы резервного копирования и протестировать процессы восстановления для подключенного хранилища. | [Основные сведения о приложениях с отслеживанием состояния в Kubernetes (видео)](https://www.youtube.com/watch?v=GieXzb91I40&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=9) <br> [Состояние и данные в приложениях Docker](/dotnet/architecture/microservices/architect-microservice-container-applications/docker-application-state-data) <br> [Варианты хранения в службе Kubernetes Azure](/azure/aks/operator-best-practices-storage) |
> | **Управление секретами приложения.** Не храните учетные данные в коде приложения. Хранилище ключей должно использоваться для хранения и извлечения ключей и учетных данных.  | [Как работает управление Kubernetes и конфигурацией (видео)](https://www.youtube.com/watch?v=vRcQOZLnKUk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=11) <br> [Общие сведения об управлении секретами в Kubernetes (видео)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) <br> [Использование Azure Key Vault с Kubernetes](https://github.com/azure/kubernetes-keyvault-flexvol) <br> [Использование удостоверения Pod Azure AD для проверки подлинности и доступа к ресурсам Azure](https://github.com/azure/aad-pod-identity) |

## <a name="deploy-to-production-and-apply-best-practices"></a>Развертывание в рабочей среде и применение рекомендаций

При подготовке приложения для рабочей среды следует реализовать минимальный набор рекомендаций. На этом этапе используйте контрольный список. Вы должны иметь возможность ответить на следующие вопросы:

> [!div class="checklist"]
>
> - Можно ли отслеживать все аспекты приложения?
> - Определены ли требования к ресурсам для вашего приложения? Как насчет требований к масштабированию?
> - Можно ли развертывать новые версии приложения, не затрагивая рабочие системы?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Контрольный список  | Ресурсы                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Настройка проверки готовности и текущих проверок работоспособности.** Kubernetes использует проверки готовности и динамичности, чтобы выяснить, когда приложение готово к получению трафика и когда его необходимо перезапустить. Не определяя такие проверки, Kubernetes не сможет определить, работает ли приложение. | [Актуальность и проверки готовности](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes) |
> | **Настройка ведения журналов, мониторинга приложений и предупреждений.** Мониторинг контейнеров крайне важен, особенно если вы управляете рабочим кластером в нужном масштабе с несколькими приложениями. Рекомендуемый метод ведения журнала для контейнерных приложений — это запись в потоки стандартных выходных данных (stdout) и стандартных ошибок (stderr). | [Вход в Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging) <br> [Приступая к работе с мониторингом и оповещениями для Kubernetes (видео)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br> [Azure Monitor для контейнеров](/azure/azure-monitor/insights/container-insights-overview) <br> [Enable and review Kubernetes master node logs in Azure Kubernetes Service (AKS)](/azure/aks/view-master-logs) (Включение и просмотр журналов главного узла Kubernetes в Службе Azure Kubernetes (AKS)) <br> [Просмотр журналов Kubernetes, событий и метрик Pod в режиме реального времени](/azure/azure-monitor/insights/container-insights-livedata-overview) |
> | **Определите требования к ресурсам для приложения.** Основным способом управления ресурсами вычислений в кластере Kubernetes является использование запросов и ограничений Pod. Эти запросы и ограничения сообщают планировщику Kubernetes, какие ресурсы вычислений должен назначить Pod. | [Определение &nbsp; &nbsp; &nbsp; запросов &nbsp; и ограничений ресурсов &nbsp; Pod](/azure/aks/developer-best-practices-resource-management) |
> | **Настройте требования к масштабированию приложений.** Kubernetes поддерживает горизонтальное автомасштабирование pod для изменения числа pod в развертывании в зависимости от использования ЦП или других выбранных метрик. Чтобы использовать Автомасштабирование, все контейнеры в модулях Pod должны иметь определенные запросы ЦП и ограничения. | [Настройка горизонтального автомасштабирования Pod](/azure/aks/tutorial-kubernetes-scale#autoscale-pods) |
> | **Развертывание приложений с помощью автоматизированного конвейера и DevOps.** Полная автоматизация всех шагов между фиксацией кода и развертыванием в рабочей среде позволяет группам сосредоточиться на построении кода и устранять издержки и потенциальную ошибку человека в ручных повседневных шагах. Развертывание нового кода происходит быстрее и менее рискованно, что способствует повышению гибкости команд, повышение производительности и более уверенности в работе кода. | [Развитие практик DevOps](/learn/paths/evolve-your-devops-practices) <br> [Настройка конвейера сборки Kubernetes (видео)](https://www.youtube.com/watch?v=5irsAdKoEBU&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=6) <br> [Центр развертывания для службы Kubernetes Azure](/azure/aks/deployment-center-launcher) <br> [Действия GitHub для развертывания в службе Kubernetes Azure](/azure/aks/kubernetes-action) <br> [НЕПРЕРЫВная интеграция и развертывание в службу Kubernetes Azure с помощью Jenkins](/azure/aks/jenkins-continuous-deployment) |

## <a name="optimize-and-scale"></a>Оптимизация и масштабирование

Теперь, когда приложение находится в рабочей среде, как можно оптимизировать рабочий процесс и подготовить приложение и команду к масштабированию? Для подготовки используйте контрольный список для оптимизации и масштабирования. Вы должны иметь возможность ответить на следующие вопросы:

> [!div class="checklist"]
>
> - Существуют ли перекрестные задачи приложения, абстрактные от вашего приложения?
> - Вы можете поддерживать надежность системы и приложений, а также выполнять итерацию по новым возможностям и версиям?

<!-- docutune:casing Consul -->

> [!div class="tdCol2BreakAll"]
>
> | Контрольный список  | Ресурсы                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Развертывание шлюза API.** Шлюз API выступает в качестве точки входа в микрослужбы, отделяет клиентов от микрослужб, добавляет дополнительный уровень безопасности и сокращает сложность микрослужб за счет устранения проблем, связанных с обработкой перекрестных задач.     | [Использование службы управления API Azure с микрослужбами, развернутыми в службе Kubernetes Azure](/azure/api-management/api-management-kubernetes) |
> | **Развертывание сетки службы.** Сетка служб предоставляет такие возможности, как управление трафиком, устойчивость, политика, безопасность, надежный идентификатор и наблюдаемость рабочих нагрузок. Приложение отделено от этих операционных возможностей, и сетка служб перемещает их из уровня приложения и на уровень инфраструктуры. | [Как &nbsp; &nbsp; работают сети служб &nbsp; &nbsp; в &nbsp; Kubernetes &nbsp; (видео)](https://www.youtube.com/watch?v=izVWk7rYqWI&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=15&t=0s) <br> [Дополнительные сведения о сетчатых службах](/azure/aks/servicemesh-about) <br> [Использование Istio со службой Kubernetes Azure](/azure/aks/servicemesh-istio-about) <br> [Использование Linkerd со службой Kubernetes Azure](/azure/aks/servicemesh-linkerd-about) <br> [Использование Consul со службой Kubernetes Azure](/azure/aks/servicemesh-consul-about) |
> | **Реализуйте рекомендации по проектированию надежности сайта (выполняются).** Технология обеспечения надежности сайта (выполняются) — это проверенный подход к обеспечению важной надежности системы и приложений при итерации по скорости, требуемой Marketplace.   | [Введение в проектирование надежности сайта (выполняются)](/learn/modules/intro-to-site-reliability-engineering) <br> [DevOps в Майкрософт: потоковая передача игр выполняются](https://azure.microsoft.com/resources/devops-at-microsoft-game-streaming-sre) |
