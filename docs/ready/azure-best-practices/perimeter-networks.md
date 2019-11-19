---
title: Сети периметра
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Сети периметра
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 08e2998e6e9f561189562f65b463aa1e0ffbe5b4
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160506"
---
# <a name="perimeter-networks"></a>Сети периметра

[Сети периметра][perimeter-network] обеспечивают безопасное подключение между облачными сетями и локальными или физическими сетями центра обработки данных, а также двухстороннюю связь с Интернетом. Они также известны как демилитаризованные зоны (DMZ).

Чтобы сети периметра эффективно работали, перед достижением внутренних серверов входящие пакеты должны проходить через устройства безопасности, размещенные в защищенных подсетях. Примерами являются брандмауэр, системы обнаружения вторжений (идентификаторы) и системы предотвращения вторжений (IP-адреса). Пакеты, направленные в Интернет рабочими нагрузками, также должны пройти через защитные устройства сети периметра перед выходом из сети. Это удобно для применения политик, выполнения проверок и аудита.

Сети периметра используют следующие функции и службы Azure:

- [Виртуальные сети][virtual-networks], [определяемые пользователем маршруты][user-defined-routes] и [группы безопасности сети][network-security-groups].
- [Сетевые виртуальные устройства (NVA)][NVA]
- [Подсистема балансировщика нагрузки Azure][ALB]
- [Шлюз приложений Azure][AppGW] и [брандмауэр веб-приложения (WAF)][AppGWWAF]
- [Общедоступные IP-адреса][PIP].
- [Azure Front Door][AFD] с [брандмауэром веб-приложения][AFDWAF].
- [Брандмауэр Azure][AzFW]

> [!NOTE]
> Эталонные архитектуры Azure содержат примеры шаблонов, которые можно использовать для реализации собственных сетей периметра:
>
> - [Реализация сети периметра между Azure и локальным центром обработки данных](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid).
> - [Реализация сети периметра между Azure и Интернетом](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json).

Как правило, основные ИТ-группы и группы безопасности отвечают за определение требований к работе с сетями периметра.

![Пример топологии сети концентратора и звезды][7]

На предыдущей схеме показан пример [топологии сети концентратора и звезды](./hub-spoke-network-topology.md) , которая реализует принудительное применение двух периметров с доступом к Интернету и локальной сети. Оба периметра располагаются в концентраторе DMZ. В концентраторе DMZ сеть периметра с доступом в Интернет можно масштабировать для поддержки большого количества бизнес-приложений (LOB) с помощью нескольких ферм WAF и экземпляров Брандмауэра Azure, которые обеспечивают защиту периферийных виртуальных сетей. Концентратор также обеспечивает подключение через VPN или Azure ExpressRoute при необходимости.

## <a name="virtual-networks"></a>Виртуальные сети

Обычно сети периметра создаются с помощью [виртуальной сети][virtual-networks] с несколькими подсетями для размещения другого типа служб, выполняющих фильтрацию и анализ трафика в Интернет и обратно через NVA, WAF и экземпляры Шлюзов приложения Azure.

## <a name="user-defined-routes"></a>Пользовательские маршруты

С помощью [определяемых пользователем маршрутов][user-defined-routes] клиенты могут развертывать брандмауэры, IDS или IPS и другие виртуальные устройства, а также направлять сетевой трафик через эти устройства безопасности. Это позволяет применять, контролировать и проверять политики границ безопасности. Определяемые пользователем маршруты можно создать, чтобы обеспечить передачу трафика через указанные пользовательские виртуальные машины, NVA и подсистемы балансировки нагрузки.

В примере с центральным и периферийным сетями, гарантируя, что трафик, создаваемый виртуальными машинами, расположенными на периферийном сервере, проходит через правильные виртуальные устройства в концентраторе, требуется определенный пользователем маршрут, определенный в подсетях периферийной зоны. Этот маршрут создает интерфейсный IP-адрес для внутренней подсистемы балансировки нагрузки в качестве следующего прыжка. Внутренняя подсистема балансировки нагрузки распределяет внутренний трафик на виртуальные устройства (внутренний пул подсистемы балансировки нагрузки).

## <a name="azure-firewall"></a>Брандмауэр Azure

