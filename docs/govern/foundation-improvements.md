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
ms.openlocfilehash: 315797d7ef4ab93d5d386ee32a499f4172752687
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2019
ms.locfileid: "74159925"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Улучшите начальное облако по управлению Cloud Foundation

В этой статье предполагается, что вы создали [начальную облачную](./initial-foundation.md)систему управления. По мере реализации плана внедрения в облако реальные риски выйдут из предложенных подходов, по которым группы хотят принять облако. Как и в случае с этими рисками в обсуждениях по планированию выпуска, используйте следующую сетку, чтобы быстро найти несколько рекомендаций по подготовке плана внедрения к предотвращению реальных угроз.

## <a name="maturity-vectors"></a>Векторы зрелости

В любое время можно применить приведенные ниже рекомендации к первоначальному управлению, чтобы устранить риск или необходимость упомянутых в таблице ниже.

> [!IMPORTANT]
> Организация ресурсов может повлиять на применение этих рекомендаций. Важно начать с рекомендаций, которые лучше согласованы с первоначальной облачной средой управления, реализованной на предыдущем шаге.

|Риск/потребность | Стандартное предприятие | Сложное предприятие |
|---|---|---|
|Конфиденциальные данные в облаке|[Улучшение дисциплины](./guides/standard/security-baseline-improvement.md)|[Улучшение дисциплины](./guides/complex/security-baseline-improvement.md)|
|Критически важные приложения в облаке|[Улучшение дисциплины](./guides/standard/resource-consistency-improvement.md)|[Улучшение дисциплины](./guides/complex/resource-consistency-improvement.md)|
|Управление затратами на облако|[Улучшение дисциплины](./guides/standard/cost-management-improvement.md)|[Улучшение дисциплины](./guides/complex/cost-management-improvement.md)|
|Многооблачная среда|[Улучшение дисциплины](./guides/standard/multicloud-improvement.md)|[Улучшение дисциплины](./guides/complex/multicloud-improvement.md)|
|Комплексное или устаревшее управление удостоверениями|Н/Д|[Улучшение дисциплины](./guides/complex/identity-baseline-improvement.md)|
|Использование нескольких уровней управления|Н/Д|[Улучшение дисциплины](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Дальнейшие действия

Помимо применения рекомендаций, методологию управления в облачной инфраструктуре внедрения можно настроить в соответствии с уникальными бизнес-ограничениями. После соблюдения соответствующих рекомендаций [оцените корпоративную политику, чтобы понять дополнительные требования к настройке](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Оценка корпоративной политики](./corporate-policy.md)
