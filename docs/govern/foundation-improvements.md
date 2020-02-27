---
title: Улучшите начальное облако по управлению Cloud Foundation
description: Используйте платформу внедрения облачных технологий для Azure, чтобы узнать, как постепенно усовершенствовать начальную облачную инфраструктуру управления.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 050d9cdfd2069a4d7da2e411233f6a60f270eb10
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706614"
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
|Комплексное или устаревшее управление удостоверениями|Недоступно|[Улучшение дисциплины](./guides/complex/identity-baseline-improvement.md)|
|Использование нескольких уровней управления|Недоступно|[Улучшение дисциплины](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Дальнейшие действия

Помимо применения рекомендаций, методологию управления в облачной инфраструктуре внедрения можно настроить в соответствии с уникальными бизнес-ограничениями. После соблюдения соответствующих рекомендаций [оцените корпоративную политику, чтобы понять дополнительные требования к настройке](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Оценка корпоративной политики](./corporate-policy.md)