[Брандмауэр Azure][AzFW] — это управляемая облачная служба, которая защищает ресурсы виртуальной сети Azure. Это управляемый брандмауэр с полным отслеживанием состояния и неограниченными возможностями облачного масштабирования. Вы можете централизованно создавать, применять и регистрировать политики приложений и сетевых подключений в подписках и виртуальных сетях.

Брандмауэр Azure использует статический общедоступный IP-адрес для ресурсов виртуальной сети. Он разрешает внешним брандмауэрам идентифицировать трафик, поступающий из вашей виртуальной сети. Служба взаимодействует с Azure Monitor для ведения журналов и аналитики.

## <a name="network-virtual-appliances"></a>Виртуальные сетевые модули

Сеть периметра с доступом в Интернет обычно управляется с помощью экземпляра Брандмауэра Azure, фермы брандмауэров или [брандмауэров веб-приложений][AFDWAF].

Разные бизнес-приложения обычно используют многие веб-приложения, которые, как правило, являются уязвимыми. Брандмауэр веб-приложений обнаруживает атаки, направленные на веб-приложения (HTTP и HTTPS). Это отличает их от обычных брандмауэров. По сравнению с традиционной технологией брандмауэра WAF содержит набор специальных функций для защиты внутренних веб-серверов от угроз.

Экземпляр Брандмауэра Azure и брандмауэр [виртуального сетевого модуля][NVA] используют общую панель администрирования с набором правил безопасности для защиты рабочих нагрузок, размещенных в периферийных зонах, а также управления доступом к локальным сетям. Брандмауэр Azure является масштабируемым решением, тогда как брандмауэры NVA можно масштабировать вручную за подсистемой балансировки нагрузки.

Как правило, программное обеспечение фермы брандмауэра менее специализированное по сравнению с ПО WAF, но включает более широкую область для фильтрации и проверки любого типа трафика (входящего и исходящего). Если вы используете брандмауэры NVA, вы можете найти и развернуть программное обеспечение из Azure Marketplace.

Используйте один набор экземпляров Брандмауэра Azure (или NVA) для трафика, поступающего из Интернета, и другой набор — для трафика, создаваемого локальными системами. Использование только одного набора брандмауэров в обоих случаях представляет угрозу безопасности, так как между двумя наборами сетевого трафика отсутствует периметр безопасности. Использование отдельных уровней брандмауэра упрощает проверку правил безопасности, а также помогает понять, какие правила соответствуют определенным входящим сетевым запросам.

## <a name="azure-load-balancer"></a>Подсистема балансировщика нагрузки Azure

[Azure Load Balancer][ALB] обеспечивает высокий уровень доступности (уровень 4) (TCP, UDP), который может распределять входящий трафик между экземплярами службы, определенными в наборе балансировки нагрузки. Трафик, отправленный в подсистему балансировки нагрузки из интерфейсных конечных точек (конечных точек общедоступного или частного IP-адреса), может распространяться с преобразованием адреса и без него в пул внутренних IP-адресов (таких как NVA или виртуальных машин).

Azure Load Balancer может также проверять работоспособность различных экземпляров сервера. Если экземпляр не отвечает на проверку, подсистема балансировки нагрузки останавливает отправку трафика в неработоспособный экземпляр.

В качестве примера использования топологии сети HUB и звезды можно развернуть внешнюю подсистему балансировки нагрузки как в концентраторе, так и на периферийных. В концентраторе подсистема балансировки нагрузки эффективно направляет трафик на службы в периферийных зонах. В периферийных зонах подсистемы балансировки нагрузки управляют трафиком приложений.

## <a name="azure-front-door-service"></a>Служба Azure Front Door

[Azure Front Door][AFD] — это высокодоступная и масштабируемая платформа от Майкрософт для ускорения веб-приложений и глобальная подсистема балансировки нагрузки HTTPS. С помощью Azure Front Door Service можно создавать, использовать и масштабировать динамические веб-приложения и статическое содержимое. Она выполняется более чем в 100 расположениях на границе глобальной сети Майкрософт.

Azure Front Door Service предоставляет вашему приложению единую автоматизацию регионального/маркированного обслуживания, автоматизацию BCDR, унифицированную клиентскую/пользовательскую информацию, кэширование и полезные сведения об услугах. Платформа обеспечивает производительность, надежность и поддержку соглашения об уровне обслуживания. Она также предлагает сертификаты соответствия и проверенные способы обеспечения безопасности, разработанные, реализуемые и поддерживаемые платформой Azure.

