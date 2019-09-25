---
title: Улучшите начальное облако по управлению Cloud Foundation
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как постепенно улучшать начальную облачную систему управления.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d7e4c0516e1c52f1fc6ddd8b42485902cb24d58e
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223641"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Улучшите начальное облако по управлению Cloud Foundation

В этой статье предполагается, что вы создали [начальную облачную](./initial-foundation.md)систему управления. По мере реализации плана внедрения в облако реальные риски выйдут из предложенных подходов, по которым группы хотят принять облако. Как и в случае с этими рисками в обсуждениях по планированию выпуска, используйте следующую сетку, чтобы быстро найти несколько рекомендаций по началу работы с планом внедрения, чтобы предотвратить реальные угрозы.

## <a name="maturity-vectors"></a>Векторы зрелости

В любое время можно применить следующие нормативные рекомендации к первоначальному руководству по управлению, чтобы устранить риск или необходимость упомянутых в таблице ниже.

> [!IMPORTANT]
> Организация ресурсов может повлиять на то, как применяется это нормативное руководство. Важно начать с рекомендаций, которые лучше согласованы с первоначальной облачной средой управления, реализованной на предыдущем шаге.

|Риск/потребность | Стандартное предприятие | Сложное предприятие |
|---|---|---|
|Конфиденциальные данные в облаке|[Нормативные руководства](./guides/standard/security-baseline-improvement.md)|[Нормативные руководства](./guides/complex/security-baseline-improvement.md)|
|Критически важные приложения в облаке|[Нормативные руководства](./guides/standard/resource-consistency-improvement.md)|[Нормативные руководства](./guides/complex/resource-consistency-improvement.md)|
|Управление затратами на облако|[Нормативные руководства](./guides/standard/cost-management-improvement.md)|[Нормативные руководства](./guides/complex/cost-management-improvement.md)|
|Многооблачная среда|[Нормативные руководства](./guides/standard/multicloud-improvement.md)|[Нормативные руководства](./guides/complex/multicloud-improvement.md)|
|Комплексное или устаревшее управление удостоверениями|Н/Д|[Нормативные руководства](./guides/complex/identity-baseline-improvement.md)|
|Использование нескольких уровней управления|Н/Д|[Нормативные руководства](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Следующие шаги

В дополнение к применению нормативных руководств методология управления в облачной инфраструктуре внедрения может быть настроена в соответствии с уникальными бизнес-ограничениями. После соблюдения соответствующих рекомендаций [оцените корпоративную политику, чтобы понять дополнительные требования к настройке](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Оценка корпоративной политики](./corporate-policy.md)
