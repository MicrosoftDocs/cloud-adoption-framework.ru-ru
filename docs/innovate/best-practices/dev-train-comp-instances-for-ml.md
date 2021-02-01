---
title: Определение экземпляров для разработки, обучения и вычислений для модели машинного обучения
description: При определении экземпляров для разработки, обучения и вычислений для модели машинного обучения следует рассмотреть используемый алгоритм, тип данных, размеры данных и способ выполнения распределенного обучения.
author: SudhandKumar
ms.author: kumarsud
ms.date: 01/20/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: think-tank
ms.openlocfilehash: 8addb89d7cbfde12bf41dde07c8bb1124efe8c50
ms.sourcegitcommit: 9cd2b48fbfee229edc778f8c5deaf2dc39dfe2d6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2021
ms.locfileid: "99230585"
---
# <a name="determine-development-training-and-compute-instances-for-your-machine-learning-model"></a>Определение экземпляров для разработки, обучения и вычислений для модели машинного обучения

При определении экземпляров для разработки, обучения и вычислений для модели машинного обучения рассмотрите используемый алгоритм, тип данных, размеры данных и, если вы выполните распределенное обучение.

## <a name="development-and-training-for-your-machine-learning-model"></a>Разработка и обучение модели машинного обучения

Ознакомьтесь со следующей схемой, чтобы ознакомиться с разработкой и обучением модели машинного обучения.

[![Схема разработки и обучения.](./media/dev-and-training.png)](./media/dev-and-training.png#lightbox)

## <a name="compute-instances-for-your-machine-learning-model"></a>Вычисление экземпляров для модели машинного обучения

На следующей схеме можно выбрать вычисление экземпляров, которые помогут модели машинного обучения запустить вывод:

[![Схема, показывающая вывод.](./media/inference.png)](./media/inference.png#lightbox)

## <a name="next-steps"></a>Дальнейшие действия

- [Создание вычислительного экземпляра и управление им](/azure/machine-learning/how-to-create-manage-compute-instance) в рабочей области машинное обучение Azure для более подробного понимания процесса.

- Ознакомьтесь со сведениями о [целевых объектах вычислений в машинное обучение Azure](/azure/machine-learning/concept-compute-target) , чтобы узнать, как эти среды могут помочь в обучении и развертывании модели во время жизненного цикла разработки.
