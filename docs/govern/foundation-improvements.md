---
title: Улучшите начальное облако по управлению Cloud Foundation
description: Используйте платформу внедрения облачных технологий для Azure, чтобы узнать, как постепенно усовершенствовать начальную облачную инфраструктуру управления.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2b8de6fb4979621b70857a3cfd3dc0cec9e9f7f7
ms.sourcegitcommit: 12fa4597633ca8e04efbae7d0bd7526d3581618e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "88661985"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Улучшите начальное облако по управлению Cloud Foundation

В этой статье предполагается, что вы создали [начальную облачную](./initial-foundation.md)систему управления. По мере реализации плана внедрения в облако реальные риски выйдут из предложенных подходов, по которым группы хотят принять облако. Как и в случае с этими рисками в обсуждениях по планированию выпуска, используйте следующую сетку, чтобы быстро найти несколько рекомендаций по подготовке плана внедрения к предотвращению реальных угроз.

## <a name="maturity-vectors"></a>Векторы зрелости

В любое время можно применить приведенные ниже рекомендации к первоначальному управлению, чтобы устранить риск или необходимость упомянутых в таблице ниже.

> [!IMPORTANT]
> Организация ресурсов может повлиять на применение этих рекомендаций. Важно начать с рекомендаций, которые лучше согласованы с первоначальной облачной средой управления, реализованной на предыдущем шаге.

| Риск/потребность | Стандартное предприятие | Сложное предприятие |
|---|---|---|
| Конфиденциальные данные в облаке | [Оптимизация аспектов](./guides/standard/security-baseline-improvement.md) | [Оптимизация аспектов](./guides/complex/security-baseline-improvement.md) |
| Критически важные приложения в облаке | [Оптимизация аспектов](./guides/standard/resource-consistency-improvement.md) | [Оптимизация аспектов](./guides/complex/resource-consistency-improvement.md) |
| Управление затратами на облако | [Оптимизация аспектов](./guides/standard/cost-management-improvement.md) | [Оптимизация аспектов](./guides/complex/cost-management-improvement.md) |
| Многооблачная среда | [Оптимизация аспектов](./guides/standard/multicloud-improvement.md) | [Оптимизация аспектов](./guides/complex/multicloud-improvement.md) |
| Комплексное или устаревшее управление удостоверениями | н/д | [Оптимизация аспектов](./guides/complex/identity-baseline-improvement.md) |
| Использование нескольких уровней управления | н/д | [Оптимизация аспектов](./guides/complex/multiple-layers-of-governance.md) |

## <a name="next-steps"></a>Дальнейшие действия

Помимо применения рекомендаций, управление методологией облачной инфраструктуры внедрения можно настроить в соответствии с уникальными бизнес-ограничениями. После соблюдения соответствующих рекомендаций [оцените корпоративную политику, чтобы понять дополнительные требования к настройке](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Оценка корпоративной политики](./corporate-policy.md)
