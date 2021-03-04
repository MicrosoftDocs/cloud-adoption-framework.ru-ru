---
title: Использование шаблона Azure Resource Manager для развертывания и подключения виртуальной машины Azure к службе "Дуга Azure"
description: Используйте шаблон Azure Resource Manager для развертывания и подключения виртуальной машины Azure к службе "Дуга" Azure.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: b4dd445fd3ac8e9dc9677ebcae0933cf4bf386e1
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102112132"
---
# <a name="use-an-azure-resource-manager-template-to-deploy-and-connect-an-azure-virtual-machine-to-azure-arc"></a>Использование шаблона Azure Resource Manager для развертывания и подключения виртуальной машины Azure к службе "Дуга Azure"

В этой статье приводятся рекомендации по использованию [шаблона Azure Resource Manager (шаблон ARM)](/azure/azure-resource-manager/templates/overview) для автоматической адаптации виртуальной машины Azure (виртуальной машины Azure) под Windows к службе "Дуга Azure". Указанный шаблон ARM отвечает за создание ресурсов Azure и выполнение встроенного сценария Azure Arc на виртуальной машине.

По умолчанию виртуальные машины Azure используют [службу метаданных экземпляров Azure (IMDS)](/azure/virtual-machines/windows/instance-metadata-service) . При проецировании виртуальной машины Azure в качестве сервера с поддержкой Arc Azure создается *конфликт* , который не позволит представить ресурсы сервера Arc Azure в качестве одного при использовании IMDS. Вместо этого сервер дуги Azure по-прежнему будет действовать как собственная виртуальная машина Azure.

В этом руководства вы сможете использовать и подключать виртуальные машины Azure к службе "Дуга" Azure **только в демонстрационных целях**. У вас будет возможность имитировать сервер, развернутый за пределами Azure, например локально или на других облачных платформах.

> [!NOTE]
> Виртуальная машина Azure не должна быть сервером с поддержкой дуги Azure. Приведенный ниже сценарий не поддерживается и должен использоваться только для демонстрационных и тестовых целей.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. Подписка Azure. Если у вас нет подписки Azure, вы можете [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/).

4. Создайте субъект-службу Azure.

    Чтобы развернуть ресурсы Azure с помощью шаблона ARM, требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

## <a name="automation-flow"></a>Поток автоматизации

Чтобы ознакомиться с автоматизацией и ходом развертывания, см. описание ниже.

1. Пользователь редактирует файл параметров шаблона ARM (один раз изменить). Эти значения параметров используются во время развертывания.

2. Шаблон ARM включает расширение пользовательских сценариев виртуальной машины Azure, которое развертывает [`install_arc_agent.ps1`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/windows/arm_template/scripts/install_arc_agent.ps1) скрипт PowerShell.

3. Чтобы разрешить успешное проецирование виртуальной машины Azure в качестве сервера с поддержкой дуги Azure, сценарий будет выполнять следующие действия:

    1. Задайте локальные переменные среды ОС.

    2. Создайте локальный скрипт входа в ОС с именем `LogonScript.ps1` . Вот что делает этот сценарий:

        - Создайте `LogonScript.log` файл.

        - Останавливает и отключает службу гостевого агента Windows Azure.

        - Создайте новое правило брандмауэра Windows, чтобы заблокировать исходящий трафик Azure IMDS на `169.254.169.254` Удаленный адрес.

        - Отмените регистрацию запланированной задачи Windows "скрипт входа", чтобы она не запускалась после первого входа.

    3. Отключите и запретите запуск диспетчер сервера Windows при запуске.

4. Пользователь подключается по протоколу RDP к виртуальной машине Windows, которая начинает работать `LogonScript.ps1` и подключает виртуальную машину к службе "Дуга Azure".

## <a name="deployment"></a>Развертывание

Как уже упоминалось, в этом развертывании будут использоваться шаблоны ARM. Будет развернут один шаблон, отвечающий за создание всех ресурсов Azure в одной группе ресурсов и подключение созданной виртуальной машины к службе "Дуга Azure".

