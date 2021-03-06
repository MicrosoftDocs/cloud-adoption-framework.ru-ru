---
title: Мотивация и бизнес-риски в дисциплине ускорения развертывания
description: Используйте инфраструктуру внедрения в облаке для Azure, чтобы понять бизнес-риски по дисциплине ускорения развертывания, которые можно использовать в стратегии управления.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: 76707cd3f67fe5dc3f6a78002b8fcecf07285b27
ms.sourcegitcommit: b6f2b4f8db6c3b1157299ece1f044cff56895919
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97021667"
---
# <a name="motivations-and-business-risks-in-the-deployment-acceleration-discipline"></a>Мотивация и бизнес-риски в дисциплине ускорения развертывания

В этой статье рассматриваются причины применения клиентами дисциплины "Ускорение развертывания" в рамках стратегии управления облаком. Здесь также приводится несколько примеров бизнес-рисков, которые могут привести в действие правила политики.

## <a name="relevance"></a>релевантности

Локальные системы часто развертываются с помощью базовых образов или сценариев установки. Обычно требуется дополнительная настройка, что может включать несколько шагов или вмешательство пользователя. Эти выполняемые вручную процессы подвержены ошибкам и часто приводят к "отклонениям конфигурации", требующим выполнение задач по устранению неполадок и исправлению, занимающих много времени.

Большинство ресурсов Azure можно развернуть и настроить вручную на портале Azure. Этого подхода может быть достаточно для ваших потребностей, если вам необходимо управлять всего несколькими ресурсами. По мере роста облачных ресурсов Организация должна приступить к интеграции автоматизации в процессы развертывания, чтобы гарантировать, что облачные ресурсы будут предотвращать отклонение конфигурации или другие проблемы, возникающие в ручных процессах. Применение подхода DevOps или [девсекопс](https://www.microsoft.com/devsecops) часто является лучшим способом управления развертываниями по мере того, как облачные решения по внедрению будут приняты.

Надежный план ускорения развертывания гарантирует, что облачные ресурсы развертываются, обновляются и настраиваются правильно и остаются в таком виде. Зрелость стратегии ускорения развертывания также может играть значительную роль в вашей [стратегии управления затратами](../cost-management/index.md). Автоматическая подготовка и настройка облачных ресурсов позволяет уменьшить масштаб или освободить ресурсы, если потребность в них низкая или привязана ко времени. Таким образом вы платите за ресурсы по мере необходимости.

## <a name="business-risk"></a>Бизнес-риск

Дисциплина ускорения развертывания направлена на устранение следующих бизнес-рисков. Во время внедрения облака отслеживайте состояние каждого из следующих значений на релевантность:

- **Прерывание работы службы:** Отсутствие предсказуемых процессов развертывания или неуправляемых изменений конфигураций системы может привести к нарушению нормальной работы, а также к потере производительности или потере бизнеса.
- **Превышение затрат:** Непредвиденные изменения в конфигурации системных ресурсов могут сделать более сложным определение основной причины проблем, повышая затраты на разработку, эксплуатацию и обслуживание.
- **Неэффективные Организации:** Барьеры между разработкой, эксплуатацией и группами безопасности могут привести к многочисленным проблемам при эффективном внедрении облачных технологий и разработке единой модели управления облаком.

## <a name="next-steps"></a>Дальнейшие действия

Используйте [шаблон "дисциплина ускорения развертывания](./template.md) " для документирования бизнес-рисков, которые, скорее всего, будут представлены текущим планом внедрения в облако.

Как только реальный бизнес-риск обнаружен, необходимо задокументировать допустимость бизнес-риска, индикаторы и основные метрики для мониторинга этой допустимости.

> [!div class="nextstepaction"]
> [Метрики, индикаторы и допустимость риска](./metrics-tolerance.md)
