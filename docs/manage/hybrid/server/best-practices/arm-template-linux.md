---
title: Использование шаблона Azure Resource Manager для развертывания и подключения виртуальной машины Ubuntu к службе "Дуга Azure"
description: Используйте шаблон Azure Resource Manager, чтобы развернуть виртуальную машину Ubuntu и подключить ее к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 50fc9c721716bd7be378db247daf3df1319f7d75
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101798373"
---
# <a name="use-an-azure-resource-manager-template-to-deploy-and-connect-an-ubuntu-virtual-machine-to-azure-arc"></a>Использование шаблона Azure Resource Manager для развертывания и подключения виртуальной машины Ubuntu к службе "Дуга Azure"

В этой статье приводятся рекомендации по использованию [шаблона ARM](/azure/azure-resource-manager/templates/overview) шаблона Azure Resource Manager для автоматической адаптации виртуальной машины Ubuntu к службе "Дуга Azure". Указанный шаблон ARM отвечает за создание ресурсов Azure и выполнение встроенного сценария Azure Arc на виртуальной машине.

По умолчанию виртуальные машины Azure используют [службу метаданных экземпляров Azure (IMDS)](/azure/virtual-machines/windows/instance-metadata-service) . При проецировании виртуальной машины Azure в качестве сервера с поддержкой Arc Azure создается *конфликт* , который не позволит представить ресурсы сервера Arc Azure в качестве одного при использовании IMDS. Вместо этого сервер дуги Azure по-прежнему будет действовать как собственная виртуальная машина Azure.

В этом руководства вы сможете использовать и подключать виртуальные машины Azure к службе "Дуга" Azure **только в демонстрационных целях**. Вы сможете имитировать сервер, развернутый за пределами Azure, например локально или на других облачных платформах.

> [!NOTE]
> Не ожидается, что виртуальная машина Azure будет вычислена как сервер с поддержкой Arc Azure. **Приведенный ниже сценарий не поддерживается и должен использоваться только для демонстрационных и тестовых целей.**

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. **Подписка Azure:** Если у вас нет подписки Azure, вы можете [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/).

4. Создайте субъект-службу Azure.

    Чтобы развернуть ресурсы Azure с помощью шаблона ARM, требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

Чтобы ознакомиться с автоматизацией и ходом развертывания, см. описание ниже.

1. Пользователь редактирует файл параметров шаблона ARM (одноразовое изменение). Эти значения параметров используются во время развертывания.

2. Шаблон ARM включает расширение пользовательских сценариев виртуальной машины Azure, которое развертывает [`install_arc_agent.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/linux/arm_template/scripts/install_arc_agent.sh) скрипт оболочки.

3. Чтобы разрешить успешное проецирование виртуальной машины Azure в качестве сервера с поддержкой дуги Azure, сценарий будет выполнять следующие действия:

    1. Задайте локальные переменные среды ОС.

    2. Создайте `~/.bash-profile` файл, который будет инициализирован при первом входе пользователя для настройки среды. Вот что делает этот сценарий:

        - Останавливает и отключает службу гостевого агента Azure для Linux.

        - Создайте новое правило брандмауэра ОС, чтобы заблокировать исходящий трафик Azure IMDS на `169.254.169.254` Удаленный адрес.

        - Установите агент подключенного компьютера ARC в Azure.

        - Удалите `~/.bash-profile` файл, чтобы он не запускался после первого входа в систему.

4. Пользователь будет подключаться к виртуальной машине Linux по протоколу SSH, которая начнет `~/.bash-profile` выполнение скрипта и будет подключать виртуальную машину к службе "Дуга Azure".

    > [!NOTE]
    >  [`install_arc_agent.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/linux/arm_template/scripts/install_arc_agent.sh)Сценарий оболочки включает БРАНДМАУЭР ОС и настраивает новые правила для входящих и исходящих подключений. По умолчанию весь входящий и исходящий трафик будет разрешен, за исключением блокировки исходящего трафика Azure IMDS на `169.254.169.254` Удаленный адрес.

## <a name="deployment"></a>Развертывание

