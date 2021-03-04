---
title: Применение тегов инвентаризации к серверам с поддержкой ARC в Azure
description: Узнайте, как использовать серверы с поддержкой ARC в Azure для предоставления возможностей управления инвентаризацией серверов в гибридных многооблачных и локальных средах.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 87bbd50d77e9fb0aad7abca351840118ef854eda
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799303"
---
# <a name="apply-inventory-tagging-to-azure-arc-enabled-servers"></a>Применение тегов инвентаризации к серверам с поддержкой ARC в Azure

В этой статье приводятся рекомендации по использованию серверов с поддержкой ARC в Azure для обеспечения возможности управления инвентаризацией серверов в гибридных многооблачных и локальных средах.

Серверы с поддержкой Arc Azure позволяют управлять компьютерами Windows и Linux, размещенными за пределами Azure, в корпоративной сети или у других поставщиков облачных служб. Это аналогично управлению собственными виртуальными машинами в Azure. Если компьютер с гибридной рабочей ролью, не относящийся к Azure, подключен к Azure, он становится подключенным компьютером и рассматривается как ресурс в Azure. Каждый подключенный компьютер имеет идентификатор ресурса, управляется как часть группы ресурсов в рамках подписки и обладает преимуществами стандартных конструкций Azure, таких как политика Azure и применение тегов. Возможность легко упорядочивать и управлять инвентаризацией серверов с помощью Azure в качестве механизма управления значительно сокращает сложность администрирования и обеспечивает единообразную стратегию гибридных и многооблачных сред.

Следующие процедуры используют [Обозреватель графов ресурсов](/azure/governance/resource-graph/first-query-portal) и [Azure CLI](/cli/azure/install-azure-cli) , чтобы продемонстрировать, как помечать и запрашивать инвентаризацию сервера в нескольких облаках из одной области прозрачности в Azure.

> [!IMPORTANT]
> В процедурах, описанных в этой статье, предполагается, что вы уже развернули виртуальные машины или серверы, работающие локально или в других облаках, и подключили их к службе "Дуга Azure". Если вы этого еще не сделали, воспользуйтесь приведенными ниже сведениями для автоматизации этого.

