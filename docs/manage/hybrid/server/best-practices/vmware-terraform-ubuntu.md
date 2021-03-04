---
title: Использование плана terraform для развертывания виртуальной машины Ubuntu в VMware и ее подключения к службе "Дуга Azure"
description: Используйте план terraform, чтобы развернуть виртуальную машину Ubuntu в VMware и подключить ее к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 99e146fe7d1a7218efc5de212c163ea87739d557
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799068"
---
# <a name="use-a-terraform-plan-to-deploy-a-vmware-ubuntu-virtual-machine-and-connect-it-to-azure-arc"></a>Использование плана terraform для развертывания виртуальной машины Ubuntu в VMware и ее подключения к службе "Дуга Azure"

В этой статье приводятся рекомендации по использованию предоставленного плана [terraform](https://www.terraform.io/) для развертывания сервера Ubuntu, VMware vSphere виртуальной машины и подключения его в качестве ресурса сервера с поддержкой ARC в Azure.

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

    ```bash
    az login
    az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
    ```

    Пример.

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

### <a name="preparing-an-ubuntu-server-vmware-vsphere-vm-template"></a>Подготовка шаблона виртуальной машины VMware vSphere Ubuntu Server

Перед использованием приведенного ниже руководством по развертыванию виртуальной машины Ubuntu Server и ее подключению к службе "Дуга Azure" требуется шаблон VMware vSphere. В [этой статье](./vmware-ubuntu-template.md) показано, как легко создать такой шаблон с помощью VMware vSphere 6,5 и более поздних версий.

> [!NOTE]
> Если у вас уже есть шаблон виртуальной машины Ubuntu Server, по-прежнему рекомендуется использовать это руководство в качестве справочной документации.

## <a name="deployment"></a>Развертывание

Перед выполнением плана terraform необходимо задать переменные среды, которые будут использоваться планом. Эти переменные основаны на только что созданном субъекте-службе Azure, вашей подписке Azure и клиенте, а также учетных данных VMware vSphere.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. План terraform создает ресурсы как в Microsoft Azure, так и в VMware vSphere. Затем он выполняет сценарий на виртуальной машине, чтобы установить агент ARC для Azure и все необходимые артефакты. Для этого скрипта требуются определенные сведения о VMware vSphere и средах Azure. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/ubuntu/terraform/scripts/vars.sh) и обновите каждую из переменных с помощью соответствующих значений.

    - `TF-VAR-subscription-id` — Идентификатор подписки Azure;
    - `TF-VAR-client-id` = Имя субъекта-службы Azure
    - `TF-VAR-client-secret`— Пароль субъекта-службы Azure.
    - `TF-VAR-tenant-id` — Идентификатор клиента Azure.
    - `TF-VAR-resourceGroup` = Имя группы ресурсов Azure
    - `TF-VAR-location` = Регион Azure
    - `TF-VAR-vsphere-user` = Имя пользователя администратора vCenter
    - `TF-VAR-vsphere-password` = Пароль администратора vCenter
    - `TF-VAR-vsphere-server` = vCenter Server FQDN/IP
    - `TF-VAR-admin-user` = Имя пользователя администратора ОС
    - `TF-VAR-admin-password` = Пароль администратора ОС

3. В интерфейсе командной строки перейдите в `azure_arc_servers_jumpstart/vmware/ubuntu/terraform` Каталог клонированного репозитория.

4. Экспортируйте измененные переменные среды, выполнив [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/ubuntu/terraform/scripts/vars.sh) команду с исходным кодом, как показано ниже. Terraform требует, чтобы они были установлены для правильного выполнения плана. Обратите внимание, что этот скрипт также будет автоматически выполняться удаленно на виртуальной машине в рамках развертывания terraform.

    `source ./scripts/vars.sh`

5. Помимо `TF-VAR` переменных среды, которые вы только что экспортировали, измените переменные terraform в в, [`terraform.tfvars`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/ubuntu/terraform/terraform.tfvars) чтобы они соответствовали вашей среде VMware vSphere.

    ![Снимок экрана переменных среды TF-VAR](./media/vmware-terraform-ubuntu/variables.png)

6. Выполните `terraform init` команду, которая загрузит поставщики terraform AzureRM, Local и vSphere.

    ![Снимок экрана команды "terraform init".](./media/vmware-terraform-ubuntu/terraform-init.png)

7. Выполните `terraform apply --auto-approve` команду и дождитесь завершения плана.

8. После завершения развертывания terraform Новая виртуальная машина Ubuntu Server будет запущена и будет рассматриваться как ресурс сервера, поддерживающий дугу Azure, в созданной группе ресурсов Azure.

    ![Снимок экрана "terraform Apply" завершен.](./media/vmware-terraform-ubuntu/terraform-apply.png)

    ![Снимок экрана новой виртуальной машины VMware vSphere Ubuntu Server.](./media/vmware-terraform-ubuntu/new-vm.png)

    ![Снимок экрана сервера с поддержкой ARC в Azure в группе ресурсов Azure.](./media/vmware-terraform-ubuntu/server-1.png)

    ![Еще один снимок экрана сервера с поддержкой ARC в Azure в группе ресурсов Azure.](./media/vmware-terraform-ubuntu/server-2.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

- Самый простой способ — удалить ресурс Arc Azure с помощью портал Azure, просто выбрать ресурс и удалить его. Кроме того, удалите VMware vSphere виртуальную машину.

  ![Снимок экрана удаляемого сервера с поддержкой дуги Azure.](./media/vmware-terraform-ubuntu/delete-server.png)

  При удалении экземпляра вручную необходимо также удалить *Install-Azure-Arc-Agent.sh* , созданный планом terraform.

- Если вы хотите разорвать всю среду, используйте `terraform destroy --auto-approve` команду, как показано ниже.

  ![Снимок экрана команды "terraform Destroy".](./media/vmware-terraform-ubuntu/terraform-destroy.png)
