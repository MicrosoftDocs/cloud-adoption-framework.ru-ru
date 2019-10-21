---
title: Звездообразная топология сети
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Звездообразная топология сети
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: fcbcda63ff080de234075f0a8784731e591ca0f3
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549007"
---
# <a name="hub-and-spoke-network-topology"></a>Звездообразная топология сети

*Звездообразная топология* — это сетевая модель для более эффективного управления общими требованиями к обмену данными или обеспечению безопасности. Она также позволяет избежать ограничений подписки Azure. В этой модели уделяется особое внимание следующим вопросам.

- **Сокращение затрат и повышение эффективности управления**. Централизация служб, которые могут совместно использоваться несколькими рабочими нагрузками, такими как сетевые виртуальные модули (NVA) и DNS-серверы, в одном расположении, что позволяет ИТ-отделу минимизировать избыток ресурсов и усилия по управлению.
- **Преодоление ограничения подписок**. Большим рабочим нагрузкам может потребоваться больше ресурсов, чем разрешено в рамках одной подписки Azure Пиринг рабочей нагрузки виртуальных сетей из различных подписок в центральный концентратор может преодолеть эти ограничения. Дополнительные сведения см. в разделе [ограничения подписки](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Четкое разделение зон ответственности**. Вы можете развертывать отдельные рабочие нагрузки между центральными ИТ-командами и командами по выполнению рабочих нагрузок.

Небольшие облачные инфраструктуры могут не воспользоваться преимуществами дополнительной структуры и возможностями, которые предлагает эта модель. Но в сценарии больших внедрений облачных технологий следует рассмотреть возможность применения сетевой звездообразной архитектуры, если у команд есть какие-либо вопросы, перечисленные ранее.

> [!NOTE]
> На сайте эталонных архитектур Azure содержатся примеры шаблонов, которые вы можете использовать в качестве основы для реализации собственных звездообразных сетей:
>
> - [Реализация звездообразной топологии сети в Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke).
> - [Реализация звездообразной топологии сети с помощью общих служб в Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services).

## <a name="overview"></a>Краткое описание

![Примеры звездообразной топологии сети][1].

Как показано на диаграмме, среда Azure поддерживает два типа звездообразного проектирования. Она поддерживает взаимодействие, общие ресурсы и централизованную политику безопасности (VNet Hub на диаграмме) или виртуальный тип WAN (Virtual WAN на диаграмме) для крупномасштабных взаимодействий типа "ветвь — ветвь" и "ветвь — Azure".

Центральная зона (концентратор) контролирует и проверяет входящий и исходящий трафик между зонами, включая Интернет, а также локальные периферийные зоны. Звездообразная топология позволяет ИТ-отделу применять политики безопасности в центральном расположении, одновременно минимизируя уязвимости и ошибки в конфигурации.

В концентраторе часто содержатся общие компоненты службы, используемые периферийными зонами. Их примеры представлены ниже.

- Инфраструктура Windows Server Active Directory для аутентификации внешних пользователей, которые пытаются получить доступ из ненадежных сетей, до предоставления таким пользователям доступа к рабочим нагрузкам в периферийных зонах. Сюда входят связанные службы федерации Active Directory (AD FS).
- Служба DNS для разрешения имен рабочих нагрузок в периферийных зонах и получения доступа к ресурсам локально и в Интернете, если [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) не используется.
- Инфраструктура открытых ключей (PKI) для реализации единого входа в рабочие нагрузки.
- Управление TCP- и UDP-трафиком между зонами периферийными зонами и Интернетом.
- Управление потоком между периферийными зонами и локальными ресурсами.
- Управление потоком между несколькими периферийными зонами (при необходимости).

Вы можете минимизировать избыточность, упростить управление и снизить общую стоимость, используя общую инфраструктуру концентратора для поддержки нескольких периферийных зон.

Роль каждой периферийной зоны может заключаться в размещении различных типов рабочих нагрузок. Использование периферийных зон также позволяют реализовать модульный подход для повторяемых развертываний одних и тех же рабочих нагрузок Примерами являются разработка и тестирование, приемочное тестирование пользователей, промежуточное и рабочее.

Также эти зоны можно использовать для разделения и включения различных групп в пределах организации, например, групп DevOps в Azure. В пределах периферийной зоны можно развернуть базовую рабочую нагрузку или сложные многоуровневые рабочие нагрузки с управлением трафиком между уровнями.

## <a name="subscription-limits-and-multiple-hubs"></a>Ограничения подписки и несколько центральных зон

В Azure каждый компонент (независимо от типа) развертывается в подписке Azure. Изоляция компонентов Azure в разных подписках Azure позволяет выполнять требования различных бизнес-приложений, например настройку дифференцированных уровней доступа и авторизации.

Единую звездообразную реализацию можно масштабировать для создания большого количества периферийных зон. Но, как и в случае с любой ИТ-системой, у этой платформы есть свои ограничения. Развертывание концентратора привязано к определенной подписке Azure, которая имеет ограничения, например максимальное количество пиринговых виртуальных сетей. Дополнительные сведения см. в статье [ограничения для подписки Azure и службы, квоты и ограничения] [limits].

В случаях, когда ограничения становятся проблемой, архитектуру можно далее масштабировать, расширяя отдельную звездообразную модель до звездообразного кластера. Вы можете связать несколько концентраторов в одном или нескольких регионах Azure с помощью пиринга между виртуальными сетями, подключения ExpressRoute Azure, виртуальной глобальной сети или VPN типа "сеть — сеть".

![Кластер концентраторов и периферийных зон][2]

Включение нескольких концентраторов приводит к увеличению затрат и накладных расходов на управление. Это может быть оправдано только требованиями масштабируемости (в соответствии с системными ограничениями или избыточностью) и региональной репликации (для обеспечения производительности или аварийного восстановления). В сценариях, требующих несколько концентраторов, все концентраторы должны обеспечивать один набор служб для упрощения выполнения операций.

## <a name="interconnection-between-spokes"></a>Взаимодействие между периферийными зонами

В пределах отдельной периферийной зоны можно реализовать сложные многоуровневые рабочие нагрузки. Вы можете реализовать многоуровневые конфигурации, используя подсети (по одной для каждого уровня) в одной виртуальной сети, а также используя группы безопасности сети для фильтрации потоков.

Архитектор может развернуть многоуровневую рабочую нагрузку в пределах нескольких виртуальных сетей. Используя пиринг между виртуальными сетями, периферийные зоны могут подключаться к другим периферийным зонам в пределах одного или нескольких концентраторов.

Типичным примером такого сценария является случай, когда серверы обработки приложения располагаются в одной периферийной зоне или виртуальной сети, а база данных развернута в другой периферийной зоне или виртуальной сети. В этом случае периферийные зоны могут легко обмениваться данными через пиринговые виртуальные сети, не используя при этом концентратор. Решение состоит в том, чтобы выполнить тщательную проверку архитектуры и безопасности, чтобы обход концентратора не обходит важные точки безопасности или аудита, которые могут существовать только в концентраторе.

![Периферийные зоны, соединяющиеся друг с другом и с концентратором][3]

Периферийные зоны могут также взаимодействовать с периферийной зоной, выполняющей функции концентратора. Такой подход создает двухуровневую иерархию: периферийная зона высокого уровня (уровень 0) становится концентратором подчиненных периферийных зон (уровень 1) иерархии. Периферийные зоны звездообразной реализации должны направлять трафик в концентратор, чтобы трафик мог проходить к своей цели в локальной сети либо в общедоступном Интернете. Такая архитектура концентратора представляет сложную маршрутизацию, что сводит на нет преимущества отдельной звездообразной связи.

<!-- images -->

[0]: ../../_images/azure-best-practices/network-redundant-equipment.png "Примеры перекрытия компонента"
[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Подробный пример звездообразной топологии"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Кластер концентраторов и периферийных зон"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Связь между периферийными зонами"
[4]: ../../_images/azure-best-practices/network-hub-spoke-block-level-diagram.png "Диаграмма концентратора и периферийной зоны уровня блока"
[5]: ../../_images/azure-best-practices/network-users-groups-subscriptions.png "Пользователи, группы, подписки и проекты"
[6]: ../../_images/azure-best-practices/network-infrastructure-high-level.png "Высокоуровневая схема инфраструктуры"
[7]: ../../_images/azure-best-practices/network-high-level-perimeter-networks.png "Высокоуровневая схема инфраструктуры"
[8]: ../../_images/azure-best-practices/network-vnet-peering-perimeter-networks.png "Пиринг между виртуальными сетями и сетями периметра"
[9]: ../../_images/azure-best-practices/network-high-level-diagram-monitoring.png "Общая схема для мониторинга"
[10]: ../../_images/azure-best-practices/network-high-level-workloads.png "Общая схема для рабочих нагрузок"

<!-- links -->

[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[azure-ad]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[vWAN]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[SubMgmt]: ../../reference/azure-scaffold.md
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[NPM]: https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
