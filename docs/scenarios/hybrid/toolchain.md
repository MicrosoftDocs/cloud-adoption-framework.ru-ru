---
title: Введение в гибридные и многооблачные продукты Azure
description: Представляем продукты Azure, помогающие использовать гибридные и многооблачные решения.
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/11/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: e2e-hybrid
ms.openlocfilehash: 8d552d0e9e109cbb2d9e98da27d29fc7fe6bdf74
ms.sourcegitcommit: c167c45b66cc7324b60c88b8b7aac439f956b65d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2021
ms.locfileid: "102208903"
---
# <a name="introduction-to-hybrid-and-multicloud-products-on-azure"></a>Введение в гибридные и многооблачные продукты в Azure

Использование эффективного многооблачного многореберного гибридного подхода является более важным, чем когда-либо. Azure нацелен на поддержку гибридных потребностей клиентов с гибридной интеграцией в рамках продуктов Azure.

Клиенты увеличили более сложные способы внедрения нескольких облаков. Несколько продуктов Azure расширили эту перспективу для поддержки локальных, многооблачных, пограничных и Объединенных в эксплуатацию требований клиентов. Гибридная интеграция означает, что клиенты могут постоянно создавать и развертывать приложения и базы данных, работать без проблем и обеспечивать интегрированную облачную безопасность в разнородных средах, обеспечивая унифицированную управление и управление.

В этой статье представлены некоторые продукты Azure с возможностями гибридного и многооблачного обеспечения, которые могут предоставить эту возможность в облачном портфеле.

Более подробные сведения о том, что можно сделать с помощью гибридных и многооблачных продуктов Azure, см. в статье [гибридный и многооблачный центр Azure](/hybrid/).

![Схема, на которой показан обзор гибридных и многооблачных продуктов Azure, перечисленных в этой статье.](../../_images/hybrid/hybrid-hero-slide.png)

Эта серия статей поможет вам интегрировать эти средства в соответствующие процессы, от первоначальной бизнес-стратегии до оптимизации рабочей нагрузки и до длительных циклов управления операциями.

## <a name="manage-hybrid-and-multicloud-environments-with-unified-operations-tools"></a>Управление гибридными и многооблачными средами с помощью единых средств управления операциями

- [Azure Arc](/azure/azure-arc/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это облачная служба, которая расширяет модель управления на основе Azure Resource Manager до ресурсов, не относящихся к Azure, таких как виртуальные машины, кластеры Kubernetes и контейнерные базы данных.
- [Серверы с поддержкой ARC в Azure](/azure/azure-arc/servers/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это гибридная служба, которую можно использовать для управления компьютерами Windows и Linux, размещенными за пределами Azure, в корпоративной сети или у другого поставщика облачных служб. Эта возможность аналогична управлению собственными виртуальными машинами Azure.
- [Kubernetes с поддержкой дуги Azure](/azure/azure-arc/kubernetes/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это гибридная служба, которую можно использовать для упрощения развертывания и управления кластерами Kubernetes внутри или за пределами Azure.
- [SQL Server с поддержкой Arc Azure](/sql/sql-server/azure-arc/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это часть серверов с поддержкой Arc Azure, которая расширяет службы azure для SQL Server экземпляров, размещенных за пределами Azure в центре обработки данных клиента, на границе или в многооблачной среде.
- [Службы данных с поддержкой Arc Azure](/azure/azure-arc/data/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это гибридная служба, которая позволяет запускать службы данных Azure локально, на границе и в общедоступных облаках с помощью Kubernetes и инфраструктуры по своему усмотрению.
- [SQL управляемый экземпляр с поддержкой дуги в Azure](/azure/azure-arc/data/managed-instance-overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это служба данных базы данных SQL Azure, которую можно создать на основе инфраструктуры, в которой размещаются службы данных с поддержкой Arc Azure.

## <a name="deploy-hybrid-and-multicloud-solutions"></a>Развертывание гибридных и многооблачных решений

- [Azure Stack хЦи (20h2)](/azure-stack/hci/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это решение кластера гиперконвергентном INFRASTRUCTURE (хЦи), в котором размещаются виртуальные рабочие нагрузки операционных систем Windows и Linux и их хранилище в гибридной локальной среде. Кластер состоит из 2 – 16 физических узлов.
- [Служба Azure Kubernetes Service (AKS) на Azure Stack хЦи](/azure-stack/aks-hci/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) является реализацией AKS, которая автоматизирует выполнение контейнерных приложений в масштабе Azure Stack хЦи.
- [Служба Azure Kubernetes](/azure/aks/intro-kubernetes?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) упрощает развертывание управляемого кластера Kubernetes в Azure.
- [Azure IOT Edge](/azure/iot-edge/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) развертывает облачные решения на границе локальной среды с полной поддержкой Azure для управления этими устройствами и данными Интернета вещей, которые они создают.

## <a name="connect-your-hybrid-and-multicloud-environments"></a>Подключение гибридных и многооблачных сред

- [Виртуальная глобальная сеть Azure](/azure/virtual-wan/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) подключается к безопасному глобальному решению для ветвления.
- [Azure ExpressRoute](/azure/expressroute/?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) создает быстрое, частное подключение к облачным службам Майкрософт.
- [VPN-шлюз Azure](/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) отправляет зашифрованный трафик в Azure.
- [Брандмауэр Azure](/azure/firewall/overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) — это полностью работоспособный брандмауэр в качестве службы со встроенными возможностями обеспечения высокой доступности и масштабируемости облака.