Как уже упоминалось, в этом развертывании будут использоваться шаблоны ARM. Будет развернут один шаблон, отвечающий за создание всех ресурсов Azure в одной группе ресурсов и подключение созданной виртуальной машины к службе "Дуга Azure".

1. Перед развертыванием шаблона ARM Войдите в систему, используя Azure CLI с помощью `az login` команды.

2. Развертывание использует файл параметров шаблона ARM. Перед запуском развертывания измените файл, [`azuredeploy.parameters.json`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/linux/arm_template/azuredeploy.parameters.json) расположенный в локальной папке клонированного репозитория. Пример файла параметров находится [здесь](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azure/linux/arm_template/azuredeploy.parameters.example.json).

3. Чтобы развернуть шаблон ARM, перейдите к папке локального клонированного [развертывания](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/azure/linux/arm_template) и выполните следующую команду:

    ```console
    az group create --name <Name of the Azure resource group> --location <Azure region> --tags "Project=jumpstart-azure-arc-servers"
    az deployment group create \
    --resource-group <Name of the Azure resource group> \
    --name <The name of this deployment> \
    --template-uri https://raw.githubusercontent.com/microsoft/azure-arc/main/azure_arc_servers_jumpstart/azure/linux/arm_template/azuredeploy.json \
    --parameters <The `azuredeploy.parameters.json` parameters file location>
    ```

    > [!NOTE]
    > Обязательно используйте имя группы ресурсов Azure, совпадающее с именем, которое использовалось в `azuredeploy.parameters.json` файле.

    Пример.

    ```console
    az group create --name Arc-Servers-Linux-Demo --location "westeurope" --tags "Project=jumpstart-azure-arc-servers"
    az deployment group create \
    --resource-group Arc-Servers-Linux-Demo \
    --name arclinuxdemo \
    --template-uri https://raw.githubusercontent.com/microsoft/azure-arc/main/azure_arc_servers_jumpstart/azure/linux/arm_template/azuredeploy.json \
    --parameters azuredeploy.parameters.json
    ```

4. После подготовки ресурсов Azure они отобразятся в портал Azure.

    ![Снимок экрана с выходными данными из шаблона ARM.](./media/arm-template/template-linux-output.png)

    ![Ресурсы снимка экрана в группе ресурсов.](./media/arm-template/template-linux-resources.png)

## <a name="linux-sign-in-and-post-deployment"></a>Вход в Linux и после развертывания

1. Теперь, когда виртуальная машина Linux создана, к ней будет подключен следующий шаг. Используя его общедоступный IP-адрес, подключитесь к виртуальной машине по протоколу SSH.

    ![Снимок экрана общедоступного IP-адреса виртуальной машины Azure.](./media/arm-template/template-linux-ip.png)

2. При первом входе в систему, как упоминалось в разделе о [потоке автоматизации](#automation-flow) , будет выполнен сценарий входа. Этот скрипт был создан в рамках процесса автоматического развертывания.

3. Дайте скрипту запуск и **не закрывайте** сеанс SSH. Сеанс будет закрыт автоматически после завершения.

    ![Снимок экрана одного типа выходных данных сценария.](./media/arm-template/template-linux-script-1.png)

    ![Снимок экрана другого типа выходных данных сценария.](./media/arm-template/template-linux-script-2.png)

    ![Снимок экрана третьего типа выходных данных сценария.](./media/arm-template/template-linux-script-3.png)

4. После успешного завершения в группу ресурсов будет добавлен новый сервер с поддержкой Arc Azure.

    ![Снимок экрана группы ресурсов с сервера с поддержкой дуги Azure.](./media/arm-template/template-linux-resource-gp.png)

    ![Снимок экрана с подробными сведениями с сервера с поддержкой Arc Azure.](./media/arm-template/template-linux-server-details.png)

## <a name="cleanup"></a>Очистка

Чтобы удалить все развертывание, удалите группу ресурсов из портал Azure.

![Снимок экрана: Удаление группы ресурсов](./media/arm-template/template-linux-delete.png)
