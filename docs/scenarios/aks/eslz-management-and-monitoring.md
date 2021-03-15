---
title: Управление и мониторинг масштаба предприятия для AKS
description: Опишите, как этот сценарий корпоративного уровня может улучшить управление и мониторинг AKS
author: BrianBlanchard
ms.author: pidebrui
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ca2e137dec3c9b2e0874003c617f783fb1e8b046
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101798708"
---
# <a name="management-and-monitoring-for-aks-enterprise-scale-scenario"></a>Управление и мониторинг для сценария AKS корпоративного уровня

Kubernetes — это относительно некоторая технология, быстро развивающаяся и имеющая впечатляющие экосистемы. Это может быть проблемой управления. Правильно разрабатывая решение с учетом управления и мониторинга, вы можете работать в оперативном и успешном направлении.

## <a name="design-considerations"></a>Рекомендации по проектированию

Примите во внимание следующие факторы.

- Учитывайте [ограничения AKS](/azure/aks/quotas-skus-regions). Используйте несколько экземпляров AKS для масштабирования за пределами этих ограничений.
- Помните о способах изоляции рабочих нагрузок логически в кластере и физически в отдельных кластерах.
- Учитывайте способы управления потреблением ресурсов рабочими нагрузками.
- Помните о способах, которые помогут Kubernetes понять работоспособность рабочих нагрузок.
- Помните о различных размерах виртуальных машин и влиянии использования одного или другого. Более крупные виртуальные машины могут справиться с нагрузкой. Более мелкие виртуальные машины можно легко заменить другими, если они недоступны для запланированного и незапланированного обслуживания. Также необходимо учитывать концепцию пулов узлов, виртуальных машин в масштабируемом наборе, которые позволяют создавать виртуальные машины разного размера в одном кластере.
- Учитывайте способы мониторинга и ведения журнала AKS. Kubernetes состоит из различных компонентов, а мониторинг и ведение журнала должны обеспечивать понимание его работоспособности, тенденций, а также потенциальных проблем.
- Сборка на основе мониторинга и ведения журнала может создавать много событий, создаваемых Kubernetes или приложениями, выполняемыми в верхней части. Оповещения позволяют различать записи журнала для исторических целей и те, которые нуждаются в немедленных действиях.
- Помните о обновлениях и обновлениях, которые следует выполнить. На уровне Kubernetes есть основной, дополнительный номер версии и версия исправления. Клиент должен применить эти обновления, чтобы остаться в поддерживаемом состоянии в соответствии с политикой в вышестоящем Kubernetes. В исправлениях ядра операционной системы на уровне рабочего узла может потребоваться перезагрузка, которую должен выполнить клиент, а также обновления до новых версий ОС.
- Учитывайте ограничения ресурсов кластера, а также отдельных рабочих нагрузок.
- Следите за использованием рекомендаций.
- Узнайте о вариантах управления несколькими кластерами с помощью Azure, а также сертифицированных кластеров Kubernetes за пределами Azure.

## <a name="design-recommendations"></a>Рекомендации по проектированию

- Общие сведения об ограничениях AKS:
  - [Квоты и региональные ограничения](/azure/aks/quotas-skus-regions)
  - [Ограничения службы AKS](/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-kubernetes-service-limits)
- Используйте логическую изоляцию на уровне пространства имен, чтобы разделить приложения, группы, среды и подразделения. [Мультитенантность и изоляция кластеров](/azure/aks/operator-best-practices-cluster-isolation). Кроме того, пулы узлов могут помочь узлам с различными спецификациями узлов, а обслуживание, например Kubernetes, обновляет [несколько пулов узлов](/azure/aks/use-multiple-node-pools) .
- Спланируйте и примените квоты ресурсов на уровне пространства имен. Если pod не определяют запросы ресурсов и ограничения, отклоните развертывание. Наблюдайте за использованием ресурсов и при необходимости изменяйте квоты. [Основные возможности планировщика](/azure/aks/operator-best-practices-scheduler)
- Добавьте пробы работоспособности в службы. Убедитесь, что модули Pod содержат `livenessProbe` , `readinessProbe` и `startupProbe` [AKS проверки работоспособности](/azure/application-gateway/ingress-controller-add-health-probes).
- Используйте размеры виртуальных машин, достаточные для хранения нескольких экземпляров контейнеров, чтобы получить преимущества повышенной плотности, но не настолько большой, что кластер не может справиться с рабочей нагрузкой сбойного узла.
- Используйте решение для мониторинга. [Azure Monitor для контейнеров](/azure/azure-monitor/containers/container-insights-overview) настраивается по умолчанию и обеспечивает простой доступ к многим ценным сведениям. Вы можете использовать [интеграцию Prometheus](/azure/azure-monitor/containers/container-insights-prometheus-integration) , если вы хотите детализировать углублением или получить опыт использования Prometheus. Если вы также хотите запустить приложение мониторинга на AKS, следует также использовать Azure Monitor для мониторинга этого приложения.
- Используйте систему предупреждений для предоставления уведомлений о необходимости прямого действия. [Оповещения на основе метрик](/azure/azure-monitor/containers/container-insights-metric-alerts)
- Используйте [автоматическую функцию масштабирования пула узлов](/azure/aks/cluster-autoscaler) вместе с [горизонтальным автомасштабированием Pod](/azure/aks/concepts-scale#horizontal-pod-autoscaler) , чтобы удовлетворить требования приложений и снизить нагрузку на часы пиковой нагрузки.
- Используйте помощник по Azure для получения рекомендаций по стоимости, безопасности, надежности, эффективной работе и производительности. Кроме того, используйте [Центр безопасности Azure](/azure/security-center/defender-for-kubernetes-introduction) для предотвращения и обнаружения угроз, таких как уязвимости образов.
- Используйте Kubernetes с поддержкой [дуги Azure](/azure/azure-arc/kubernetes/overview) для управления кластерами AKS Kubernetes в Azure с помощью политики Azure, центра безопасности, гитопс и т. д.