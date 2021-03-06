---
title: Управляйте портфелем в гибридных и многооблачных операциях
description: Реализуйте эффективные элементы управления, чтобы обеспечить управление операциями в гибридных и многооблачных развертываниях с помощью плоскости управления предприятием Azure.
author: brianblanchard
ms.author: brblanch
ms.date: 02/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: e2e-hybrid
ms.openlocfilehash: bc9912d7226b204e34c6944585ab3b2a73c4ff12
ms.sourcegitcommit: c167c45b66cc7324b60c88b8b7aac439f956b65d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2021
ms.locfileid: "102208529"
---
# <a name="manage-your-portfolio-across-hybrid-and-multicloud-operations"></a>Управляйте портфелем в гибридных и многооблачных операциях

Использование гибридной и облачной сред приводит к естественным сдвигам работы в облаке. [Методология управления](../../manage/index.md) в облачной инфраструктуре внедрения для Azure описывает путь для реализации базовых показателей операций и разработки этих базовых показателей на протяжении всего жизненного цикла внедрения в облако. Расширение стратегии для развертывания гибридных, многооблачных и пограничных развертываний требует смены способа реализации надлежащего управления операциями. [Единые операции](./unified-operations.md) — это лучшая концепция для решения этих требований по сдвигу.

В следующем разделе показано, как можно применить концепцию Объединенных операций и реализовать рекомендации по обеспечению эффективной гибридной, многооблачной и пограничной операций.

## <a name="extend-your-operations-baseline"></a>Расширение базовых показателей операций

Служба " [дуга Azure](/azure/azure-arc/overview) " уменьшает сложность и стоимость расширения базовых показателей операций. Развертывание дуги Azure в центре обработки данных, гибридном облаке и в нескольких облачных средах расширяет собственные функции Azure, которые включены в Azure Resource Manager.

Чтобы начать работу с базовым планом операций, охватывающим локальные и несколько облачных поставщиков, выполните упражнения по инвентаризации и разметки. Это упражнение приступит к расширению базовых показателей операций за несколько этапов:

- Добавьте тег для `hosting platform` всех гибридных, многооблачных и краевых ресурсов.
- Пометьте ресурсы в AWS, обеспечить и т. д.
- Запросите ресурсы, чтобы узнать, где они размещены.

Чтобы приступить к работе, проведите [инвентаризацию и пометьте гибридные и многооблачные ресурсы](../../manage/hybrid/server/best-practices/arc-inventory-tagging.md).

<!-- docutune:casing "update management guide" -->

После завершения упражнения можно приступить к работе с гибридной и многооблачной средой. Как правило, первый шаг, выполняемый при расширении операций в облаках, заключается в *создании согласованного плана для управления обновлениями и исправлениями*. Для развертывания средств, которые могут управлять исправлениями для поставщиков облачных служб, следуйте инструкциям в [руководстве по управлению гибридными и многооблачными обновлениями](../../manage/hybrid/server/best-practices/arc-update-management.md).

## <a name="enhanced-baseline"></a>Улучшенный базовый план

Улучшите базовые показатели операций, применяя постоянно широкий спектр активов и поставщиков облачных услуг. В следующем списке приведено несколько примеров типов ресурсов, которые можно добавить в Расширенные базовые показатели операций:

- **Ресурсы Azure**: [виртуальные машины Linux](../../manage/hybrid/server/best-practices/arm-template-linux.md) и [виртуальные машины Windows](../../manage/hybrid/server/best-practices/arm-template-windows.md)
- **Ресурсы в локальном центре обработки данных**: [виртуальные машины Linux](../../manage/hybrid/server/best-practices/onboard-server-linux.md) и [виртуальные машины Windows](../../manage/hybrid/server/best-practices/onboard-server-windows.md)
- **Ресурсы VMware**: [виртуальные машины Linux](../../manage/hybrid/server/best-practices/vmware-scaled-powercli-linux.md) и [виртуальные машины Windows](../../manage/hybrid/server/best-practices/vmware-scaled-powercli-windows.md)
- **AWS активы**: [виртуальные машины Linux с terraform](../../manage/hybrid/server/best-practices/aws-terraform-al2.md) и [AWS Ubuntu с terraform](../../manage/hybrid/server/best-practices/aws-terraform-ubuntu.md)
- **Ресурсы обеспечить**: [виртуальные машины Ubuntu](../../manage/hybrid/server/best-practices/gcp-terraform-ubuntu.md) и [виртуальные машины Windows](../../manage/hybrid/server/best-practices/gcp-terraform-windows.md)

## <a name="operations-management-disciplines"></a>Дисциплины управления операциями

Наряду с разметкой и переносом ресурсов можно также предоставить множество дисциплин управления операциями с помощью гибридных и многооблачных средств.

Одним из примеров готовой дисциплины управления операциями является использование Microsoft Monitoring Agent для управления установкой программного обеспечения, антивирусной защитой или другими функциями управления конфигурацией. В следующих статьях описывается настройка агента мониторинга в гибридной и многооблачной среде.

- [Управление виртуальными машинами с помощью агента мониторинга](../../manage/hybrid/server/best-practices/arc-vm-extension-mma.md)
- [Масштабирование конфигурации агента мониторинга](../../manage/hybrid/server/best-practices/arc-vm-extension-custom-script.md)

## <a name="next-steps"></a>Дальнейшие действия

После завершения переноса Объединенных операций группа по внедрению в облако может начать следующую миграцию для конкретного сценария. Если вы хотите перенести больше платформ, используйте следующие статьи, чтобы помочь вам выполнить следующие операции по переносу или развертыванию Объединенных операций:

- [Стратегия для Объединенных операций](./strategy.md)
- [Планирование Объединенных операций](./plan.md)
- [Проверка среды или целевых зон Azure](./ready.md)
- [Гибридная и многооблачная миграция](./migrate.md)
- [Управление гибридными и многооблачными средами](./govern.md)
