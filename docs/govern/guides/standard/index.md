---
title: Руководство по организации системы управления для стандартных предприятий
description: На примере вымышленного стандартного предприятия изучите различные этапы развития системы управления, необходимые для создания минимально жизнеспособного продукта (MVP) на основе рекомендаций.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: 3975c2f9f4e849cdf996a4b83448e0a6e5c3d871
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102112659"
---
# <a name="standard-enterprise-governance-guide"></a>Руководство по организации системы управления для стандартных предприятий

## <a name="overview-of-best-practices"></a>Обзор рекомендаций

Руководство по организации системы управления построено на примере вымышленной компании на различных этапах развития системы управления. Сведения основаны на реальных сценариях взаимодействия с клиентом. Рекомендации основаны на ограничениях и потребностях вымышленной компании.

Чтобы предоставить вам быструю отправную точку, в этом обзоре определен минимально жизнеспособный продукт (MVP) системы управления, основанный на рекомендациях. Здесь также содержатся ссылки на данные об улучшении системы управления, которые позволяют получить рекомендации по мере возникновения новых бизнес-рисков или технических рисков.

> [!WARNING]
> Этот MVP — это базовая начальная точка, для которой учитываются определенные допущения. Даже этот минимальный набор рекомендаций основывается на корпоративных политиках, созданных с учетом уникальных бизнес-рисков и допустимых рисков. Чтобы понять, применимы ли эти допущения к вам, ознакомьтесь с [подробным описанием](./narrative.md), которое следует за этой статьей.

### <a name="governance-best-practices"></a>Рекомендации по реализации системы управления

Эти рекомендации помогут организациям быстро и согласованно добавлять в подписки Azure средства защиты, предлагаемые системой управления.

### <a name="resource-organization"></a>Организация ресурсов

В примере ниже показана иерархия MVP системы управления для организации ресурсов.

![Схема организации ресурсов](../../../_images/govern/resource-organization.png)

Каждое приложение необходимо развернуть в соответствующей области иерархии группы управления, подписки и группы ресурсов. Во время планирования развертывания команда по управлению облачными решениями создаст в иерархии необходимые узлы для работы команд по внедрению облачных решений.

1. Группа управления для каждого типа среды (например, рабочая среда, среда разработки и тестирования).
2. Две подписки: для рабочей и нерабочей рабочих нагрузок.
3. На каждом уровне иерархии группирования должна применяться [согласованная номенклатура](../../../ready/azure-best-practices/naming-and-tagging.md).
4. Группы ресурсов следует развертывать способом, который учитывает особенности жизненного цикла ее содержимого: развертывание активов, управление ими и прекращение использования должно осуществляться в комплексе. Дополнительные сведения о рекомендациях по группам ресурсов см. в [руководстве по принятию решений для согласования ресурсов](../../../decision-guides/resource-consistency/index.md).
5. Очень важно [выбрать правильный регион](../../../migrate/azure-best-practices/multiple-regions.md). Мы рекомендуем выбирать регион так, чтобы вы имели доступ к сетевым ресурсам, средствам мониторинга и аудита в процессе отработки отказа или восстановления размещения, а также чтобы [нужные SKU были доступны в предпочтительных регионах](https://azure.microsoft.com/global-infrastructure/services/).

Ниже приведен пример использования этого шаблона:

![Пример организации ресурсов в компании среднего размера](../../../_images/govern/mid-market-resource-organization.png)

Эти шаблоны предоставляют пространство для роста без лишних усложнений иерархии.

[!INCLUDE [governance-of-resources](../../../../includes/governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Итеративное улучшение системы управления

После развертывания MVP в среду можно быстро интегрировать дополнительные уровни управления. Ниже описаны некоторые способы улучшения MVP в соответствии с потребностями конкретной организации:

- [Базовые средства безопасности для защиты данных](./security-baseline-improvement.md)
- [Настройки ресурсов для критически важных приложений](./resource-consistency-improvement.md)
- [Элементы управления для Управления затратами](./cost-management-improvement.md)
- [Элементы управления для развития возможностей работы с несколькими облаками](./multicloud-improvement.md)

## <a name="what-does-this-guidance-provide"></a>Что предоставляет это руководство?

В MVP устанавливаются рекомендации и средства дисциплины [ускорения развертывания](../../deployment-acceleration/index.md), которые позволяют быстро применять корпоративную политику. В частности MVP использует Azure Blueprints, Политику Azure и группы управления Azure для применения нескольких основных корпоративных политик, как определено в описании этой вымышленной компании. Эти корпоративные политики применяются с использованием шаблонов Resource Manager и политик Azure для определения основных минимальных показателей идентификации и безопасности.

![Схема с примером минимально жизнеспособного продукта для системы управления инкрементальной модели.](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Поэтапное улучшение методик управления

Со временем MVP системы управления будет использоваться для усовершенствования рекомендаций по ее организации. По мере внедрения растут риски для бизнеса. Для снижения этих рисков мы будем вносить изменения в разные аспекты моделей системы управления Cloud Adoption Framework. В более поздних статьях этой серии рассматривается добавочное улучшение корпоративной политики, влияющей на вымышленную компанию. Это улучшение осуществляется в трех различных дисциплинах:

- "Управление затратами" по мере масштабирования внедрения.
- "Базовые средства безопасности" по мере развертывания защищенных данных.
- "Согласованность ресурсов" по мере поддержки критически важных рабочих нагрузок отделом ИТ-операций.

![Схема с примером поэтапного улучшения методик управления.](../../../_images/govern/governance-improvement.png)

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы знакомы с минимально жизнеспособным продуктом для системы управления и имеете представление об улучшении системы управления, ознакомьтесь с контекстуальными сведениями в дополнительной статье.

> [!div class="nextstepaction"]
> [Читать вспомогательное описание](./narrative.md)
