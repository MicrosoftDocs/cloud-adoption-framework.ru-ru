---
title: Развертывание Microsoft Monitoring Agent в Azure Arc и серверы Windows
description: Узнайте, как управлять расширениями и использовать шаблон Azure Resource Manager для развертывания Microsoft Monitoring Agent в Azure Arc и Windows Servers.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: c1555d43bfe245f307284b0702742c41f6030cbc
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102112184"
---
# <a name="manage-extensions-and-use-an-azure-resource-manager-template-to-deploy-microsoft-monitoring-agent-to-azure-arc-linux-and-windows-servers"></a>Управление расширениями и использование шаблона Azure Resource Manager для развертывания Microsoft Monitoring Agent в Azure Arc на серверах Linux и Windows

В этой статье содержатся рекомендации по управлению расширениями на серверах с поддержкой ARC в Azure. Расширения виртуальных машин — это небольшие приложения, которые обеспечивают настройку и задачи автоматизации после развертывания, такие как установка программного обеспечения, антивирусная защита или механизм выполнения пользовательского сценария.

Серверы с поддержкой ARC в Azure позволяют развертывать расширения виртуальных машин Azure на виртуальных машинах Windows и Linux без Azure, обеспечивая гибридную или облачную среду управления с уровнями для виртуальных машин Azure.

Вы можете использовать портал Azure, Azure CLI, шаблон Azure Resource Manager (шаблон ARM), скрипт PowerShell или политики Azure для управления развертыванием расширения на серверах с поддержкой ARC в Azure, как в Linux, так и в Windows. В следующих процедурах используется шаблон ARM для развертывания Microsoft Monitoring Agent (MMA) на серверах. Это позволит подключить их в службах Azure, использующих этот агент: Azure Monitor, центр безопасности Azure, Sentinel Azure и т. д.

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

Ознакомьтесь с [Azure Monitor поддерживаемой документацией ОС](/azure/azure-monitor/vm/vminsights-enable-overview#supported-operating-systems) и убедитесь, что виртуальные машины, которые будут использоваться для этого упражнения, поддерживаются. Для виртуальных машин Linux проверьте как дистрибутив Linux, так и ядро, чтобы убедиться в том, что используется поддерживаемая конфигурация.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. Как уже упоминалось, это руководства начинается в том месте, где вы уже развернули и подключили виртуальные машины или серверы без операционной системы в дугу Azure. В этом сценарии используется экземпляр Google Cloud Platform (обеспечить), который уже подключен к службе "Дуга Azure" и отображается как ресурс в Azure. Как показано на следующих снимках экрана:

    ![Снимок экрана группы ресурсов с сервера с поддержкой дуги Azure.](./media/arc-vm-extension-mma/mma-resource-group.png)

    ![Снимок экрана с подключенным состоянием с сервера с поддержкой дуги Azure.](./media/arc-vm-extension-mma/mma-connected-status.png)

3. [Установите или обновите Azure CLI](/cli/azure/install-azure-cli). Azure CLI должна работать под управлением версии 2,7 или более поздней. Используйте `az --version` для проверки текущей установленной версии.

4. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину или сервер без операционной системы к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в свою учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

    ```console
    az login
    az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
    ```

    Пример:

    ```console
    az ad sp create-for-rbac -n "http://AzureArcServers" --role contributor
    ```

    Выходные данные должны выглядеть следующим образом:

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

5. Кроме того, потребуется развернутая Рабочая область Log Analytics. Можно автоматизировать развертывание, изменив [файл параметров](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/extensions/arm/log_analytics-template.parameters.json)шаблона ARM и указав имя и расположение рабочей области.

    ![Снимок экрана параметров шаблона ARM для имени и расположения.](./media/arc-vm-extension-mma/parameters-file-1.png)

6. Чтобы развернуть шаблон ARM, перейдите в `../extensions/arm` папку Deployment и выполните следующую команду:

    ```console
    az deployment group create --resource-group <Name of the Azure resource group> \
    --template-file <The `log_analytics-template.json` template file location> \
    --parameters <The `log_analytics-template.parameters.json` template file location>
    ```

## <a name="azure-arc-enabled-servers-microsoft-monitoring-agent-extension-deployment"></a>Развертывание расширений Microsoft Monitoring Agent серверов с поддержкой ARC в Azure

1. Изменение [файла параметров расширений](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/extensions/arm/mma-template.parameters.json)

    ![Снимок экрана файла параметров расширений ARM.](./media/arc-vm-extension-mma/parameters-file-2.png)

    Чтобы соответствовать вашей конфигурации, необходимо предоставить следующие параметры:

    - Имя виртуальной машины, зарегистрированное в службе "Дуга Azure".

      ![Снимок экрана имени компьютера с сервера с поддержкой дуги Azure.](./media/arc-vm-extension-mma/mma-machine-name.png)

    - Расположение группы ресурсов, в которой зарегистрирован сервер с поддержкой Arc Azure.

      ![Снимок экрана региона Azure.](./media/arc-vm-extension-mma/mma-azure-region.png)

    - Сведения о созданной ранее рабочей области Log Analytics (идентификатор и ключ рабочей области). Эти параметры используются для настройки агента MMA. Чтобы найти эти сведения, перейдите в рабочую область Log Analytics и в разделе **Параметры** выберите **Управление агентами**.

      ![Снимок экрана управления агентами на сервере с поддержкой дуги Azure.](./media/arc-vm-extension-mma/agents-management.png)

      ![Снимок экрана конфигурации рабочей области.](./media/arc-vm-extension-mma/mma-workspace-config.png)

2. Выберите шаблон ARM, соответствующий вашей операционной системе, [Windows](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/extensions/arm/mma-template-windows.json) или [Linux](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/extensions/arm/mma-template-linux.json), разверните шаблон, выполнив следующую команду:

    ```console
    az deployment group create --resource-group <Name of the Azure resource group> \
    --template-file <The `mma-template.json` template file location> \
    --parameters <The `mma-template.parameters.json` template file location>
    ```

3. После завершения выполнения шаблона вы увидите результат, аналогичный приведенному ниже:

    ![Снимок экрана с выходными данными из шаблона ARM.](./media/arc-vm-extension-mma/mma-output.png)

4. Вы получите Microsoft Monitoring Agent, развернутую в системе Windows или Linux, и отправите отчеты в выбранную рабочую область Log Analytics. Вы можете проверить, вернувшись к **управлению агентами** в рабочей области и выбрав **Windows** или **Linux**. Вы должны увидеть дополнительную подключенную виртуальную машину.

    ![Снимок экрана подключенных агентов для серверов Windows.](./media/arc-vm-extension-mma/windows-agents.png)

    ![Снимок экрана с подключенными агентами для серверов Linux.](./media/arc-vm-extension-mma/linux-agents.png)

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

1. Удалите виртуальные машины из каждой среды, следуя инструкциям по уничтожению, приведенным в каждом из руководств.

    - Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
    - [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
    - [VMware VSPHERE виртуальной машины Ubuntu](./vmware-terraform-ubuntu.md) и [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
    - [Vagrant Ubuntu](./local-vagrant-ubuntu.md) и [Vagrant Windows Box](./local-vagrant-windows.md)

2. Удалите рабочую область Log Analytics, выполнив следующую команду в Azure CLI. Укажите имя рабочей области, которое использовалось при создании рабочей области Log Analytics.

    ```console
    az monitor log-analytics workspace delete --resource-group <Name of the Azure resource group> --workspace-name <Log Analytics Workspace Name> --yes
    ```
