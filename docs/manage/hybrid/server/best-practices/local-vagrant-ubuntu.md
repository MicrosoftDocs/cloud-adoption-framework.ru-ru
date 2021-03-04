---
title: Развертывание локального сервера Ubuntu, размещенного на Vagrant, и его подключение к службе "Дуга Azure"
description: Разверните локальный сервер Ubuntu, размещенный с помощью Vagrant, и подключите его к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 367b08aa62b68120def9e9788129cbe21b483d6c
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102111979"
---
# <a name="deploy-a-local-ubuntu-server-hosted-with-vagrant-and-connect-it-to-azure-arc"></a>Развертывание локального сервера Ubuntu, размещенного на Vagrant, и его подключение к службе "Дуга Azure"

В этой статье приводятся рекомендации по развертыванию локальной виртуальной машины **Ubuntu** с помощью [Vagrant](https://www.vagrantup.com/) и ее подключению в качестве ресурса сервера с поддержкой ARC в Azure.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. Vagrant полагается на базовую низкоуровневую оболочку. Для этого руководством мы будем использовать "Oracle VM VirtualBox".

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

5. Файл Vagrant выполняет сценарий в ОС виртуальной машины для установки всех необходимых артефактов и вставки переменных среды. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/local/vagrant/ubuntu/scripts/vars.sh) сценарий оболочки в соответствии с созданным субъектом-службой Azure.

    - `subscriptionId` — Идентификатор подписки Azure;
    - `appId` = имя субъекта-службы Azure
    - `password` — пароль субъекта-службы Azure.
    - `tenantId` — Идентификатор клиента Azure.
    - `resourceGroup` = Имя группы ресурсов Azure
    - `location` = Регион Azure

## <a name="deployment"></a>Развертывание

Как и любое Vagrant развертывание, требуется поле [vagrantfile.](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/local/vagrant/ubuntu/Vagrantfile) и [Vagrant](https://www.vagrantup.com/docs/boxes) . На высоком уровне развертывание будет следующим:

- Скачайте [Vagrant](https://app.vagrantup.com/ubuntu/boxes/xenial64) файл образа Ubuntu 16,04
- Выполнение скрипта установки

После редактирования `scripts/vars.sh` сценария в соответствии с используемой средой в `Vagrantfile` папке выполните команду `vagrant up` . Поскольку это первый раз при создании виртуальной машины, первый запуск будет выполняться **намного медленнее** , чем раньше, поскольку развертывание загружает поле Ubuntu в первый раз.

![Снимок экрана команды "Vagrant Up".](./media/local-vagrant/vagrant-ubuntu-vagrant-up.png)

После завершения загрузки начинается подготовка. Как показано на следующем снимке экрана, процесс занимает не более трех минут.

![Снимок экрана завершенной команды "Vagrant Up".](./media/local-vagrant/vagrant-ubuntu-vagrant-up-complete.png)

После завершения будет развернута локальная виртуальная машина Ubuntu, подключенная как новый сервер с поддержкой ARC в Azure, в новой группе ресурсов.

![Снимок экрана сервера с поддержкой дуги Azure в портал Azure.](./media/local-vagrant/vagrant-ubuntu-server.png)

![Снимок экрана с подробными сведениями из сервера с поддержкой Arc Azure в портал Azure.](./media/local-vagrant/vagrant-ubuntu-server-details.png)

## <a name="semi-automated-deployment-optional"></a>Частично автоматизированное развертывание (необязательно)

Последний шаг — зарегистрировать виртуальную машину в качестве нового ресурса сервера с поддержкой дуги Azure.

![Еще один снимок экрана команды "Vagrant Up".](./media/local-vagrant/vagrant-ubuntu-vagrant-up-2.png)

Если вы хотите получить демонстрацию или управлять фактическим процессом регистрации, выполните следующие действия.

1. В [`install_arc_agent`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/local/vagrant/ubuntu/scripts/install_arc_agent.sh) скрипте оболочки закомментируйте `run connect command` раздел и сохраните файл. Можно также закомментировать или изменить создание группы ресурсов.

    ![Снимок экрана команды "азкмажент Connect".](./media/local-vagrant/vagrant-ubuntu-azcmagent.png)

    ![Снимок экрана команды "az Group Create".](./media/local-vagrant/vagrant-ubuntu-azgroup-create.png)

2. Подключитесь к виртуальной машине по протоколу SSH с помощью `vagrant ssh` команды.

    ![Снимок экрана ключа SSH, подключающегося к компьютеру Vagrant.](./media/local-vagrant/vagrant-ubuntu-ssh.png)

3. Выполните ту же `azcmagent connect` команду, с которой были внесены комментарии, используя переменные среды.

    ![Еще один снимок экрана команды "азкмажент Connect".](./media/local-vagrant/vagrant-ubuntu-azcmagent-2.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить все развертывание, выполните `vagrant destroy -f` команду. Vagrantfile. включает `before: destroy` триггер Vagrant, который будет выполнять сценарий для удаления группы ресурсов Azure перед уничтожением реальной виртуальной машины.

![Снимок экрана команды "Vagrant Destroy".](./media/local-vagrant/vagrant-ubuntu-vagrant-destroy.png)
