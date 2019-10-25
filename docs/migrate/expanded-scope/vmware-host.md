---
title: Ускорение миграции с помощью узлов VMWare
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ускорение миграции с помощью узлов VMWare
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: da05a1acea8029620e55ffbd11c108ab656bd491
ms.sourcegitcommit: 15898374495761bfb76cee719e0f9189856884e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2019
ms.locfileid: "72888864"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Ускорение миграции с помощью узлов VMWare

Миграция целых узлов VMWare может привести к перемещению нескольких рабочих нагрузок и нескольких ресурсов за одну миграцию. Следующие рекомендации помогут расширить область [руководства по миграции Azure](../azure-migration-guide/index.md) с помощью миграции узла VMware.

## <a name="general-scope-expansion"></a>Расширение общей области

Большая часть этих усилий, необходимых для этого расширения области, будет происходить во время выполнения необходимых условий и миграции.

## <a name="suggested-prerequisites"></a>Рекомендуемые предварительные требования

При переносе первого узла VMWare в Azure необходимо выполнить ряд необходимых условий для подготовки требований к идентификации, сети и управлению. После соблюдения предварительных требований для миграции на каждый дополнительный узел требуется значительно меньше усилий. Эти предварительные требования обеспечивают соответствие некоторым ключевым усилиям: Защита среды Azure, управление частным облаком и сеть частного облака.

### <a name="secure-your-azure-environment"></a>Защита среды Azure

Реализуйте соответствующее облачное решение для RBAC и сетевого подключения в среде Azure. В этой реализации можно получить справку по [обеспечению безопасности среды](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) .

### <a name="private-cloud-management"></a>Управление частным облаком

Существует две обязательные задачи и одна необязательная задача, позволяющая установить управление частным облаком. Все необходимые рекомендации необходимы для [повышения привилегий частного облака](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) и [настройки DNS и конфигурации DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) .

Если цель заключается в [переносе рабочих нагрузок с помощью растянутых сетей уровня 2](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), то необходимо использовать эту третьую рекомендацию.

### <a name="private-cloud-networking"></a>Сеть частного облака

После установки требований к управлению сеть частного облака может быть установлена с использованием следующих рекомендаций:

- [VPN-подключение к частному облаку](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Локальное сетевое подключение с помощью ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Подключение виртуальной сети Azure к ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Настройка разрешения DNS-имен](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Интеграция с планом внедрения в облако

После соблюдения предварительных требований каждый узел VMWare будет включен в [план внедрения в облако](../../plan/template.md). В рамках плана внедрения в облако добавьте каждый перемещаемый узел в качестве отдельной [рабочей нагрузки](../../plan/workloads.md). В каждой рабочей нагрузке виртуальные машины, подлежат миграции, могут добавляться в качестве [ресурсов](../../plan/workloads.md). Дополнительные сведения о добавлении рабочих нагрузок и ресурсов в план внедрения см. в разделе [Добавление и изменение рабочих элементов с помощью Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Изменения в процессе миграции

Во время каждой итерации группа перехода работает с помощью невыполненной работы для переноса рабочих нагрузок с наивысшим приоритетом. Процесс в действительности не изменяется для узлов VMWare. Когда следующая Рабочая нагрузка в невыполненной работе является узлом VMWare, единственным изменением будет использование средства.

### <a name="suggested-action-during-the-migrate-process"></a>Предлагаемое действие во время процесса миграции

Ниже приведено несколько примеров средств, которые можно использовать при миграции.

- [Собственные средства VMWare](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Кроме того, можно выполнить миграцию рабочих нагрузок с помощью отработки отказа аварийного восстановления с помощью следующих средств:

- [Резервное копирование виртуальных машин рабочей нагрузки](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Настройка частного облака в качестве сайта аварийного восстановления с помощью Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Настройка частного облака в качестве сайта аварийного восстановления с помощью VMware СРМ](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Дальнейшие действия

Вернитесь к [контрольному списку расширенной области](./index.md), чтобы убедиться, что выбранный метод миграции полностью вам подходит.

> [!div class="nextstepaction"]
> [Контрольный список расширенной области](./index.md)
