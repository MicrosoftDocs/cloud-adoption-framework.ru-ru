---
title: Управление политиками Azure и развертывание расширения агента мониторинга Azure в Azure Arc Linux и Windows Server
description: Узнайте, как использовать серверы с поддержкой ARC в Azure для назначения политик Azure виртуальным машинам вне Azure, будь то локальная среда или другие облака.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 56210c7fdef90f9ba50378adce35ab7f8a09b3e3
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799258"
---
# <a name="manage-azure-policies-and-deploy-the-azure-monitoring-agent-extension-to-azure-arc-linux-and-windows-servers"></a>Управление политиками Azure и развертывание расширения агента мониторинга Azure в Azure Arc Linux и Windows Server

В этой статье приводятся рекомендации по использованию серверов с поддержкой ARC в Azure для назначения политик Azure виртуальным машинам вне Azure, будь то локальная среда или другие облака. С помощью этой функции вы теперь можете использовать политику Azure для аудита параметров в операционной системе сервера с поддержкой дуги Azure, если параметр не соответствует требованиям, также можно запустить задачу исправления.

В этом случае необходимо назначить политику для аудита, если на подключенном компьютере Arc Azure установлен агент MMA (Microsoft Monitoring Agent). В противном случае используйте функцию расширений, чтобы автоматически развернуть ее на виртуальной машине. это процедура регистрации для виртуальных машин Azure. Этот подход можно использовать, чтобы убедиться, что все серверы подключены к службам, таким как Azure Monitor, центр безопасности Azure, Sentinel Azure и т. д.

Для назначения политик подпискам Azure или группам ресурсов можно использовать портал Azure, шаблон Azure Resource Manager (шаблон ARM) или скрипт PowerShell. Следующие процедуры используют шаблон ARM для назначения встроенных политик.

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

