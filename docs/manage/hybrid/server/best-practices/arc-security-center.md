---
title: Подключение серверов с поддержкой ARC в Azure к центру безопасности Azure
description: Узнайте, как подключить сервер с поддержкой Arc Azure к центру безопасности Azure.
author: likamrat
ms.author: brblanch
ms.date: 01/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 0829a67a8ddc00d3db73ff2ac67d781b7e52f01e
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799228"
---
# <a name="connect-azure-arc-enabled-servers-to-azure-security-center"></a>Подключение серверов с поддержкой ARC в Azure к центру безопасности Azure

В этой статье содержатся рекомендации по подключению сервера с поддержкой Arc Azure к [центру безопасности Azure (центр безопасности Azure)](/azure/security-center/). Это поможет вам начать сбор связанных с безопасностью конфигураций и журналов событий, чтобы вы могли рекомендовать действия и улучшить общую безопасность Azure.

В следующих процедурах вы включаете и настраиваете центр безопасности Azure уровня "Стандартный" в подписке Azure. Это обеспечивает расширенные возможности защиты от угроз (ATP) и функции обнаружения. Процесс включает в себя следующее:

- Настройка Log Analytics рабочей области, в которой выполняется статистическая обработка журналов и событий для анализа.
- Назначение политик безопасности по умолчанию для центра безопасности.
- Ознакомьтесь с рекомендациями центра безопасности Azure.
- Применение рекомендуемых конфигураций на серверах с поддержкой дуги Azure с помощью **быстрого исправления исправлений** .

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
    git clone https://github.com/microsoft/azure_arc
    ```

2. Как уже упоминалось, это руководства начинается в том месте, где вы уже развернули и подключили виртуальные машины или серверы без операционной системы в дугу Azure. В этом сценарии используется экземпляр Google Cloud Platform (обеспечить), который уже подключен к службе "Дуга Azure" и отображается как ресурс в Azure. Как показано на следующих снимках экрана:

    ![Снимок экрана сервера с поддержкой дуги Azure в портал Azure.](./media/arc-security-center/arc-overview.png)

    ![Снимок экрана с подробными сведениями из сервера с поддержкой Arc Azure в портал Azure.](./media/arc-security-center/arc-status.png)

3. [Установите или обновите Azure CLI](/cli/azure/install-azure-cli). Azure CLI должна работать под управлением версии 2,7 или более поздней. Используйте `az --version` для проверки текущей установленной версии.

4. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину или сервер без операционной системы к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

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

## <a name="onboard-azure-security-center"></a>Подключение центра безопасности Azure

1. Данные, собираемые центром безопасности Azure, хранятся в Log Analytics рабочей области. Можно использовать значение по умолчанию, созданное центром безопасности Azure, или пользователь, созданный вами. Если вы хотите создать выделенную рабочую область, можно автоматизировать развертывание, изменив [файл параметров](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/securitycenter/arm/log_analytics-template.parameters.json)шаблона Azure Resource Manager (шаблон ARM), указав имя и расположение рабочей области:

   ![Снимок экрана шаблона ARM.](./media/arc-security-center/arm-template.png)

2. Чтобы развернуть шаблон ARM, перейдите в [папку Deployment](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/securitycenter/arm) и выполните следующую команду:

   ```console
   az deployment group create --resource-group <Name of the Azure resource group> \
   --template-file <The `log_analytics-template.json` template file location> \
   --parameters <The `log_analytics-template.parameters.json` template file location>
   ```

3. Если вы планируете использовать определенную пользователем рабочую область, следует указать центру безопасности, что он будет использоваться вместо по умолчанию, используя следующую команду:

   ```console
   az security workspace-setting create --name default \
   --target-workspace '/subscriptions/<Your subscription ID>/resourceGroups/<Name of the Azure resource group>/providers/Microsoft.OperationalInsights/workspaces/<Name of the Log Analytics Workspace>'
   ```

4. Выберите уровень центра безопасности Azure. Уровень "бесплатный" включен для всех подписок Azure по умолчанию и обеспечит непрерывную оценку безопасности и рекомендации по обеспечению безопасности. В этом руководство вы используете уровень "Стандартный" для виртуальных машин Azure, которые расширяют возможности унифицированного управления безопасностью и защиты от угроз в гибридных облачных рабочих нагрузках. Чтобы включить уровень "Стандартный" центра безопасности Azure для виртуальных машин, выполните следующую команду:

    ```console
    az security pricing create -n VirtualMachines --tier 'standard'
    ```

5. Назначьте инициативу политики центра безопасности по умолчанию. Центр безопасности Azure предоставляет свои рекомендации по безопасности на основе политик. Существует специальная инициатива, которая группирует политики центра безопасности с ИДЕНТИФИКАТОРом определения `1f3afdf9-d0c9-4c3d-847f-89da613e70a8` . Следующая команда назначает инициативу центра безопасности Azure своей подписке.

    ```console
    az policy assignment create --name 'Azure Security Center Default <Your subscription ID>' \
    --scope '/subscriptions/<Your subscription ID>' \
    --policy-set-definition '1f3afdf9-d0c9-4c3d-847f-89da613e70a8'
    ```

## <a name="azure-arc-and-azure-security-center-integration"></a>Интеграция Azure Arc и центра безопасности Azure

После успешного подключения центра безопасности Azure вы получите рекомендации по защите ресурсов, включая серверы с поддержкой дуги Azure. Центр безопасности Azure периодически анализирует состояние безопасности ресурсов Azure для выявления потенциальных уязвимостей системы безопасности.

В разделе " **вычисление & приложений** " в разделе " **серверы & виртуальных машин**" в центре безопасности Azure представлен обзор всех обнаруженных рекомендаций по безопасности для виртуальных машин и компьютеров, включая виртуальные машины Azure, классические виртуальные машины Azure, серверы и компьютеры ARC в Azure.

![Снимок экрана: * * вычисление & приложений * * в центре безопасности Azure.](./media/arc-security-center/compute-apps.png)

На серверах с поддержкой Arc Azure центр безопасности Azure рекомендует установить агент Log Analytics. Каждая рекомендация также включает:

- Краткое описание рекомендации.
- Влияние на показатель безопасности, в данном случае с состоянием **Высокая**.
- Действия по исправлению, которые необходимо выполнить для реализации рекомендации.

Для получения конкретных рекомендаций, как на следующем снимке экрана, вы также получите **Быстрое исправление** , позволяющее быстро исправлять рекомендацию по нескольким ресурсам.

  ![Снимок экрана с рекомендацией центра безопасности Azure для сервера с поддержкой ARC в Azure.](./media/arc-security-center/recommendation-quick-fix.png)

  ![Снимок экрана рекомендации центра безопасности Azure по установке Log Analytics.](./media/arc-security-center/recommendation-remediate.png)

Следующее **Быстрое исправление** исправления использует шаблон ARM для развертывания расширения Microsoft Monitoring Agent на компьютере Arc Azure.

  ![Снимок экрана центра безопасности Azure * * быстрое исправление * * шаблон ARM.](./media/arc-security-center/quick-fix-template.png)

Вы можете активировать исправление с помощью шаблона ARM на панели мониторинга центра безопасности Azure, выбрав Log Analytics рабочую область, используемую для центра безопасности Azure, а затем выбрав вариант **исправлять 1 ресурс**.

  ![Снимок экрана, посвященный запуску шага исправления в центре безопасности Azure.](./media/arc-security-center/remediation-trigger.png)

После применения рекомендации на сервере с поддержкой дуги Azure ресурс будет помечен как работоспособный.

  ![Снимок экрана с работоспособным сервером с поддержкой дуги Azure.](./media/arc-security-center/healthy-server.png)

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

1. Удалите виртуальные машины из каждой среды, следуя инструкциям по уничтожению, приведенным в каждом из руководств.

    - Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
    - [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
    - [Виртуальная машина](./vmware-terraform-ubuntu.md)  /  Ubuntu VMware vSphere [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
    - [Vagrant Ubuntu](./local-vagrant-ubuntu.md)  /  [Окно Vagrant Windows](./local-vagrant-windows.md)

2. Удалите рабочую область Log Analytics, выполнив следующий скрипт в Azure CLI. Укажите имя рабочей области, которое использовалось при создании рабочей области Log Analytics.

  ```console
  az monitor log-analytics workspace delete --resource-group <Name of the Azure resource group> --workspace-name <Log Analytics Workspace Name> --yes
  ```
