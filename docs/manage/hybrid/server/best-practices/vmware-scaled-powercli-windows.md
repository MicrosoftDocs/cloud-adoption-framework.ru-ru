---
title: Использование VMware PowerCLI для масштабирования VMware vSphere виртуальных машин Windows Server в дугу Azure
description: Используйте VMware PowerCLI для масштабирования VMware vSphere виртуальных машин Windows Server в службе "Дуга" Azure.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: a1ea6c6d66c6b47377228a1b35f237ccb71fcbdf
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101798598"
---
# <a name="use-vmware-powercli-to-scale-onboarding-vmware-vsphere-windows-server-virtual-machines-to-azure-arc"></a>Использование VMware PowerCLI для масштабирования VMware vSphere виртуальных машин Windows Server в дугу Azure

В этой статье приводятся рекомендации по использованию предоставленного сценария [VMware PowerCLI](https://code.vmware.com/web/dp/tool/vmware-powercli/) для выполнения автоматического масштабируемого развертывания агента подключенного компьютера ARC в Azure на нескольких VMware vSphere виртуальных машинах и в результате адаптации этих виртуальных машин в качестве серверов с поддержкой дуги Azure.

В этом учебнике предполагается, что у вас уже есть выход из инвентаризации виртуальных машин VMware, и он будет использовать модуль PowerShell PowerCLI для автоматизации процесса адаптации виртуальных машин в дугу Azure.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 или более поздней.](/cli/azure/install-azure-cli) Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. Установите VMware PowerCLI.

    > [!NOTE]
    > Это руководством было протестировано с последней версией PowerCLI на дату (12.0.0), но более ранние версии должны работать.

    - **Поддерживаемые версии PowerShell:** VMware PowerCLI 12.0.0 совместим со следующими версиями PowerShell:
      - Windows PowerShell 5.1
      - PowerShell 7
      - Подробные инструкции по установке можно найти [здесь](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.esxi.install.doc/GUID-F02D0C2D-B226-4908-9E5C-2E783D41FE2D.html) , но проще всего воспользоваться модулем VMware. PowerCLI из коллекции PowerShell с помощью следующей команды.

        ```powershell
        Install-Module -Name VMware.PowerCLI
        ```

4. Чтобы иметь возможность читать инвентаризацию виртуальных машин из vCenter, а также вызывать скрипт на уровне ОС виртуальной машины, необходимы следующие разрешения.

    - [`VirtualMachine.GuestOperations`](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-6A952214-0E5E-4CCF-9D2A-90948FF643EC.html) Учетная запись пользователя

    - VMware vCenter Server пользователя, которому назначена [роль только для чтения](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.security.doc/GUID-93B962A7-93FA-4E96-B68F-AE66D3D6C663.html)

5. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину VMware vSphere к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

    ```console
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

## <a name="automation-flow"></a>Поток автоматизации

Ниже можно найти поток автоматизации для этого сценария:

1. Пользователь редактирует `vars.ps1` Скрипт PowerCLI.

2. `scale_deploy.ps1`Выполнение скрипта начнет проверку подлинности в vCenter и проверит целевую папку виртуальной машины, где находятся виртуальные машины-кандидаты Azure Arc, и скопирует `vars.ps1` `install-azure-arc-agent.ps1` сценарии и PowerCLI в ОС Windows VM, расположенные в [этой папке](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/vmware/scaled_deployment/powercli/windows) , на каждую виртуальную машину в этой папке.

3. `install-azure-arc-agent.ps1`Сценарий PowerCLI будет выполняться в гостевой ОС виртуальной машины и будет установлен агент подключенного компьютера ARC в Azure для подключения виртуальной машины к службе "Дуга Azure".

## <a name="predeployment"></a>Перед развертыванием

Чтобы продемонстрировать этот сценарий до и после этого, на следующих снимках экрана показана выделенная пустая группа ресурсов Azure, папка виртуальной машины vCenter с потенциальными виртуальными машинами и представление **приложений & компонентов** в Windows, где не установлен агент.

![Снимок экрана: пустая группа ресурсов Azure.](./media/vmware-scale-powercli/cli-windows-empty.png)

![Снимок экрана виртуальной машины обычный VMware vSphere без агента Azure ARC.](./media/vmware-scale-powercli/cli-windows-vanilla-1.png)

![Еще один снимок экрана обычный VMware vSphere виртуальной машины без агента Azure ARC.](./media/vmware-scale-powercli/cli-windows-vanilla-2.png)

## <a name="deployment"></a>Развертывание

Перед выполнением скрипта PowerCLI необходимо задать [переменные среды](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/scaled_deployment/powercli/windows/vars.ps1) , которые будут использоваться сценарием *install-azure-arc-agent.ps1* . Эти переменные основаны на только что созданном субъекте-службе Azure, вашей подписке Azure и клиенте, а также учетных данных и VMware vSphere.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. Используйте идентификатор и пароль субъекта-службы Azure, созданные в разделе Предварительные требования:

    ![Снимок экрана: экспорт переменных среды.](./media/vmware-scale-powercli/cli-windows-export-variables.png)

3. В `azure_arc_servers_jumpstart\vmware\scaled-deploy\powercli\windows` папке откройте сеанс PowerShell от имени администратора и запустите `scale-deploy.ps1` сценарий.

    ![Снимок экрана, посвященный масштабированию и развертыванию с помощью скрипта PowerShell.](./media/vmware-scale-powercli/cli-windows-scale-deploy-1.png)

    ![Второй снимок экрана, посвященный масштабированию и развертыванию с помощью скрипта PowerShell.](./media/vmware-scale-powercli/cli-windows-scale-deploy-2.png)

    ![Третий снимок экрана, посвященный масштабированию и развертыванию с помощью скрипта PowerShell.](./media/vmware-scale-powercli/cli-windows-scale-deploy-3.png)

4. После завершения работы на виртуальной машине будет установлен агент подключенного компьютера Arc Azure, а также группа ресурсов Azure, заполненная новыми серверами с поддержкой дуги Azure.

    ![Снимок экрана виртуальной машины с установленным агентом Arc Azure.](./media/vmware-scale-powercli/cli-windows-agent.png)

    ![Снимок экрана с новыми серверами с поддержкой ARC в Azure в группе ресурсов Azure.](./media/vmware-scale-powercli/cli-windows-servers-1.png)

    ![Еще один снимок экрана с новыми серверами с поддержкой ARC в Azure в группе ресурсов Azure.](./media/vmware-scale-powercli/cli-windows-servers-2.png)
