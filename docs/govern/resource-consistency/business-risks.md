---
title: Мотивации и бизнес-риски согласованности ресурсов
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Мотивации и бизнес-риски согласованности ресурсов
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fd1eb5d9425b87d17613507d3955126ce1437edd
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222020"
---
# <a name="resource-consistency-motivations-and-business-risks"></a>Мотивации и бизнес-риски согласованности ресурсов

В этой статье рассматриваются причины применения клиентами дисциплины "Согласованность ресурсов" в рамках стратегии управления облаком. Здесь также приводятся несколько примеров потенциальных бизнес-рисков, которые могут управлять правилами политики.

<!-- markdownlint-disable MD026 -->

## <a name="resource-consistency-relevancy"></a>Релевантность для согласованности ресурсов

Когда речь идет о развертывании ресурсов и рабочих нагрузок, облако обеспечивает повышенную гибкость и динамичность в большинстве традиционных локальных центров обработки данных. Но эти потенциальные преимущества облака также сопряжены с потенциальными недостатками управления, которые могут поставить под угрозу успешное внедрение облака. Какие ресурсы вы развернули? Какие ресурсы принадлежат определенным командам? Достаточно ли у вас ресурсов, поддерживающих рабочую нагрузку? Как узнать о работоспособности рабочих нагрузок?

Согласованность ресурсов крайне важна для того, чтобы гарантировать, что ресурсы развертываются, обновляются и настраиваются постоянно, и что перерывы в работе службы сведены к минимуму и исправлено как можно меньшее время.

Дисциплина "Согласованность ресурсов" отвечает за определение и устранение бизнес-рисков, связанных с эксплуатационными аспектами вашего облачного развертывания. Согласованность ресурсов включает мониторинг приложений, рабочих нагрузок и производительности ресурсов. Она также включает задачи, необходимые для удовлетворения требований масштабирования, обеспечения возможности аварийного восстановления, устранения нарушений Соглашение об уровне обслуживания производительности (SLA) и упреждающего предотвращения этих нарушений соглашений об уровне обслуживания с помощью автоматического исправления.

Для начальных тестовых развертываний может потребоваться только внедрение вводных стандартов именования и присвоения тегов для поддержки ваших потребностей согласованности ресурсов. В ходе внедрения облака и развертывания более сложных и критически важных ресурсов быстро возрастает необходимость инвестировать средства в дисциплину "Согласованность ресурсов".

## <a name="business-risk"></a>Бизнес-риск

Дисциплина "Согласованность ресурсов" направлена на устранение основных операционных бизнес-рисков. Работайте с вашим бизнесом и ИТ-специалистами, чтобы определить эти риски, а также отслеживать каждый из них для релевантности при планировании и осуществлении облачных развертываний.

Риски могут различаться в разных организациях, но ниже перечислены распространенные риски, которые можно использовать в качестве отправной точки для обсуждения в группе управления Cloud.

- **Ненужные эксплуатационные расходы.** Устаревшие или неиспользуемые ресурсы или ресурсы, избыточно подготовленные в периоды низкой загрузки, добавляют ненужные эксплуатационные расходы.
- **Ресурсы, подготове к работе.** Если ресурсов меньше, чем ожидалось, это может вызвать нарушение бизнес-процессов, так как облачные ресурсы перегружаются по запросу.
- **Эффективность управления.** Отсутствие согласованного именования и добавления тегов к метаданным, связанного с ресурсами, может усложнить ИТ-специалистам поиск необходимых ресурсов для выполнения задач управления или определения владения и данных учета, относящихся к ресурсам. Это приводит к снижению эффективности управления, что может увеличить расходы и снизить скорость реагирования ИТ-отдела на перебои в работе службы или другие проблемы с работоспособностью.
- **Прерывание бизнеса.** Перебои в работе службы, которые приводят к нарушениям условий установленного Соглашения об уровне обслуживания вашей организации, может повлечь за собой потерю бизнеса или другие финансовые последствия для вашей компании.

## <a name="next-steps"></a>Следующие шаги

С помощью [шаблона управления облачными](./template.md)службами Задокументируйте бизнес-риски, которые, скорее всего, будут представлены текущим планом внедрения в облако.

Как только реальный бизнес-риск обнаружен, необходимо задокументировать допустимость бизнес-риска, индикаторы и основные метрики для мониторинга этой допустимости.

> [!div class="nextstepaction"]
> [Общие сведения о метриках, индикаторах и допустимости риска](./metrics-tolerance.md)