Обратитесь к [документации по поддерживаемой ос Azure Monitor](/azure/azure-monitor/insights/vminsights-enable-overview#supported-operating-systems) и убедитесь, что виртуальные машины, используемые для этих процедур, поддерживаются. Для виртуальных машин Linux проверьте как дистрибутив Linux, так и ядро, чтобы убедиться в том, что используется поддерживаемая конфигурация.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

   ```console
   git clone https://github.com/microsoft/azure_arc
   ```

2. Как уже упоминалось, это руководства начинается в том месте, где вы уже развернули и подключили виртуальные машины или серверы в дугу Azure. На следующих снимках экрана сервер Google Cloud Platform (обеспечить) был подключен к службе "Дуга Azure" и отображается как ресурс в Azure.

   ![Снимок экрана группы ресурсов для сервера с поддержкой Arc Azure.](./media/arc-policies-mma/resource-group.png)

   ![Снимок экрана с состоянием "подключено" для сервера с поддержкой Arc Azure.](./media/arc-policies-mma/connected-status.png)

3. [Установите или обновите Azure CLI](/cli/azure/install-azure-cli). Azure CLI должна работать под управлением версии 2,7 или более поздней. Используйте `az --version` для проверки текущей установленной версии.

4. Создайте субъект-службу Azure.

   Чтобы подключить виртуальную машину или сервер без операционной системы к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

   ```console
   az login
   az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
   ```

   Пример.

   ```console
   az ad sp create-for-rbac -n "http://AzureArcServers" --role contributor
   ```

   Выходные данные должны выглядеть так:

   ```json
   {
   "appId": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
   "displayName": "AzureArcServers",
   "name": "http://AzureArcServers",
   "password": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
   "tenant": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
   }
   ```

   > [!NOTE]
   > Мы настоятельно рекомендуем ограничить субъект-службу определенной [подпиской Azure и группой ресурсов](/cli/azure/ad/sp).

Вам также потребуется развернутая Рабочая область Log Analytics. Вы можете автоматизировать развертывание, изменив [файл параметров](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/policies/arm/log_analytics-template.parameters.json) шаблона ARM и указав имя и расположение рабочей области.

![Снимок экрана файла параметров шаблона ARM.](./media/arc-policies-mma/parameter-file-1.png)

Чтобы развернуть шаблон ARM, перейдите в [папку Deployment](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/policies/arm) и выполните следующую команду:

```console
az deployment group create --resource-group <Name of the Azure resource group> \
--template-file <The `log_analytics-template.json` template file location> \
--parameters <The `log_analytics-template.parameters.json` template file location>
```

## <a name="assign-policies-to-azure-arc-connected-machines"></a>Назначение политик для подключенных к Azure Arc компьютеров

После установки всех необходимых компонентов можно назначить политики для подключенных к Azure Arc компьютеров. Измените [файл параметров](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/policies/arm/policy.json) , чтобы указать идентификатор подписки, а также рабочую область log Analytics.

![Снимок экрана другого файла параметров шаблона ARM.](./media/arc-policies-mma/parameter-file-2.png)

1. Чтобы запустить развертывание, используйте следующую команду:

   ```console
   az policy assignment create --name 'Enable Azure Monitor for VMs' \
   --scope '/subscriptions/<Your subscription ID>/resourceGroups/<Name of the Azure resource group>' \
   --policy-set-definition '55f3eceb-5573-4f18-9695-226972c6d74a' \
   -p <The *policy.json* template file location> \
   --assign-identity --location <Azure Region>
   ```

   `policy-set-definition`Флаг указывает на `Enable Azure Monitor` идентификатор определения инициативы.

2. После назначения инициативы для применения назначения к определенной области потребуется около 30 минут. Затем политика Azure запускает цикл оценки на подключенном компьютере ARC в Azure и распознает его как несоответствующий, так как по-прежнему не развернута конфигурация агента Log Analytics. Чтобы проверить это, перейдите на подключенный компьютер ARC в Azure в разделе "политики".

   ![Снимок экрана состояния политики Azure, не совместимой с.](./media/arc-policies-mma/noncompliant-policy.png)

3. Теперь назначьте задаче исправления несоответствующему ресурсу, чтобы перевести его в соответствующее состояние.

   ![Снимок экрана создания задачи по исправлению политик Azure.](./media/arc-policies-mma/create-remediation-task.png)

4. В разделе **Политика для исправления** выберите **\[ Предварительный просмотр] разверните узел log Analytics агент на компьютерах с машинными машинами Linux Azure** и выберите **исправить**. Эта задача по исправлению сообщает политике Azure о выполнении этого `DeployIfNotExists` действия и использует возможности управления расширениями Arc Azure для развертывания агента log Analytics на виртуальной машине.

   ![Снимок экрана действия по исправлению политики Azure в рамках задачи исправления.](./media/arc-policies-mma/remediation-action.png)

5. После назначения задачи по исправлению политика будет повторно оценена. Он должен показывать, что сервер на обеспечить соответствует требованиям, а расширение Microsoft Monitoring Agent установлено на компьютере Arc Azure.

   ![Снимок экрана конфигурации задачи исправления.](./media/arc-policies-mma/task-config.png)

   ![Снимок экрана состояния совместимой политики Azure.](./media/arc-policies-mma/compliant-status.png)

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

1. Удалите виртуальные машины из каждой среды, следуя инструкциям по уничтожению, приведенным в каждом из руководств.

   - Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
   - [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
   - [VMware VSPHERE виртуальной машины Ubuntu](./vmware-terraform-ubuntu.md) и [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
   - [Vagrant Ubuntu](./local-vagrant-ubuntu.md) и [Vagrant Windows Box](./local-vagrant-windows.md)

2. Удалите назначение политики Azure, выполнив следующий скрипт в Azure CLI.

   ```console
   az policy assignment delete --name 'Enable Azure Monitor for VMs' --resource-group <resource-group>
   ```

3. Удалите рабочую область Log Analytics, выполнив следующий скрипт в Azure CLI. Укажите имя рабочей области, которое использовалось при создании рабочей области Log Analytics.

   ```console
   az monitor log-analytics workspace delete --resource-group <Name of the Azure resource group> --workspace-name <Log Analytics workspace Name> --yes
   ```
