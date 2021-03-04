---
title: Использование плана terraform для развертывания виртуальной машины VMware Windows и подключения ее к службе "Дуга" Azure
description: Используйте план terraform для развертывания виртуальной машины VMware Windows и подключения ее к службе "Дуга" Azure.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: b2540c18ea1aa98b0188c29c59564f303fd6fe6c
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102114172"
---
# <a name="use-a-terraform-plan-to-deploy-a-vmware-windows-virtual-machine-and-connect-it-to-azure-arc"></a>Использование плана terraform для развертывания виртуальной машины VMware Windows и подключения ее к службе "Дуга" Azure

В этой статье приводятся рекомендации по использованию предоставленного плана [terraform](https://www.terraform.io/) для развертывания Windows Server, VMware vSphere виртуальной машины и подключения ее в качестве ресурса сервера с поддержкой ARC в Azure.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. [Установка terraform >= 0,12](https://learn.hashicorp.com/tutorials/terraform/install-cli)

4. Пользователь VMware vCenter Server с [разрешениями на развертывание](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-4D0F8E63-2961-4B71-B365-BBFA24673FDB.html) виртуальной машины из шаблона в веб-клиенте vSphere.

5. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину VMware vSphere к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

### <a name="prepare-a-windows-server-vmware-vsphere-vm-template"></a>Подготовка шаблона виртуальной машины VMware vSphere Windows Server

Прежде чем использовать это руководство для развертывания виртуальной машины Windows Server и подключения ее к службе "Дуга Azure", требуется шаблон VMware vSphere. [Такой шаблон можно легко создать с помощью VMware vSphere 6,5 и более поздних версий](./vmware-windows-template.md).

**План terraform использовал подготовку, `remote-exec` который использует протокол WinRM для копирования и выполнения требуемого скрипта Arc Azure. Чтобы разрешить подключение к виртуальной машине по протоколу WinRM, запустите [`allow_winrm`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/winsrv/terraform/scripts/allow_winrm.ps1) сценарий PowerShell на виртуальной машине, прежде чем преобразовывать его в шаблон.**

> [!NOTE]
> Если у вас уже есть шаблон виртуальной машины Windows Server, по-прежнему рекомендуется использовать это руководство в качестве справочной документации.

## <a name="deployment"></a>Развертывание

Перед выполнением плана terraform необходимо задать переменные среды, которые будут использоваться планом. Эти переменные основаны на только что созданном субъекте-службе Azure, вашей подписке Azure и клиенте, а также учетных данных VMware vSphere.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. План terraform создает ресурсы как в Microsoft Azure, так и в VMware vSphere. Затем он выполняет сценарий на виртуальной машине, чтобы установить агент ARC для Azure и все необходимые артефакты. Для этого скрипта требуются определенные сведения о VMware vSphere и средах Azure. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/winsrv/terraform/scripts/vars.sh) и обновите каждую из переменных с помощью соответствующих значений.

    - `TF_VAR_subscription_id` — Идентификатор подписки Azure;
    - `TF_VAR_client_id` = Имя субъекта-службы Azure
    - `TF_VAR_client_secret` — Пароль субъекта-службы Azure.
    - `TF_VAR_tenant_id` — Идентификатор клиента Azure.
    - `TF_VAR_resourceGroup` = Имя группы ресурсов Azure
    - `TF_VAR_location` = Регион Azure
    - `TF_VAR_vsphere_user` = Имя пользователя администратора vCenter
    - `TF_VAR_vsphere_password` = Пароль администратора vCenter
    - `TF_VAR_vsphere_server` = vCenter Server FQDN/IP
    - `TF_VAR_admin_user` = Имя пользователя администратора ОС
    - `TF_VAR_admin_password` = Пароль администратора ОС

3. В интерфейсе командной строки перейдите в `azure_arc_servers_jumpstart/vmware/winsrv/terraform` Каталог клонированного репозитория.

4. Экспортируйте измененные переменные среды, выполнив [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/winsrv/terraform/scripts/vars.sh) команду с исходным кодом, как показано ниже. Terraform требует, чтобы они были установлены для правильного выполнения плана. Обратите внимание, что этот скрипт также будет автоматически выполняться удаленно на виртуальной машине в рамках развертывания terraform.

    ```console
    source ./scripts/vars.sh
    ```

5. Помимо `TF_VAR` переменных среды, которые вы только что экспортировали, измените переменные terraform в в, [`terraform.tfvars`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/winsrv/terraform/terraform.tfvars) чтобы они соответствовали вашей среде VMware vSphere.

    ![Снимок экрана переменных среды "TF_VAR"](./media/vmware-terraform-windows/windows-variables.png)

6. Выполните `terraform init` команду, которая загрузит поставщики terraform AzureRM, Local и vSphere.

    ![Снимок экрана команды "terraform init".](./media/vmware-terraform-windows/terraform-init.png)

7. Выполните `terraform apply --auto-approve` команду и дождитесь завершения плана. После завершения развертывания terraform Новая виртуальная машина Windows Server будет запущена и будет рассматриваться как ресурс сервера Arc Azure во вновь созданной группе ресурсов Azure.

    ![Снимок экрана "terraform Apply" завершен.](./media/vmware-terraform-windows/terraform-apply.png)

    ![Снимок экрана новой VMware vSphere виртуальной машины Windows Server.](./media/vmware-terraform-windows/new-vm.png)

    ![Снимок экрана сервера с поддержкой ARC в Azure в группе ресурсов Azure.](./media/vmware-terraform-windows/server-1.png)

    ![Еще один снимок экрана сервера с поддержкой ARC в Azure в группе ресурсов Azure.](./media/vmware-terraform-windows/server-2.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

- Самый простой способ — удалить ресурс Arc Azure с помощью портал Azure, просто выбрать ресурс и удалить его. Кроме того, удалите VMware vSphere виртуальную машину.

    ![Снимок экрана удаляемого сервера с поддержкой дуги Azure.](./media/vmware-terraform-windows/delete-server.png)

- При удалении экземпляра вручную необходимо также удалить `install_arc_agent.ps1` , который создается с помощью плана terraform.

- Если вы хотите разорвать всю среду, используйте `terraform destroy --auto-approve` команду, как показано ниже.

    ![Снимок экрана команды "terraform Destroy".](./media/vmware-terraform-windows/terraform-destroy.png)
