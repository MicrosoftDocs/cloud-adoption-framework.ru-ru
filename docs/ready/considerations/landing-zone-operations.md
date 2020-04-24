---
title: Улучшение операций размещения в зонах
description: Улучшение операций размещения в зонах
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 7c3e7bb61ba6fde3ad2c236706673fbc7d195ef6
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2020
ms.locfileid: "81121809"
---
# <a name="improve-landing-zone-operations"></a>Улучшение операций размещения в зонах

Операции размещения зоны обеспечивают первоначальную основу для управления операциями. В качестве масштаба операций эти улучшения переоптимизируют целевые зоны, чтобы удовлетворить растущие эксплуатационные требования, надежность и производительность.

## <a name="landing-zone-operations-best-practices"></a>Рекомендации по операциям с главной зоной

Следующие ссылки содержат рекомендации по улучшению операций размещения в зонах.

- [Управление сервером Azure](../../manage/azure-server-management/index.md). Руководство по внедрению собственных средств и служб, необходимых для управления операциями в облаке.
- [Гибридный мониторинг](../../manage/monitor/index.md). Многие клиенты уже внесли значительный вклад в System Center Operations Manager. Для этих клиентов это руководством по гибридному мониторингу помогает им сравнивать и отменять облачные средства создания отчетов с помощью инструментов Operations Manager. Это сравнение упрощает выбор средств, используемых для операционного управления.
- [Централизованное управление операциями управления](../../manage/centralize-operations.md). Используйте Azure лигхсаусе для централизации управления операциями в нескольких клиентах Azure.
- [Создание проверки](../../manage/operational-fitness-review.md)готовности к работе: Проверка среды на предмет пригодности к эксплуатации.
- Рекомендации по операциям для конкретной рабочей нагрузки:
  - [Контрольный список для обеспечения устойчивости](https://docs.microsoft.com/azure/architecture/checklist/resiliency-per-service?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
  - [Анализ режима сбоя](https://docs.microsoft.com/azure/architecture/resiliency/failure-mode-analysis?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
  - [Восстановление после прерывания работы служб во всем регионе](https://docs.microsoft.com/azure/architecture/resiliency/recovery-loss-azure-region?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
  - [Восстановление данных после повреждения или случайного удаления](https://docs.microsoft.com/azure/architecture/framework/resiliency/data-management?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="four-steps-to-improve-operations-beyond-a-single-landing-zone"></a>Четыре шага для улучшения операций за пределами одной целевой зоны

[Методология управления](../../manage/index.md) предоставляет общие рекомендации по созданию емкости для управления операциями, описанной в разделе [Управление методологией](../../manage/index.md). Мы будем использовать базовую структуру этой методологии и следующие шаги из этой методологии, чтобы улучшить операции размещения и операции в каждой целевой зоне.

![Управление методологией](../../_images/manage/caf-manage.png)

1. [Создание базового плана управления](../../manage/azure-server-management/index.md). базовый уровень управления определяет основу для управления операциями. Рекомендации на первом шаге можно применить к любой целевой зоне, чтобы улучшить начальные операции.
2. [Определение бизнес-обязательств](../../manage/considerations/business-alignment.md). понимание важности и влияния каждой рабочей нагрузки в целевой зоне приведет к определению "завершено" для любых текущих улучшений управления для любой целевой зоны. Этот процесс также определит требования к надежности, производительности и эксплуатации каждой рабочей нагрузки.
3. [Развертывание базового плана управления](../../manage/best-practices.md). Этот набор рекомендаций можно применять для улучшения операций размещения в основной зоне за пределами исходного базового плана.
4. [Расширенные принципы эксплуатации и проектирования](../../manage/design-principles.md): Изучите проектирование и операции конкретных рабочих нагрузок, платформ или полных целевых зон для удовлетворения более глубоких требований.

## <a name="test-driven-development-cycle"></a>Цикл разработки на основе тестирования

Прежде чем приступить к улучшению безопасности, важно понять «определение завершенных» и все «условия приемки». Дополнительные сведения см. в статьях о [разработке целевых зон на основе тестирования](./test-driven-development.md) и [разработке на основе тестирования в Azure](./azure-test-driven-development.md).

![Процесс разработки на основе тестирования для облачных целевых зон](../../_images/ready/test-driven-development-process.png)

## <a name="next-steps"></a>Следующие шаги

Узнайте, как [улучшить управление главной зоной](./landing-zone-governance.md) для поддержки внедрения в масштабе.

> [!div class="nextstepaction"]
> [Улучшенное управление начальной зоной](./landing-zone-governance.md)
