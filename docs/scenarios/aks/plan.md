---
title: Планирование современных контейнеров
description: Описание влияния сценария на планирование
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 03e946b343661d76c7203dc1b26d93e8ff3729a6
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101797918"
---
# <a name="plan-for-modern-containers"></a>Планирование современных контейнеров

[Методология плана внедрения в облако](../../plan/index.md) помогает создать общий план внедрения в облако, который поможет программам и командам, вовлеченным в облачное цифровое преобразование. В этом руководстве содержатся шаблоны для создания невыполненной работы и планов по созданию необходимых навыков в группах в зависимости от того, что вы пытаетесь сделать в облаке.

Стандартная методика плана ориентирована на [пять RS рационализацию вашего цифрового пространства](../../digital-estate/5-rs-of-rationalization.md). (Слабо переведенные: наиболее распространенные пути к внедрению в облако.) В частности, эти планы адаптированы к наиболее распространенным сценариям: повторное размещение, перестроение и повторная разработка.

## <a name="initial-containers-considerations"></a>Рекомендации по первоначальным контейнерам

Упаковка рабочих нагрузок в контейнеры — это первый текст работы, который необходимо запланировать и обойти. Второй — планирование размещения этих контейнеров.

### <a name="containers-without-orchestration"></a>Контейнеры без оркестрации

Некоторые рабочие нагрузки являются строго автономными и не обязательно имеют преимущества дополнительных элементов управления и требований к инфраструктуре, которые поставляются с крупной платформой, такой как Kubernetes. Так как Рабочая нагрузка в контейнере не означает, что она должна быть развернута в Kubernetes. Azure предоставляет разнообразные решения для запуска рабочих нагрузок в портфеле, которые не требуют уровня управления и инфраструктуры, которые требуются AKS. Следующие решения применяют этот подход к планированию:

- [Служба приложений](/azure/app-service/)
- [Функции Azure](/azure/azure-functions/functions-overview)
- [Экземпляры контейнеров Azure](/azure/container-instances/container-instances-overview);
- [Пакетная служба](/azure/batch/batch-technical-overview)

Рассмотрите возможность использования более упрощенного решения для контейнеров для рабочих нагрузок, которые не предполагают роста сложности и согласованы с целями и ограничениями перечисленных выше решений.

### <a name="containers-with-orchestration"></a>Контейнеры с оркестрации

Для рабочих нагрузок, которые не могут работать на полностью управляемой платформе PaaS и должны ретранслироваться на элементы управления уровня инфраструктуры, нужно использовать расширенные функции развертывания, такие как предложения, предоставляемые оркестрации контейнеров, или превысить сложность модульной сложности, включив службу Azure Kubernetes Service (AKS). AKS решает оба размещения контейнеров, но также предоставляет широкие возможности архитектуры, выполняются, безопасности, развертывания, мониторинга и инфраструктуры.

Набор функций платформы имеет требование для изучения платформы как на уровне оператора кластера, так и на уровне рабочей нагрузки. Обработайте группы операций, группы архитектуры и рабочие группы разработчиков рабочих нагрузок в шкале времени миграции. Кроме того, поскольку AKS является платформой, следует убедиться в том, что группы рабочих нагрузок понимают разделение обязанностей на этой платформе и их текущее размещение. В некоторых случаях он может быть похожим, но, скорее всего, будет романским в других.

Для очень специализированных рабочих нагрузок или конкретных организационных требований Azure предлагает две другие основные платформы в пространстве оркестрации контейнера.

- Azure Red Hat OpenShift
- Azure Service Fabric

Если есть причины для изучения альтернатив, следует убедиться в том, что выделено время, чтобы понять преимущества и компромиссы всех параметров платформы. Решение Azure по умолчанию — AKS, и в этой документации предполагается, что AKS является выбранной технологией.

## <a name="digital-estate"></a>Цифровые активы

При планировании вашего цифрового пространства необходимо [собрать данные инвентаризации](../../digital-estate/inventory.md) и [рационально](../../digital-estate/rationalize.md)расставить свое место. В плане внедрения контейнеров все ресурсы, например виртуальные машины, данные и приложения, группируются по рабочей нагрузке, которую они поддерживают. После завершения группирования и базовой рационализации можно оценить эти рабочие нагрузки, чтобы определить параметры пакета, повторного размещения или реконструирования.

При оценке цифровых площадок необходимо также оценить план для данных на основе сохраняемости контейнера. Контейнеры могут работать в постоянном или непостоянном состоянии. Контейнеры постоянных состояний будут хранить данные в случае сбоя. Контейнеры, не являющиеся постоянными, не поддерживают данные. Если вы выбираете непостоянную конфигурацию, которая является общей для современных DevOps групп, вам потребуется учитывать размещение данных рабочих нагрузок в постоянной среде, например в базе данных SQL Azure.

Эти рекомендации помогут вам наглядно ознакомиться с действиями, необходимыми для завершения внедрения контейнерных рабочих нагрузок в облако.

## <a name="modern-container-adoption-plan"></a>Современный план внедрения контейнеров

Стандартные учетные записи [шаблона плана внедрения облака](../../plan/template.md) для типов работы, необходимых для типичных усилий по внедрению в облако. Но вам потребуется добавить в план задачи для упаковки рабочей нагрузки в контейнеры и согласование подготовки контейнеров.

## <a name="modern-container-readiness-plan"></a>План готовности современных контейнеров

Помимо плана подготовки к внедрению в облако, группам внедрения облака может потребоваться разработать навыки, связанные с контейнером и Kubernetes, перед выполнением плана:

- [Основные сведения о Kubernetes](https://aka.ms/LearnAKS)
- [Дополнительные сведения о контейнерах](https://azure.microsoft.com/product-categories/containers/)
- [Ознакомьтесь с рекомендациями по Kubernetes](https://aka.ms/aks/bestpractices)

Выделять время для групп рабочей нагрузки для документирования и выполнения планов миграции. Существующее приложение или внешняя система (зависимости и системы, зависящие от этой рабочей нагрузки) может потребоваться изменить с помощью дополнительной гибкости для поддержки усилий по миграции. Это справедливо и для подготовительных, и для рабочих сред.

## <a name="next-step-review-your-environment-or-azure-landing-zone"></a>Следующий шаг: Проверка среды или целевой зоны Azure

В приведенном ниже списке статей приводятся рекомендации в конкретных точках пути внедрения в облако, которые помогут вам успешно пройти в сценарии внедрения в облако.

- [Проверка среды или целевых зон Azure](./ready.md)
- [Перенос рабочих нагрузок в современные контейнеры](./migrate.md)
- [Внедрять новые решения на основе современных контейнеров](/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
- [Управление решениями современных контейнеров](./govern.md)
- [Управление решениями современных контейнеров](./manage.md)
- [См. раздел дерево решений для контейнеров и вычислений.](/azure/architecture/guide/technology-choices/compute-decision-tree)
