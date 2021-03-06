---
title: Общие сведения о сценарии внедрения современных контейнеров
description: Описание сценария
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 1a9cb60e3579589c0d6c6399da0dd7c3f656ebbe
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101793119"
---
# <a name="introduction-to-the-modern-containers-adoption-scenario"></a>Общие сведения о сценарии внедрения современных контейнеров

По мере использования более значительных и продуманных форм внедрения облачных технологий переход клиентов в облачную среду усложняется. В этой серии статей содержатся технические и нетехнические замечания, необходимые для подготовки к интеграции Kubernetes и контейнеров в облачную стратегию.

В этом сценарии основное внимание уделяется двум конечным результатам.

- **Контейнерные решения.** Контейнеры формируют уровень абстракции между техническими ресурсами и базовой инфраструктурой. Организации включают контейнеры в свои общие стратегии для снижения зависимости от поставщиков и повышения переносимости рабочих нагрузок.
- **Управление контейнерами в Kubernetes.** Kubernetes предоставляет панель для развертывания контейнерных приложений и управления ими, для управления плотностью вычислительными ресурсами и описания потребности в высоком уровне доступности для рабочих нагрузок.

В этой серии статей объясняется, как интегрировать контейнеры и процесс управления ими в имеющуюся стратегию организации, а также как внедрять контейнеры и работать с ними в облаке.

## <a name="components-of-the-scenario"></a>Компоненты сценария

Этот сценарий предназначен для реализации полного пути взаимодействия пользователя в рамках всего жизненного цикла перехода в облачную среду. Для завершения перехода требуется несколько важных наборов руководств.

- **Cloud Adoption Framework.** В этих статьях рассматривается минимум особенностей и реализаций каждой методики CAF. Сведения в этих статьях буду полезны для подготовки лиц, ответственных за принятие решений, сотрудников центрального ИТ-отдела и облачного центра инноваций к реализации основной части технологической стратегии — внедрению контейнеров и управлению ими.
- **Платформа Azure с продуманной архитектурой.** В этих статьях описываются моменты, которые должен учитывать каждый владелец рабочей нагрузки при развертывании рабочих нагрузок с использованием контейнеров или решений по управлению контейнерами, таких как Kubernetes.
- Эталонные архитектуры. Эти эталонные решения помогают ускорить развертывание контейнерных решений с использованием Azure Kubernetes Service (AKS).
- **Популярные продукты Azure.** Узнайте больше о продуктах, которые поддерживают ваши контейнеры и стратегию управления контейнерами в Azure.
- **Модули Microsoft Learn.** Получите практические навыки, необходимые для внедрения, обслуживания и поддержки решений для контейнеров и AKS.

## <a name="common-customer-journeys"></a>Распространенные сценарии клиентов

**Эталонные архитектуры AKS.** Приведенные на левой панели эталонные архитектуры демонстрируют развертывание различных проверенных архитектур для управления платформами контейнеров и Kubernetes с помощью службы Azure Kubernetes Service (AKS). Эти архитектуры являются предлагаемой отправной точкой для Kubernetes в Azure.

**Миграция существующих рабочих нагрузок в AKS.** Распространенным вариантом использования AKS в Azure является перенос существующих рабочих нагрузок на основе веб-технологий напрямую в контейнерное или облачное решение, а не выполнение традиционных действий по миграции. В статье о [переносе в контейнеры](./migrate.md) содержатся сведения о том, как Миграция Azure может ускорить перенос в контейнеры в рамках стандартных процессов миграции.

**Стандартизация развертывания контейнеров и управления ими.** В первом наборе статей на левой панели приводятся подробные инструкции по централизации стратегии использования контейнеров. Эта серия статей предназначена для того, чтобы помочь сотрудникам центрального ИТ-отдела и командам облачного центра инноваций понять влияние контейнеров на облачную стратегию и узнать, как обеспечить согласованную централизованную поддержку.

**Подготовка к использованию контейнеров и управлению ими в большом масштабе.** Набор конструирования корпоративного масштаба показывает, как можно использовать корпоративные целевые зоны для обеспечения согласованного управления, безопасности и эксплуатации в нескольких целевых зонах для масштабного и централизованного управления контейнерами.

**Реализация конкретных продуктов Azure.** Ускоряйте и улучшайте возможности контейнера и Kubernetes, используя различные виды продуктов Azure, описанных в разделе популярных продуктов.

## <a name="next-step-integrate-modern-containers-into-your-cloud-adoption-journey"></a>Следующий шаг. Интеграция современных контейнеров в план внедрения облачных технологий

В приведенном ниже списке статей приводятся полезные рекомендации по конкретным вопросам в процессе внедрения облачных технологий.

- [Стратегия для современных контейнеров](./strategy.md)
- [Планирование для современных контейнеров](./plan.md)
- [Проверка среды или целевых зон Azure](./ready.md)
- [Перенос рабочих нагрузок в современные контейнеры](./migrate.md)
- [Внедрение инноваций с помощью решений для современных контейнеров](/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
- [Управление решениями для современных контейнеров](./govern.md)
- [Управление решениями для современных контейнеров](./manage.md)
