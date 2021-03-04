---
title: Развертывание локального экземпляра Windows Server, размещенного на Vagrant, и подключение его к службе "Дуга Azure"
description: Разверните локальный экземпляр Windows Server, размещенный на Vagrant, и подключите его к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: f2a0dc375146f9f35bb3b1d91cf2cb039510fb56
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101797387"
---
# <a name="deploy-a-local-windows-server-instance-hosted-by-vagrant-and-connect-it-to-azure-arc"></a>Развертывание локального экземпляра Windows Server, размещенного на Vagrant, и подключение его к службе "Дуга Azure"

В следующей статье приводятся рекомендации по развертыванию локальной виртуальной машины **Windows 10** с помощью [Vagrant](https://www.vagrantup.com/) и ее подключению в качестве ресурса сервера с поддержкой ARC в Azure.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. Vagrant полагается на базовую низкоуровневую оболочку. Для этого руководством мы будем использовать виртуальную машину Oracle VirtualBox.

    1. Установите [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

        - Если вы являетесь пользователем macOS, выполните команду `brew cask install virtualbox`
        - Если вы являетесь пользователем Windows, вы можете использовать [шоколадный пакет](https://chocolatey.org/packages/virtualbox) .
        - Если вы являетесь пользователем Linux, то все методы установки пакета можно найти [здесь](https://www.virtualbox.org/wiki/Linux_Downloads) .

    2. Установка [Vagrant](https://www.vagrantup.com/docs/installation)

        - Если вы являетесь пользователем macOS, выполните команду `brew cask install vagrant`
        - Если вы являетесь пользователем Windows, вы можете использовать [шоколадный пакет](https://chocolatey.org/packages/vagrant) .
        - Если вы являетесь пользователем Linux, посмотрите [здесь](https://www.vagrantup.com/downloads)

4. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину Vagrant к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

- Vagrantfile. выполняет сценарий в ОС виртуальной машины для установки всех необходимых артефактов и вставки переменных среды. Измените [`scripts/vars.ps1`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/local/vagrant/windows/scripts/vars.ps1) скрипт PowerShell в соответствии с созданным субъектом-службой Azure.

  - `subscriptionId` — Идентификатор подписки Azure;
  - `appId` = Имя субъекта-службы Azure
  - `password` — Пароль субъекта-службы Azure.
  - `tenantId` — Идентификатор клиента Azure.
  - `resourceGroup` = Имя группы ресурсов Azure
  - `location` = Регион Azure

## <a name="deployment"></a>Развертывание

Как и любое Vagrant развертывание, требуется поле [vagrantfile.](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/local/vagrant/windows/Vagrantfile) и [Vagrant](https://www.vagrantup.com/docs/boxes) . На высоком уровне развертывание будет следующим:

- Скачивание [Vagrant](https://app.vagrantup.com/StefanScherer/boxes/windows_10) файла образа Windows 10
- Выполнение скрипта установки Azure Arc

После редактирования `scripts/vars.ps1` сценария в соответствии с используемой средой в `Vagrantfile` папке выполните команду `vagrant up` . Так как вы впервые создаете виртуальную машину, первый запуск будет выполняться **намного медленнее** , чем в последующих. Это связано с тем, что развертывание загружает Windows 10 в первый раз.

![Снимок экрана: запуск команды "Vagrant Up".](./media/local-vagrant/vagrant-windows-cmd.png)

После завершения скачивания начнется фактическая подготовка. Как показано на следующем снимке экрана, процесс может занять от 7 до 10 минут.

![Снимок экрана завершенной команды "Vagrant Up".](./media/local-vagrant/vagrant-windows-complete.png)

После завершения развертывания будет развернута локальная виртуальная машина Windows 10, подключенная как новый сервер с поддержкой ARC в Azure в новой группе ресурсов.

![Снимок экрана сервера с поддержкой дуги Azure в портал Azure.](./media/local-vagrant/vagrant-windows-server.png)

![Снимок экрана с подробными сведениями из сервера с поддержкой Arc Azure в портал Azure.](./media/local-vagrant/vagrant-windows-server-details.png)

## <a name="semi-automated-deployment-optional"></a>Частично автоматизированное развертывание (необязательно)

Последний этап выполнения — зарегистрировать виртуальную машину в качестве нового ресурса сервера с поддержкой дуги Azure.

![Еще один снимок экрана завершенной команды "Vagrant Up".](./media/local-vagrant/vagrant-windows-complete-2.png)

Если вы хотите получить демонстрацию и управлять фактическим процессом регистрации, выполните следующие действия.

1. В [`install_arc_agent`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/local/vagrant/windows/scripts/install_arc_agent.ps1) скрипте PowerShell закомментируйте `run connect command` раздел и сохраните файл. Можно также закомментировать или изменить создание группы ресурсов.

    ![Снимок экрана сценария PowerShell "install_arc_agent".](./media/local-vagrant/vagrant-windows-install-arc-agent.png)

    ![Снимок экрана команды "az Group Create".](./media/local-vagrant/vagrant-windows-az-group-create.png)

2. Подключитесь к виртуальной машине по протоколу RDP с помощью `vagrant rdp` команды. Используйте `vagrant/vagrant` в качестве имени пользователя и пароля.

    ![Снимок экрана: доступ к серверу Vagrant с помощью протокола Удаленный рабочий стол (Майкрософт).](./media/local-vagrant/vagrant-windows-rdp.png)

3. Откройте интегрированную среду сценариев PowerShell **от имени администратора** и измените `C:\runtime\vars.ps1` файл с помощью переменных среды.

    ![Снимок экрана интегрированной среды сценариев Windows PowerShell.](./media/local-vagrant/vagrant-windows-ise.png)

4. Вставьте `Invoke-Expression "C:\runtime\vars.ps1"` команду, `az group create --location $env:location --name $env:resourceGroup --subscription $env:subscriptionId` команду и ту же команду и `azcmagent connect` выполните сценарий.

    ![Снимок экрана ИНТЕГРИРОВАНной среды сценариев PowerShell с запуском скрипта.](./media/local-vagrant/vagrant-windows-ise-script.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить все развертывание, выполните `vagrant destroy -f` команду. Vagrantfile. включает `before: destroy` триггер Vagrant, который запускает команду для удаления группы ресурсов Azure перед уничтожением реальной виртуальной машины.

![Снимок экрана команды "Vagrant Destroy".](./media/local-vagrant/vagrant-windows-vagrant-destroy.png)
