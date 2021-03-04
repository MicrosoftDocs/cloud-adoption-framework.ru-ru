---
title: Использование расширений виртуальной машины и шаблона Azure Resource Manager для развертывания настраиваемых скриптов в Azure Arc Linux и Windows Server
description: Узнайте, как выполнять пользовательские скрипты на серверах с поддержкой дуги Azure с помощью расширений виртуальной машины, которые обеспечивают настройку и задачи автоматизации после развертывания.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: b8ac9e7f9041fe94d0644e06e342a1a1f6978d8a
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102112013"
---
# <a name="use-virtual-machine-extensions-and-an-azure-resource-manager-template-to-deploy-custom-scripts-to-azure-arc-linux-and-windows-servers"></a>Использование расширений виртуальной машины и шаблона Azure Resource Manager для развертывания настраиваемых скриптов в Azure Arc Linux и Windows Server

В этой статье содержатся инструкции по выполнению настраиваемых сценариев на серверах с поддержкой ARC в Azure с помощью расширений виртуальной машины. Расширения виртуальных машин — это небольшие приложения, которые обеспечивают настройку и задачи автоматизации после развертывания, такие как установка программного обеспечения, антивирусная защита или механизм выполнения пользовательского сценария.

Вы можете использовать портал Azure, Azure CLI, шаблон Azure Resource Manager (шаблон ARM), PowerShell или скрипт оболочки Linux или политики Azure для управления развертыванием расширения на серверах с поддержкой Arc Azure. В следующих процедурах используется шаблон ARM для развертывания расширения пользовательских скриптов. Это расширение скачивает и выполняет сценарии на виртуальных машинах. Это полезно для настройки после развертывания, установки программного обеспечения или любых других задач настройки или управления.

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
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. Как упоминалось ранее, это руководства начинается в том месте, где вы уже развернули и подключили виртуальные машины или серверы в дугу Azure. На следующих снимках экрана показан сервер обеспечить, подключенный к службе "Дуга Azure" и видимый как ресурс в Azure.

    ![Снимок экрана группы ресурсов с сервера с поддержкой дуги Azure.](./media/arc-vm-extension-custom-script/resource-group.png)

    ![Снимок экрана с подключенным состоянием с сервера с поддержкой дуги Azure.](./media/arc-vm-extension-custom-script/connected-status.png)

3. [Установите или обновите Azure CLI](/cli/azure/install-azure-cli). Azure CLI должна работать под управлением версии 2,7 или более поздней. Используйте `az --version` для проверки текущей установленной версии.

4. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину или сервер без операционной системы к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

Чтобы продемонстрировать расширение пользовательского скрипта, используйте приведенные ниже сценарии Linux и Windows.

- [Linux](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/scripts/custom_script_linux.sh). сценарий изменит сообщение в операционной системе.
- [Windows](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/scripts/custom_script_windows.ps1): скрипт установит Windows Terminal, Microsoft погранично, 7-Zip и Visual Studio Code [шоколадные](https://chocolatey.org/) пакеты на виртуальной машине.

## <a name="azure-arc-enabled-servers-custom-script-extension-deployment"></a>Развертывание расширения пользовательских скриптов для серверов с поддержкой ARC в Azure

1. Изменение файла параметров расширений для [Windows](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/extensions/arm/customscript-templatewindows.parameters.json) или [Linux](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/extensions/arm/customscript-templatelinux.parameters.json)

   ![Снимок экрана файла параметров шаблона ARM.](./media/arc-vm-extension-custom-script/parameters-file.png)

2. Укажите следующие сведения в соответствии с конфигурацией среды:

    - Имя виртуальной машины, зарегистрированное в службе "Дуга Azure".

    ![Снимок экрана имени компьютера с сервера с поддержкой дуги Azure.](./media/arc-vm-extension-custom-script/machine-name.png)

    - Расположение группы ресурсов, в которой зарегистрирован сервер с поддержкой Arc Azure.

    ![Снимок экрана региона Azure.](./media/arc-vm-extension-custom-script/azure-region.png)

    - Общедоступный URI для скрипта, который вы хотите запустить на серверах. в этом случае используйте URL-адрес скрипта в формате RAW.
      - Для Windows: [общедоступный URI](https://raw.githubusercontent.com/microsoft/azure_arc/main/azure_arc_servers_jumpstart/scripts/custom_script_windows.ps1)
      - Для Linux: [общедоступный URI](https://raw.githubusercontent.com/microsoft/azure_arc/main/azure_arc_servers_jumpstart/scripts/custom_script_linux.sh)

3. Чтобы выполнить любой из этих сценариев, используйте следующие команды:

    - Windows:

         ```powershell
         powershell -ExecutionPolicy Unrestricted -File custom_script_windows.ps1
         ```

    - Linux:

         ```bash
         ./custom_script_linux.sh
         ```

4. Чтобы развернуть шаблон ARM для Linux или Windows, перейдите к [папке развертывания](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/extensions/arm) и выполните следующую команду с шаблонами, соответствующими вашей операционной системе:

    ```bash
    az deployment group create --resource-group <Name of the Azure resource group> \
    --template-file <The `customscript-template.json` template file location for Linux or Windows> \
    --parameters <The `customscript-template.parameters.json` template file location>
    ```

5. После завершения развертывания шаблона вы увидите выходные данные следующим образом:

    ![Снимок экрана с выходными данными из шаблона ARM.](./media/arc-vm-extension-custom-script/output.png)

6. Проверьте успешность развертывания на сервере с поддержкой ARC в Azure в портал Azure, выбрав параметры **расширения** . Вы должны увидеть установленное расширение пользовательских скриптов.

    ![Снимок экрана расширения пользовательского скрипта.](./media/arc-vm-extension-custom-script/custom-script-extension.png)

Еще один способ проверки успешного выполнения пользовательского скрипта — подключение к виртуальным машинам и проверка настройки операционной системы.

- Для виртуальной машины Linux используйте SSH для подключения к виртуальной машине и извлечения сообщения дня, настроенного сценарием:

  ![Снимок экрана с обновленным ежедневным сообщением.](./media/arc-vm-extension-custom-script/daily-message.png)

- Подключитесь к виртуальной машине Windows по протоколу RDP и убедитесь, что установлено дополнительное программное обеспечение: Microsoft погранично, 7-Zip и Visual Studio Code.

  ![Снимок экрана с установленным дополнительным программным обеспечением.](./media/arc-vm-extension-custom-script/additional-software.png)

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

Удалите виртуальные машины из каждой среды, следуя инструкциям по уничтожению, приведенным в каждом из руководств.

- Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
- [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
- [VMware VSPHERE виртуальной машины Ubuntu](./vmware-terraform-ubuntu.md) и [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
- [Vagrant Ubuntu](./local-vagrant-ubuntu.md) и [Vagrant Windows Box](./local-vagrant-windows.md)
