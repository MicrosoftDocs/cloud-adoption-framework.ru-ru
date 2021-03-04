---
title: Подключение существующего сервера Linux к службе "Дуга Azure"
description: Подключите существующий сервер Linux к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 6961d80e893d59361ae0c9475972ddfb0e4f87f5
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101797342"
---
# <a name="connect-an-existing-linux-server-to-azure-arc"></a>Подключение существующего сервера Linux к службе "Дуга Azure"

В этой статье приводятся рекомендации по подключению сервера Linux к службе "Дуга Azure" с помощью простого сценария оболочки.

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

3. Создайте новую группу ресурсов Azure для своих серверов.

    ![Снимок экрана портал Azure с пустой группой ресурсов.](./media/onboard-server/linux-resource-group.png)

4. Скачайте [`az-connect-linux`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/scripts/az_connect_linux.sh) сценарий оболочки.

5. Измените переменные среды в соответствии с используемой средой.

    ![Снимок экрана переменных среды для изменения.](./media/onboard-server/linux-variables.png)

6. Скопируйте сценарий на назначенный сервер, используя предпочтительное средство выбора (или скопируйте или вставьте сценарий в новый файл на сервере). В следующем примере показано, как скопировать скрипт из macOS на сервер с помощью `scp` .

    ![Снимок экрана скрипта SCP.](./media/onboard-server/linux-scp.png)

## <a name="deployment"></a>Развертывание

Запустите скрипт с помощью `. ./az-connect-linux.sh` команды.

> [!NOTE]
> Дополнительной точкой является то, что в скрипте есть функция *экспорта* и необходимо, чтобы переменных был экспортирован в тот же сеанс оболочки, что и остальные команды.

После успешного завершения вы получите сервер Linux, подключенный как новый ресурс дуги Azure в группе ресурсов.

![Снимок экрана запуска сценария Linux "az_connect".](./media/onboard-server/az-connect-linux.png)

![Снимок экрана ресурса с поддержкой дуги Azure в портал Azure.](./media/onboard-server/linux-resource.png)

![Снимок экрана с подробными сведениями о ресурсе с поддержкой дуги Azure в портал Azure.](./media/onboard-server/linux-resource-detail.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить сервер, выберите сервер и удалите его из портал Azure.

![Снимок экрана с параметром удаления ресурса в портал Azure.](./media/onboard-server/linux-delete-resource.png)

Чтобы удалить все развертывание, удалите группу ресурсов Azure из портал Azure.

![Снимок экрана с параметром удаления группы ресурсов с помощью портал Azure.](./media/onboard-server/linux-delete-resource-group.png)
