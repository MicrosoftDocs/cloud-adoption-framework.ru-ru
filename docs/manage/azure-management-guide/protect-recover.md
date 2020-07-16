---
title: Защита и восстановление в Azure
description: Узнайте, как обеспечить стабильность бизнеса, уменьшив время восстановления и вероятность прерываний коммерческой деятельности.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: c25329eae0a7b416b9bcd11eab6599e2e28781fc
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2020
ms.locfileid: "86190708"
---
<!-- cSpell:ignore siterecovery -->

# <a name="protect-and-recover-in-azure"></a>Защита и восстановление в Azure

_Защита и восстановление_ — это третья и окончательная дисциплина в любом базовом плане управления облаком.

![Базовый план управления облаком](../../_images/manage/management-baseline.png)

В статье [Соответствие операций нормативным требованиям в Azure](./operational-compliance.md) задача заключается в снижении вероятности прерывания бизнес-процессов. В этой статье описывается, как сократить длительность и влияние сбоев, которые невозможно предотвратить.

В этой таблице приведены рекомендуемые минимальные средства для базового плана управления для любой среды корпоративного уровня:

| Процесс                 | Инструмент                  | Назначение                                                                                  |
| ----------------------- | --------------------- | ---------------------------------------------------------------------------------------- |
| Защита данных            | Azure Backup          | Резервное копирование данных и виртуальных машин в облаке.                                          |
| Защита среды | Центр безопасности Azure | Повышение уровня безопасности и обеспечение расширенной защиты от угроз для гибридных рабочих нагрузок. |

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backup"></a>[Azure Backup](#tab/AzureBackup)

::: zone-end

С помощью Azure Backup можно выполнять резервное копирование, защиту и восстановление данных в Microsoft Cloud. Azure Backup заменяет имеющееся локальное или внешнее решение резервного копирования облачным. Это новое решение надежное, безопасное и экономически выгодное. Azure Backup также можно использовать для защиты и восстановления локальных ресурсов с помощью единого решения.

### <a name="enable-backup-for-an-azure-vm"></a>Включение резервного копирования для виртуальной машины Azure

1. На портале Azure щелкните **Виртуальные машины**, а затем выберите виртуальную машину для репликации.
1. В области **Операции** выберите **Резервное копирование**.
1. Выберите имеющееся или создайте новое хранилище Служб восстановления Azure.
1. Выберите **Create (or edit) a new policy** (Создать (или изменить) новую политику).
1. Настройте расписание и период хранения.
1. Щелкните **ОК**.
1. Выберите элемент **Включить резервное копирование**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Обзор](https://docs.microsoft.com/azure/backup/backup-overview)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery является критически важным компонентом в стратегии аварийного восстановления.

Site Recovery реплицирует виртуальные машины и рабочие нагрузки, размещенные в основном регионе Azure, в копию, размещенную в дополнительном регионе. При возникновении сбоя в основном регионе выполняется отработка отказа в копию, выполняющуюся в дополнительном регионе. Затем вы можете работать с приложениями и службами оттуда. Этот упреждающий подход к восстановлению может значительно сократить его время. Если среда восстановления больше не нужна, размещение рабочего трафика можно восстановить в исходной среде.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery"></a>Репликация виртуальной машины Azure в другой регион с помощью службы Site Recovery

Далее описан процесс репликации из Azure в Azure (репликация виртуальной машины Azure в другой регион) с помощью Site Recovery.
>
> [!TIP]
> В зависимости от сценария конкретные действия могут немного отличаться.
>

### <a name="enable-replication-for-the-azure-vm"></a>Включение репликации виртуальной машины Azure

1. На портале Azure щелкните **Виртуальные машины**, а затем выберите виртуальную машину для репликации.
1. В области **Операции** выберите **Аварийное восстановление**.
1. Выберите **Настройка аварийного восстановления** > **Целевой регион** и целевой регион, в который будет выполняться репликация.
1. В рамках этого краткого руководства примите значения по умолчанию для остальных параметров.
1. Щелкните **Включить репликацию**, чтобы запустить задание для включения репликации виртуальной машины.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Проверка параметров

После завершения задания репликации можно узнать состояние репликации, проверить работоспособность репликации и протестировать развертывание.

1. В меню виртуальной машины щелкните **Аварийное восстановление**.
1. Проверьте работоспособность репликации, созданные точки восстановления, а также исходный и целевой регионы на карте.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Дополнительные сведения

- [Обзор Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Репликация виртуальной машины Azure в другой регион](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
