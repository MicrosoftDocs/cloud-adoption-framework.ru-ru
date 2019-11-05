---
title: Ускорение миграции с помощью узлов VMware
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ускорение миграции с помощью узлов VMware
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 724a227407f431e08b5344dfd1280397bfca9b65
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566871"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Ускорение миграции с помощью узлов VMware

Миграция целых узлов VMware может привести к перемещению нескольких рабочих нагрузок и нескольких ресурсов за одну миграцию. Следующие рекомендации расширяют область действия [руководства по миграции Azure](../azure-migration-guide/index.md) с помощью миграции узла VMware. Большая часть усилий, которые необходимо выполнить в этом расширении области, возникает во время выполнения предварительных требований и процессов миграции.

## <a name="suggested-prerequisites"></a>Рекомендуемые предварительные требования

При переносе первого узла VMware в Azure необходимо выполнить ряд предварительных требований для подготовки требований к идентификации, сети и управлению. После выполнения этих предварительных требований для миграции на каждый дополнительный узел требуется значительно меньше усилий. Следующие разделы содержат более подробные сведения о необходимых условиях.

### <a name="secure-your-azure-environment"></a>Защита среды Azure

Реализуйте соответствующее облачное решение для управления доступом на основе ролей и сетевое подключение в среде Azure. В этой реализации можно получить справку по [обеспечению безопасности среды](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) .

### <a name="private-cloud-management"></a>Управление частным облаком

Существует две обязательные задачи и одна необязательная задача, позволяющая установить управление частным облаком. Все необходимые рекомендации необходимы для [повышения привилегий частного облака](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) и [настройки DNS и конфигурации DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) .

Если цель заключается в [переносе рабочих нагрузок с помощью растянутых сетей уровня 2](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), также необходимо использовать эту третьную рекомендацию.

### <a name="private-cloud-networking"></a>Сети для частного облака

После установки требований к управлению можно установить сеть частного облака, следуя приведенным ниже рекомендациям.

- [VPN-подключение к частному облаку](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Локальное сетевое подключение с помощью ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Подключение виртуальной сети Azure к ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Настройка разрешения DNS-имен](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Интеграция с планом внедрения в облако

После выполнения других условий необходимо включить каждый узел VMware в [план внедрения в облако](../../plan/template.md). В рамках плана внедрения в облако добавьте каждый перемещаемый узел в качестве отдельной [рабочей нагрузки](../../plan/workloads.md). В каждой рабочей нагрузке добавьте виртуальные машины для переноса в качестве [ресурсов](../../plan/workloads.md). Дополнительные сведения о добавлении рабочих нагрузок и ресурсов в план внедрения см. в разделе [Добавление и изменение рабочих элементов с помощью Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Изменения в процессе миграции

Во время каждой итерации группа перехода работает с помощью невыполненной работы для переноса рабочих нагрузок с наивысшим приоритетом. Процесс в действительности не изменяется для узлов VMware. Когда следующая Рабочая нагрузка в невыполненной работе является узлом VMware, единственным изменением будет использование средства.

В ходе миграции можно использовать следующие средства.

- [Собственные средства VMware](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Кроме того, можно перенести рабочие нагрузки с помощью отработки отказа аварийного восстановления с помощью следующих средств:

- [Резервное копирование виртуальных машин рабочей нагрузки](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Настройка частного облака в качестве сайта аварийного восстановления с помощью Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Настройка частного облака в качестве сайта аварийного восстановления с помощью VMware СРМ](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Дальнейшие действия

Вернитесь к контрольному списку расширенной области, чтобы обеспечить полное согласование метода миграции.

> [!div class="nextstepaction"]
> [Контрольный список расширенной области](./index.md)