- [Экземпляр обеспечить Ubuntu](./gcp-terraform-ubuntu.md)
- [ОБЕСПЕЧИТЬ экземпляр Windows](./gcp-terraform-windows.md)
- [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
- [AWS Amazon Linux 2, экземпляр EC2](./aws-terraform-al2.md)
- [Виртуальная машина Ubuntu VMware vSphere](./vmware-terraform-ubuntu.md)
- [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
- [Vagrant Ubuntu](./local-vagrant-ubuntu.md)
- [Окно Vagrant Windows](./local-vagrant-windows.md)

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

   ```console
   git clone https://github.com/microsoft/azure_arc
   ```

2. [Установите или обновите Azure CLI до версии 2,7 или более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

   ```console
   az --version
   ```

## <a name="verify-that-your-azure-arc-connected-servers-are-ready-for-tagging"></a>Проверка готовности подключенных серверов ARC в Azure к разметке

Используйте обозреватель графов ресурсов для запроса и просмотра ресурсов в Azure.

1. Введите **Обозреватель графа ресурсов** в верхней строке поиска в портал Azure и выберите его.

    ![Снимок экрана обозревателя графа ресурсов в портал Azure.](./media/inventory-tagging/resource-graph-explorer.png)

1. В окне запроса введите следующий запрос, а затем выберите **выполнить запрос**:

    ```kusto
    Resources
    | where type =~ 'Microsoft.HybridCompute/machines'
    ```

1. Если вы правильно создали серверы с поддержкой ARC в Azure, они будут перечислены на панели результатов в обозревателе графов ресурсов. Кроме того, с помощью портал Azure можно просмотреть включенную дугу Azure.

    ![Снимок экрана запроса обозревателя графа ресурсов.](./media/inventory-tagging/run-query.png)

    ![Снимок экрана с подробными сведениями о сервере с поддержкой дуги Azure в портал Azure.](./media/inventory-tagging/arc-server.png)

## <a name="create-a-basic-azure-tag-taxonomy"></a>Создание базовой таксономии тегов Azure

Откройте Azure CLI и выполните следующие команды, чтобы создать базовую структуру таксономии, позволяющую легко запрашивать и сообщать о том, где размещаются ресурсы сервера (в Azure, AWS, обеспечить или в локальной среде). Дополнительные рекомендации по созданию таксономии тегов см. в [руководстве по именованию ресурсов и созданию тегов](../../../../decision-guides/resource-tagging/index.md).

```console
az tag create --name "Hosting Platform"
az tag add-value --name "Hosting Platform" --value "Azure"
az tag add-value --name "Hosting Platform" --value "AWS"
az tag add-value --name "Hosting Platform" --value "GCP"
az tag add-value --name "Hosting Platform" --value "On-premises"
```

![Снимок экрана с выводом команды "az Tag Create".](./media/inventory-tagging/az-tag-create.png)

## <a name="tag-your-azure-arc-resources"></a>Добавление тегов для ресурсов ARC в Azure

После создания базовой структуры таксономии примените теги к ресурсам сервера с поддержкой дуги Azure. Следующая процедура демонстрирует использование тегов для ресурсов в AWS и обеспечить. Если у вас есть ресурсы только одного из этих поставщиков, можно перейти к соответствующему разделу для AWS или обеспечить.

### <a name="tag-the-azure-arc-connected-aws-ubuntu-ec2-instance"></a>Пометка для экземпляра Azure Arc Connected AWS Ubuntu EC2

В интерфейсе командной строки выполните следующие команды, чтобы применить `Hosting Platform : AWS`  тег к серверам с поддержкой дуги AWS Azure.

> [!NOTE]
> Если вы подключились к экземплярам AWS EC2 с помощью метода, отличного от описанного в [руководстве по Azure](./aws-terraform-ubuntu.md), необходимо скорректировать значения для `awsResourceGroup` и `awsMachineName` в соответствии со значениями конкретной среды.

```console
export awsResourceGroup="arc-aws-demo"
export awsMachineName="arc-aws-demo"
export awsMachineResourceId="$(az resource show --resource-group $awsResourceGroup --name $awsMachineName --resource-type "Microsoft.HybridCompute/machines" --query id)"
export awsMachineResourceId="$(echo $awsMachineResourceId | tr -d "\"" | tr -d '\r')"
az resource tag --ids $awsMachineResourceId --tags "Hosting Platform"="AWS"
```

![Снимок экрана с одним выходом команды AZ Resource Tag.](./media/inventory-tagging/az-resource-tag-1.png)

### <a name="tag-azure-arc-connected-gcp-ubuntu-server"></a>Тег Azure Arc Connected обеспечить Ubuntu Server

В интерфейсе командной строки выполните следующие команды, чтобы применить `Hosting Platform : GCP`  тег к серверам с поддержкой дуги обеспечить Azure.

> [!NOTE]
> Если вы подключились к экземплярам обеспечить с помощью метода, отличного от описанного в соответствующем [руководстве по Terraformу Azure Arc](./gcp-terraform-ubuntu.md), необходимо настроить значения для `gcpResourceGroup` и `gcpMachineName` в соответствии со значениями конкретной среды.

```console
export gcpResourceGroup="arc-gcp-demo"
export gcpMachineName="arc-gcp-demo"
export gcpMachineResourceId="$(az resource show --resource-group $gcpResourceGroup --name $gcpMachineName --resource-type "Microsoft.HybridCompute/machines" --query id)"
export gcpMachineResourceId="$(echo $gcpMachineResourceId | tr -d "\"" | tr -d '\r')"
az resource tag --resource-group $gcpResourceGroup --ids $gcpMachineResourceId --tags "Hosting Platform"="GCP"
```

![Снимок экрана с другим выходом команды AZ Resource Tag.](./media/inventory-tagging/az-resource-tag-2.png)

## <a name="query-resources-by-tag-using-resource-graph-explorer"></a>Запрос ресурсов по тегу с помощью обозревателя графа ресурсов

После применения тегов к ресурсам, размещенным в нескольких облаках, используйте обозреватель графов ресурсов, чтобы запросить их и получить представление о работе в разных облаках.

1. В окне запроса введите следующее:

   ```kusto
   Resources
   | where type =~ 'Microsoft.HybridCompute/machines'
   | where isnotempty(tags['Hosting Platform'])
   | project name, location, resourceGroup, tags
   ```

   ![Снимок экрана с подробными сведениями о запросе обозревателя графа ресурсов.](./media/inventory-tagging/run-query-details.png)

2. Нажмите кнопку **выполнить запрос** , а затем выберите переключатель **отформатированные результаты** . При правильном завершении вы увидите все серверы с поддержкой ARC в Azure и их назначенные `Hosting Platform` значения тегов.

   ![Снимок экрана с результатами запроса обозревателя графа ресурсов.](./media/inventory-tagging/run-query-results.png)

   Также можно просмотреть теги на прогнозируемых серверах с портал Azure.

   ![Снимок экрана одного набора тегов на сервере с поддержкой дуги Azure.](./media/inventory-tagging/tags-1.png)

   ![Снимок экрана другого набора тегов на сервере с поддержкой дуги Azure.](./media/inventory-tagging/tags-2.png)

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

1. Удалите виртуальные машины из каждой среды, следуя инструкциям по уничтожению, приведенным в каждом из руководств.

   - Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
   - [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
   - [VMware VSPHERE виртуальной машины Ubuntu](./vmware-terraform-ubuntu.md) и [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
   - [Vagrant Ubuntu](./local-vagrant-ubuntu.md) и [Vagrant Windows Box](./local-vagrant-windows.md)

1. Удалите теги, созданные в рамках этого руководств, выполнив следующий скрипт в Azure CLI.

   ```console
   az tag remove-value --name "Hosting Platform" --value "Azure"
   az tag remove-value --name "Hosting Platform" --value "AWS"
   az tag remove-value --name "Hosting Platform" --value "GCP"
   az tag remove-value --name "Hosting Platform" --value "On-premises"
   az tag create --name "Hosting Platform"
   ```