## <a name="application-gateway"></a>Шлюз приложений

[Шлюз приложений Azure][AppGW] является выделенным виртуальным устройством, которое предоставляет управляемый контроллер доставки приложений (ADC). Он предлагает различные возможности подсистемы балансировки нагрузки уровня 7 для вашего приложения.

Шлюз приложений позволяет оптимизировать производительность веб-фермы за счет выполнения операции завершения SSL-запросов, требующей интенсивного использования ЦП, на шлюзе приложений. Кроме того, пользователи получают другие возможности маршрутизации уровня 7, включая распределение входящего трафика методом циклического перебора, соответствие сеансу на основе файлов cookie, маршрутизацию на основе URL-путей и возможность размещения нескольких веб-сайтов за одним шлюзом приложений.

Номер SKU для WAF шлюза приложений включает брандмауэр веб-приложения. Этот SKU обеспечивает защиту веб-приложений от распространенных веб-уязвимостей и эксплойтов. Шлюз приложений можно настроить как шлюз с доступом в Интернет, внутренний шлюз или же как сочетание этих вариантов.

## <a name="public-ips"></a>Общедоступные IP-адреса.

Некоторые функции Azure позволяют связывать конечные точки службы с [общедоступным IP-адресом][PIP] для получения доступа к ресурсам из Интернета. Эта конечная точка использует преобразование сетевых адресов (NAT) для маршрутизации трафика на внутренний адрес и порт в виртуальной сети Azure. Это основной путь передачи внешнего трафика в виртуальную сеть. Общедоступные IP-адреса можно настроить, чтобы определить, какой трафик следует пропускать в виртуальную сеть, а также как и где его следует пропускать.

## <a name="azure-ddos-protection-standard"></a>Защита от атак DDoS Azure уровня "Стандартный"

[Защита от атак DDoS Azure уровня "Стандартный"][DDoS] предоставляет дополнительные возможности по устранению рисков по сравнению с уровнем [службы "Базовый"][DDoS], которые разработаны для ресурсов виртуальной сети Azure. Службу "Защита от атак DDoS" уровня "Стандартный" легко включить, и для ее использования не нужно изменять приложение.

Политики защиты можно настроить на основе мониторинга выделенного трафика и алгоритмов машинного обучения. Они применяются к общедоступным IP-адресам, связанным с ресурсами, развернутыми в виртуальных сетях, такими как Azure Load Balancer, Шлюз приложений Azure и экземпляры Azure Service Fabric.

Данные телеметрии доступны в представлениях Azure Monitor в режиме реального времени во время атаки и для статистических целей. Вы можете добавить защиту на прикладном уровне, используя брандмауэр веб-приложения в Шлюзе приложений Azure. Защита обеспечивается для общедоступных IP-адресов Azure IPv4.

<!-- images -->

[0]: ../../_images/azure-best-practices/network-redundant-equipment.png "Примеры перекрытия компонента"
[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Подробный пример звездообразной топологии"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Кластер концентраторов и периферийных зон"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Связь между периферийными зонами"
[4]: ../../_images/azure-best-practices/network-hub-spoke-block-level-diagram.png "Схема звездообразной топологии на уровне блоков"
[5]: ../../_images/azure-best-practices/network-users-groups-subscriptions.png "Пользователи, группы, подписки и проекты"
[6]: ../../_images/azure-best-practices/network-infrastructure-high-level.png "Высокоуровневая схема инфраструктуры"
[7]: ../../_images/azure-best-practices/network-high-level-perimeter-networks.png "Высокоуровневая схема инфраструктуры"
[8]: ../../_images/azure-best-practices/network-vnet-peering-perimeter-networks.png "Пиринг виртуальных сетей и сети периметра"
[9]: ../../_images/azure-best-practices/network-high-level-diagram-monitoring.png "Общая схема для мониторинга"
[10]: ../../_images/azure-best-practices/network-high-level-workloads.png "Схема высокого уровня для рабочих нагрузок"

<!-- links -->

[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[virtual-networks]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
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
[SubMgmt]: https://docs.microsoft.com/azure/architecture/cloud-adoption/reference/azure-scaffold
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[perimeter-network]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[AppGWWAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
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
