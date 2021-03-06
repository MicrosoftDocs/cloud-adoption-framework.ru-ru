---
title: Планирование проверки трафика
description: Изучите ключевые вопросы проектирования и рекомендации, касающиеся зеркального отображения или касания трафика в виртуальной сети Azure.
author: JefferyMitchell
ms.author: brblanch
ms.date: 02/18/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: dba15dab8463e7708c7f9bf0e45080417886393e
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799098"
---
# <a name="plan-for-traffic-inspection"></a>Планирование проверки трафика

Во многих отраслях организация требует, чтобы трафик в Azure был зеркально отражен в сборщик сетевых пакетов для глубокой проверки и анализа. Это требование обычно посвящено входящему и исходящему интернет – трафику. В этом разделе рассматриваются ключевые моменты и Рекомендуемые подходы к зеркальному отображению или касанию трафика в виртуальной сети Azure.

**Рекомендации по проектированию:**

<!-- docutune:ignore TAP -->

- [Точка доступа к терминалу виртуальной сети Azure (TAP)](/azure/virtual-network/virtual-network-tap-overview) находится на этапе предварительной версии. Обратитесь к `azurevnettap@microsoft.com` сведениям о доступности.

- Запись пакетов в наблюдатель за сетями Azure доступна в общедоступной версии, но количество записей ограничено максимальным сроком пять часов.

**Рекомендации по проектированию:**

В качестве альтернативы отводам виртуальной сети Azure следует оценить следующие параметры.

- Используйте пакеты наблюдателя за сетями для захвата, несмотря на ограниченное окно записи.

- Оцените, что последняя версия журналов потоков NSG предоставляет необходимый уровень детализации.

- Используйте решения партнеров для сценариев, требующих глубокой проверки пакетов.

- Не Разрабатывайте пользовательское решение для зеркального отображения трафика. Хотя этот подход может быть приемлемым для небольших сценариев, мы не рекомендуем его масштабировать из-за сложности и проблем, связанных с поддержкой, которые могут возникнуть.
