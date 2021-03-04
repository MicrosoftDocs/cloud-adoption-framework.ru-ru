---
title: Общие сведения о топологии сети и подключении
description: Изучите ключевые вопросы проектирования и практические рекомендации по работе с сетью и подключением к Microsoft Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/18/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: internal
ms.openlocfilehash: 06aa20a707b816ea0bd004131747b0dcac1cb832
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101788085"
---
<!-- docutune:casing "Azure VPN Gateway" L7 -->
<!-- cSpell:ignore autoregistration BGPs MACsec MPLS MSEE onprem privatelink VPNs -->

# <a name="network-topology-and-connectivity-overview"></a>Общие сведения о топологии сети и подключении

В этой серии статей рассматриваются ключевые вопросы проектирования и рекомендации по работе с сетью и подключением к Microsoft Azure.

## <a name="plan-for-ip-addressing"></a>Планирование IP-адресации

Важно, чтобы ваша организация запланировать IP-адресацию в Azure, чтобы пространство IP-адресов не перекрывались между локальными расположениями и регионами Azure.
[В этом разделе содержатся рекомендации по планированию IP-адресации для гибридной реализации.](../azure-best-practices/plan-for-ip-addressing.md)

## <a name="configure-dns-and-name-resolution-for-on-premises-and-azure-resources"></a>Настройка DNS и разрешения имен для локальных и ресурсов Azure

Служба доменных имен (DNS) является важнейшим разделом разработки в общей архитектуре корпоративного масштаба. Некоторым организациям может потребоваться использовать существующие вложения в DNS. Другие могут видеть внедрение облака как возможность модернизировать свою внутреннюю инфраструктуру DNS и использовать собственные возможности Azure.
[В этом разделе рассматриваются рекомендации по планированию DNS и разрешения имен для гибридных реализаций.](../azure-best-practices/dns-for-on-premises-and-azure-resources.md)

## <a name="define-an-azure-network-topology"></a>Определение топологии сети Azure

Топология сети является важнейшим элементом архитектуры корпоративного уровня, так как он определяет, как приложения могут взаимодействовать друг с другом. [В этом разделе рассматриваются технологии и подходы к топологии для развертываний Azure.](../azure-best-practices/define-an-azure-network-topology.md) Он посвящен двум основным подходам: топологии на основе виртуальной глобальной сети Azure и традиционных топологий.

## <a name="virtual-wan-network-topology"></a>Топология сети виртуальной глобальной сети

[В этом разделе рассматривается возможность реализации топологии сети виртуальной глобальной сети Azure.](../azure-best-practices/virtual-wan-network-topology.md)

## <a name="traditional-azure-networking-topology"></a>Традиционная топология сетей Azure

[В этом разделе рассматривается возможность реализации традиционной топологии сетей Azure.](../azure-best-practices/traditional-azure-networking-topology.md)

## <a name="connectivity-to-azure"></a>Подключение к Azure

[Этот раздел расширяет топологию сети, чтобы рассмотреть Рекомендуемые модели для подключения локальных расположений к Azure.](../azure-best-practices/connectivity-to-azure.md)

## <a name="private-link-and-dns-integration-at-scale"></a>Частная ссылка и интеграция DNS в масштабе

[В этом разделе описывается, как интегрировать частную связь Azure для служб PaaS с зонами Частная зона DNS Azure в архитектурах центральных и периферийных сетей.](../azure-best-practices/private-link-and-dns-integration-at-scale.md)

## <a name="connectivity-to-azure-paas-services"></a>Подключение к службам PaaS Azure

Основываясь на предыдущих разделах подключения, в [этом разделе рассматриваются рекомендуемые подходы к подключению для использования служб PaaS Azure.](../azure-best-practices/connectivity-to-azure-paas-services.md)

## <a name="plan-for-inbound-and-outbound-internet-connectivity"></a>Планирование входящего и исходящего подключения к Интернету

[В этом разделе описываются рекомендуемые модели подключения для входящего и исходящего подключения к общедоступному Интернету.](../azure-best-practices/plan-for-inbound-and-outbound-internet-connectivity.md)

## <a name="plan-for-application-delivery"></a>Планирование доставки приложений

[В этом разделе рассматриваются основные рекомендации по обеспечению безопасности, высокой масштабируемости и высокой доступности внешних приложений с внешними приложениями.](../azure-best-practices/plan-for-app-delivery.md)

## <a name="plan-for-landing-zone-network-segmentation"></a>Планирование сегментации сети для целевой зоны

[В этом разделе рассматриваются ключевые рекомендации по обеспечению высоконадежной сегментации внутренних сетей в целевой зоне для обеспечения реализации бесконечных сетей без доверия.](../azure-best-practices/plan-for-landing-zone-network-segmentation.md)

## <a name="define-network-encryption-requirements"></a>Определение требований к шифрованию сети

[В этом разделе рассматриваются основные рекомендации по обеспечению шифрования сети между локальной средой и Azure, а также между регионами Azure.](../azure-best-practices/define-network-encryption-requirements.md)

## <a name="plan-for-traffic-inspection"></a>Планирование проверки трафика

Во многих отраслях организация требует, чтобы трафик в Azure был зеркально отражен в сборщик сетевых пакетов для глубокой проверки и анализа. Это требование обычно посвящено входящему и исходящему интернет – трафику. [В этом разделе рассматриваются ключевые моменты и Рекомендуемые подходы к зеркальному отображению или касанию трафика в виртуальной сети Azure](../azure-best-practices/plan-for-traffic-inspection.md).

## <a name="connectivity-to-other-cloud-providers"></a>Подключение к другим поставщикам облачных служб

[В этом разделе приводятся различные подходы к соединению для интеграции архитектуры целевой зоны Azure корпоративного уровня с другими поставщиками облачных служб](../azure-best-practices/connectivity-to-other-cloud-providers.md).
