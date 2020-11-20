---
title: Повышение безопасности целевых зон
description: Улучшение безопасности зоны размещения.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8640ea8c6e9e346502382c329f506ab5b933b609
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/20/2020
ms.locfileid: "94997239"
---
# <a name="improve-landing-zone-security"></a>Повышение безопасности целевых зон

Если рабочей нагрузке или зонам размещения, на которых размещена эта система, требуется доступ к любым конфиденциальным данным или важным системам, важно защитить данные и ресурсы. Повышение безопасности узловой зоны основано на [подходе к разработке на основе тестирования для размещения зон](./test-driven-development.md) путем расширения или рефакторинга целевой зоны для учета повышенных требований к безопасности.

## <a name="landing-zone-security-best-practices"></a>Рекомендации по обеспечению безопасности зоны размещения

В следующем списке эталонных архитектур и рекомендаций приведены примеры способов улучшения безопасности зоны размещения.

- [Центр безопасности Azure](/azure/security-center/security-center-get-started?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json): подключение подписки к центру безопасности.
- [Azure Sentinel](/azure/sentinel/quickstart-onboard?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Подключите метку Azure, чтобы предоставить решение для **управления событиями сведений о безопасности (SIEM)** и **автоматизированного реагирования на системы безопасности (взлетел)** .
- [Безопасность границы сети](../../reference/networking-vdc.md): несколько шаблонов ссылок для разработки сети, аналогично тому, как граница сети защищена в центре обработки данных.
- [Архитектура защищенной сети](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json): Эталонная архитектура для реализации сети периметра и безопасной сетевой архитектуры.
- [Управление удостоверениями и доступом](/azure/security/fundamentals/identity-management-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). ряд рекомендаций по реализации удостоверений и доступа для защиты целевой зоны в Azure.
- [Рекомендации по сетевой безопасности](/azure/security/fundamentals/network-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). предоставляет дополнительные рекомендации по обеспечению безопасности сети.
- [Операционная безопасность](/azure/security/fundamentals/operational-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) предоставляет рекомендации по повышению эксплуатационной безопасности в Azure.
- [Основы безопасности](../../govern/guides/complex/security-baseline-improvement.md#incremental-improvement-of-best-practices): пример разработки базовых показателей безопасности, основанных на управлении, для соблюдения требований безопасности.

## <a name="test-driven-development-cycle"></a>Цикл разработки на основе тестирования

Прежде чем приступить к улучшению безопасности, важно понять «определение завершенных» и все «условия приемки». Дополнительные сведения см. в статьях о [разработке целевых зон на основе тестирования](./test-driven-development.md) и [разработке на основе тестирования в Azure](./azure-test-driven-development.md).

![Процесс разработки на основе тестирования для облачных целевых зон](../../_images/ready/test-driven-development-process.png)

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как [улучшить операции размещения зоны](./landing-zone-operations.md) для поддержки важных приложений.

> [!div class="nextstepaction"]
> [Оптимизация операций с целевыми зонами](./landing-zone-operations.md)