1. Перед развертыванием шаблона ARM Войдите в Azure, используя Azure CLI с помощью `az login` команды.

2. Развертывание использует файл параметров шаблона ARM. Перед запуском развертывания измените файл, [`azuredeploy.parameters.json`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/windows/arm_template/azuredeploy.parameters.json) расположенный в локальной папке клонированного репозитория. Пример файла параметров находится [здесь](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/windows/arm_template/azuredeploy.parameters.example.json).

3. Чтобы развернуть шаблон ARM, перейдите к папке локального клонированного [развертывания](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/azure/windows/arm_template) и выполните следующую команду:

    ```console
    az group create --name <Name of the Azure resource group> --location <Azure Region> --tags "Project=jumpstart_azure_arc_servers"
    az deployment group create \
    --resource-group <Name of the Azure resource group> \
    --name <The name of this deployment> \
    --template-uri https://raw.githubusercontent.com/microsoft/azure-arc/main/azure_arc_servers_jumpstart/azure/windows/arm_template/azuredeploy.json \
    --parameters <The `azuredeploy.parameters.json` parameters file location>
    ```

    > [!NOTE]
    > Убедитесь, что используется имя группы ресурсов Azure, совпадающее с именем, использованным в `azuredeploy.parameters.json` файле.

    Пример:

    ```console
    az group create --name Arc-Servers-Win-Demo --location "East US" --tags "Project=jumpstart_azure_arc_servers"
    az deployment group create \
    --resource-group Arc-Servers-Win-Demo \
    --name arcwinsrvdemo \
    --template-uri https://raw.githubusercontent.com/microsoft/azure-arc/main/azure_arc_servers_jumpstart/azure/windows/arm_template/azuredeploy.json \
    --parameters azuredeploy.parameters.json
    ```

4. После подготовки ресурсов Azure их можно просмотреть в портал Azure.

    ![Снимок экрана с выходными данными из шаблона ARM.](./media/arm-template/template-windows-output.png)

    ![Ресурсы снимка экрана в группе ресурсов.](./media/arm-template/template-windows-resources.png)

## <a name="windows-sign-in-and-post-deployment"></a>Вход в Windows и после развертывания

1. Теперь, когда виртуальная машина Windows Server создана, ее можно подключить следующим шагом. Используя его общедоступный IP-адрес, подключитесь к виртуальной машине по протоколу RDP.

    ![Снимок экрана общедоступного IP-адреса виртуальной машины Azure.](./media/arm-template/template-windows-ip.png)

2. При первом входе в систему, как упоминалось в разделе " [поток автоматизации](#automation-flow) ", будет выполнен сценарий входа. Этот скрипт создается как часть процесса автоматического развертывания.

3. Позвольте скрипту запуститься и **не закрывать** сеанс PowerShell. Сеанс закрывается автоматически после завершения.

    > [!NOTE]
    > Время выполнения сценария — ~ 1-2 минут.

    ![Снимок экрана одного типа выходных данных сценария.](./media/arm-template/template-windows-script-1.png)

    ![Снимок экрана второго типа выходных данных сценария.](./media/arm-template/template-windows-script-2.png)

    ![Снимок экрана третьего типа выходных данных сценария.](./media/arm-template/template-windows-script-3.png)

    ![Снимок экрана четвертого типа выходных данных сценария.](./media/arm-template/template-windows-script-4.png)

4. После успешного завершения в группу ресурсов будет добавлен новый сервер с поддержкой Arc Azure.

![Снимок экрана группы ресурсов с сервера с поддержкой дуги Azure.](./media/arm-template/template-windows-resource-gp.png)

![Снимок экрана с подробными сведениями с сервера с поддержкой Arc Azure.](./media/arm-template/template-windows-server-details.png)

## <a name="cleanup"></a>Очистка

Чтобы удалить все развертывание, удалите группу ресурсов из портал Azure.

![Снимок экрана, посвященный удалению группы ресурсов.](./media/arm-template/template-windows-delete.png)
