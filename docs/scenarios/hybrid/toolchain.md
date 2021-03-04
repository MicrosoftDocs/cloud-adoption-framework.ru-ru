---
title: Введение в гибридные и многооблачные продукты Azure
description: Представляем продукты Azure, помогающие использовать гибридные и многооблачные решения
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/11/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: e2e-hybrid
ms.openlocfilehash: 026170a7d3a70abed6d396eae395bc4c3cd525e4
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101797438"
---
# <a name="introduction-to-hybrid-and-multicloud-products-on-azure"></a>Введение в гибридные и многооблачные продукты в Azure

Использование эффективного многооблачного гибридного подхода является еще более важным, чем когда-либо. Служба Azure была гибридна по проекту с момента начала, что посвящена поддержке гибридных потребностей клиентов, а за последние несколько лет — в центре работ по гибридной интеграции в продуктах Azure.

По мере того как клиенты расширили свое внедрение в нескольких облаках, некоторые продукты Azure были расширены с точки зрения поддержки локальных, многооблачных, пограничных и унифицированных требований клиентов. Гибридная интеграция означает, что клиенты могут постоянно создавать и развертывать приложения и базы данных, работать без проблем и обеспечивать интегрированную облачную безопасность в разнородных средах с единой системой управления и управлением.

В этой статье мы не будем внедрять все продукты Azure с возможностями гибридного и многооблачного, но представите несколько основных продуктов, которые могут разблокировать эту возможность в облачном портфеле.

Более подробные сведения о том, что можно сделать с помощью гибридных и многооблачных продуктов Azure, см. в статье [гибридный и многооблачный центр Azure](/hybrid/) .

![Обзор гибридных и многооблачных продуктов Azure, перечисленных ниже](../../_images/hybrid/hybrid-hero-slide.png)

Эта серия статей поможет интегрировать эти средства в соответствующие процессы — от первоначальной бизнес-стратегии до оптимизации рабочей нагрузки и в течение длительного времени в циклах управления операциями.

## <a name="manage-hybrid-and-multicloud-environments-with-unified-operations-tools"></a>Управление гибридными и многооблачными средами с помощью единых средств управления операциями

- [Дуга Azure](/azure/azure-arc/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) эта облачная служба расширяет модель управления на основе Azure Resource Manager до ресурсов, не относящихся к Azure, включая виртуальные машины, кластеры Kubernetes и контейнерные базы данных.
- [Серверы с поддержкой дуги Azure](/azure/azure-arc/servers/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) эта гибридная служба позволяет управлять компьютерами под управлением Windows и Linux, размещенными за пределами Azure, в корпоративной сети или у другого поставщика облачных служб. Это аналогично управлению собственными виртуальными машинами Azure.
- Служба " [дуга Azure" включена Kubernetes](/azure/azure-arc/kubernetes/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) . Это позволяет упростить развертывание и Управление кластерами Kubernetes внутри или за пределами Azure.
- Служба " [дуга Azure", включенная SQL Server](/sql/sql-server/azure-arc/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) этой части серверов с поддержкой дуги Azure, расширяет службы azure для SQL Server экземпляров, размещенных за пределами Azure в центре обработки данных клиента, на границе или в многооблачной среде.
- [Службы данных, поддерживающие службу "Дуга Azure](/azure/azure-arc/data/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) ". Эта гибридная служба позволяет запускать службы данных Azure локально, на границе и в общедоступных облаках с помощью Kubernetes и инфраструктуры по своему усмотрению.
- Служба " [дуга Azure" с поддержкой sql управляемый экземпляр](/azure/azure-arc/data/managed-instance-overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) эту службу данных базы данных SQL Azure можно создать на выбранной инфраструктуре, где размещаются службы данных, поддерживающие службу "Дуга Azure".

## <a name="deploy-hybrid-and-multicloud-solutions"></a>Развертывание гибридных и многооблачных решений

- [Azure Stack хЦи (20h2)](/azure-stack/hci/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) это решение кластера гиперконвергентном Infrastructure (хЦи), которое содержит виртуализированные рабочие нагрузки операционных систем Windows и Linux и их хранилище в гибридной локальной среде. Кластер состоит из двух и 16 физических узлов.
- [Служба Kubernetes Azure на Azure Stack хЦи](/azure-stack/aks-hci/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) . это реализация AKS, которая автоматизирует выполнение контейнерных приложений в масштабе Azure Stack хЦи.
- [Служба Kubernetes Azure](/azure/aks/intro-kubernetes?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это служба, которая упрощает развертывание управляемого кластера Kubernetes в Azure.
- [Azure IOT Edge](/azure/iot-edge/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) развернуть облачные решения на границе локальной среды с полной поддержкой Azure для управления этими устройствами и данными Интернета вещей, которые они создают.

## <a name="connect-your-hybrid-and-multicloud-environments"></a>Подключение гибридных и многооблачных сред

- [Виртуальная глобальная сеть](/azure/virtual-wan/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) подключается к защищенному глобальному решению разветвления.
- [ExpressRoute](/azure/expressroute/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) создает быстрое, частное подключение к облачным службам Майкрософт
- [VPN-шлюз](/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) отправляет зашифрованный трафик в Azure
- Брандмауэр [Azure](/azure/firewall/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) с полным состоянием брандмауэра в качестве службы со встроенными возможностями обеспечения высокой доступности и масштабируемости облака.
