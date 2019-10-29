---
title: Защита и восстановление в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Обеспечение стабильности бизнес-процессов за счет уменьшения времени восстановления
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: a79164435772f571849d0a836f43b53ce3bca087
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557012"
---
# <a name="protect-and-recover-in-azure"></a>Защита и восстановление в Azure

Защита и восстановление — это третья и окончательная дисциплина в любом базовом плане управления облаком.

![Базовый план управления облаком](../../_images/manage/management-baseline.png)

В последней статье ("Соответствие операций нормативным требованиям") задача заключается в снижении вероятности прерывания бизнес-процессов. В этой статье ("Защита и восстановление") описывается, как сократить длительность и влияние сбоев, которые невозможно предотвратить.

В следующей таблице приведены рекомендуемые минимальные средства для любого базового плана управления для любой среды корпоративного уровня.

|Process  |Средство  |Назначение  |
|---------|---------|---------|
|Защита данных|Azure Backup|Резервное копирование данных и виртуальных машин в облаке|
|Защита среды|Центр безопасности Azure|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Azure Backup — это служба на платформе Azure, используемая для архивации (защиты) и восстановления данных в Microsoft Cloud. Azure Backup позволяет заменить существующее локальное или автономное решение для резервного копирования на надежное, безопасное и экономичное облачное решение. Ее также можно использовать для защиты и восстановления локальных ресурсов с помощью единого решения.

### <a name="enable-backup-for-an-azure-vm"></a>Включение резервного копирования для виртуальной машины Azure

1. На портале Azure щелкните **Виртуальные машины**, а затем выберите виртуальную машину, которую требуется реплицировать.
1. Из списка **Операции** выберите **Резервное копирование**.
1. Выберите существующее или создайте новое хранилище Служб восстановления.
1. Выберите **Create (or edit) a new policy** (Создать (или изменить) новую политику).
1. Настройте расписание и период хранения.
1. Нажмите кнопку **ОК**.
1. Выберите **Включить резервное копирование**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Обзор](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery является критически важным компонентом в стратегии аварийного восстановления.

Служба Azure Site Recovery позволяет реплицировать виртуальные машины и рабочие нагрузки, размещенные в основном регионе Azure, в их копии, размещенные в дополнительном регионе. При возникновении сбоя в основном регионе можно выполнить отработку отказа на копию, работающую в дополнительном регионе, и продолжить работу со своими приложениями и службами. Этот упреждающий подход к восстановлению может значительно сократить его время. Если среда восстановления больше не нужна, размещение рабочего трафика можно восстановить в исходной среде.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Репликация виртуальной машины Azure в другой регион с помощью службы Site Recovery

Ниже описывается процесс использования службы Site Recovery для репликации виртуальной машины Azure в другой регион (из Azure в Azure).

>
> [!TIP]
> В зависимости от сценария конкретные действия могут немного отличаться.
>

### <a name="enable-replication-for-the-azure-vm"></a>Включение репликации виртуальной машины Azure

1. На портале Azure щелкните **Виртуальные машины**, а затем выберите виртуальную машину, которую требуется реплицировать.
1. В разделе **Операции** щелкните **Аварийное восстановление**.
1. В разделе **Настройка аварийного восстановления** > **Целевой регион** выберите целевой регион, в который будет выполняться репликация.
1. Для выполнения действий в этом кратком руководстве примите другие значения по умолчанию.
1. Щелкните **Включить репликацию**, чтобы запустить задание для включения репликации виртуальной машины.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Проверка параметров

После завершения задания репликации можно узнать состояние репликации, проверить работоспособность репликации и протестировать развертывание.

1. В меню виртуальной машины щелкните **Аварийное восстановление**.
2. Проверьте работоспособность репликации, созданные точки восстановления, а также исходный и целевой регионы на карте.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Подробнее

- [Обзор Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Репликация виртуальной машины Azure в другой регион](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
