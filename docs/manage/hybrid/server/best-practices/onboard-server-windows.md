---
title: Подключение существующего экземпляра Windows Server к службе "Дуга Azure"
description: Подключите существующий экземпляр Windows Server к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 91bbb5af82efc6e54c414c7a6a9e80a72e06ce2d
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102114342"
---
# <a name="connect-an-existing-windows-server-instance-to-azure-arc"></a>Подключение существующего экземпляра Windows Server к службе "Дуга Azure"

В этой статье приводятся рекомендации по подключению компьютера Windows к службе "Дуга Azure" с помощью простого сценария PowerShell.

## <a name="prerequisites"></a>Предварительные требования

1. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

2. Создайте субъект-службу Azure.

    Чтобы подключить сервер к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

3. Создайте новую группу ресурсов Azure для своих компьютеров.

    ![Снимок экрана пустой группы ресурсов в портал Azure.](./media/onboard-server/windows-resource-group.png)

4. Скачайте [`az_connect_win.ps1`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/scripts/az_connect_win.ps1) сценарий PowerShell.

5. Измените переменные среды в соответствии со своей средой и скопируйте сценарий на указанный компьютер.

    ![Снимок экрана переменных среды для изменения.](./media/onboard-server/windows-variables.png)

## <a name="deployment"></a>Развертывание

На указанном компьютере откройте интегрированную среду сценариев PowerShell **от имени администратора** и запустите сценарий. Обратите внимание, что сценарий используется в `$env:ProgramFiles` качестве пути установки агента, поэтому **не используйте PowerShell ISE (x86)**.

![Снимок экрана команды "азкмажент Connect".](./media/onboard-server/azcmagent.png)

![Снимок экрана сценария Windows "az_connect_win.ps1".](./media/onboard-server/az-connect-windows-2.png)

После завершения вы получите экземпляр Windows Server, подключенный как новый ресурс дуги Azure в группе ресурсов.

![Снимок экрана с выполняемым сценарием Windows "az_connect_win.ps1".](./media/onboard-server/az-connect-windows.png)

![Снимок экрана ресурса с поддержкой дуги Azure в портал Azure.](./media/onboard-server/windows-resource.png)

![Снимок экрана с подробными сведениями о ресурсе с поддержкой дуги Azure в портал Azure.](./media/onboard-server/windows-resource-detail.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить сервер, выберите сервер и удалите его из портал Azure.

![Снимок экрана с параметром удаления ресурса в портал Azure.](./media/onboard-server/windows-delete-resource.png)

Чтобы удалить все развертывание, удалите группу ресурсов Azure из портал Azure.

![Снимок экрана с параметром удаления группы ресурсов с помощью портал Azure.](./media/onboard-server/windows-delete-resource-group.png)
