---
title: Подключение серверов с поддержкой ARC в Azure к Sentinel
description: Узнайте, как подключить серверы с поддержкой ARC в Azure к Sentinel.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 8b177db065887d3031797a26109389fd44c35f58
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799308"
---
# <a name="connect-azure-arc-enabled-servers-to-azure-sentinel"></a>Подключение серверов с поддержкой ARC в Azure к Sentinel

В этой статье содержатся рекомендации по подключению серверов с поддержкой ARC в Azure к [Sentinel](/azure/sentinel/). Это позволяет начать сбор событий, связанных с безопасностью, и начать их сопоставление с другими источниками данных.

Следующие процедуры позволят включить и настроить метку Azure для подписки Azure. Процедура включает следующие операции:

- Настройка Log Analytics рабочей области, в которой выполняется статистическая обработка журналов и событий для анализа и корреляции.
- Включение Sentinel Azure в рабочей области.
- Подключение серверов с поддержкой дуги Azure в Azure Sentinel с помощью функции управления расширениями и политики Azure.

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

1. Как уже упоминалось, это руководства начинается в том месте, где вы уже развернули и подключили виртуальные машины или серверы без операционной системы в дугу Azure. В этом сценарии используется экземпляр Google Cloud Platform (обеспечить), который уже подключен к службе "Дуга Azure" и отображается как ресурс в Azure. Как показано на следующих снимках экрана:

    ![Снимок экрана с обзором сервера с поддержкой дуги Azure в портал Azure.](./media/arc-azure-sentinel/sentinel-1.png)

    ![Снимок экрана, показывающий сведения о сервере Arc Azure в портал Azure.](./media/arc-azure-sentinel/sentinel-2.png)

1. [Установите или обновите Azure CLI](/cli/azure/install-azure-cli). Azure CLI должна работать под управлением версии 2,7 или более поздней. Используйте `az --version` для проверки текущей установленной версии.

1. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину или сервер без операционной системы к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Кроме того, это можно сделать в [Azure Cloud Shell](https://shell.azure.com/).

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

## <a name="onboard-azure-sentinel"></a>Подключение к Azure Sentinel

Sentinel Azure использует агент Log Analytics для получения файлов журналов для серверов Windows и Linux и пересылает их в Azure Sentinel. Собранные данные хранятся в Log Analytics рабочей области. Так как вы не можете использовать рабочую область по умолчанию, созданную центром безопасности Azure, требуется специальный пользователь. Вы можете иметь необработанные события и оповещения для центра безопасности Azure в той же пользовательской рабочей области, что и Sentinel Azure.

1. Создайте выделенную рабочую область Log Analytics и включите решение Sentinel для Azure в верхней части. Используйте этот [шаблон Azure Resource Manager (шаблон ARM)](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azuresentinel/arm/sentinel-template.json) для создания новой log Analytics рабочей области, определения решения Sentinel Azure и включения его для рабочей области. Чтобы автоматизировать развертывание, можно изменить [файл параметров](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/azuresentinel/arm/sentinel-template.parameters.json)шаблона ARM, указать имя и расположение рабочей области.

    ![Снимок экрана шаблона ARM.](./media/arc-azure-sentinel/sentinel-3.png)

1. Разверните шаблон Resource Manager. Перейдите в [папку развертывания](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/azuresentinel/arm) и выполните следующую команду.

  ```console
  az deployment group create --resource-group <Name of the Azure resource group> \
  --template-file <The `sentinel-template.json` template file location> \
  --parameters <The `sentinel-template.parameters.json` template file location>
  ```

Пример.

   ![Снимок экрана команды "az Deployment Group Create".](./media/arc-azure-sentinel/sentinel-4.png)

## <a name="onboard-azure-arc-enabled-vms-on-azure-sentinel"></a>Подключение виртуальных машин с поддержкой ARC в Azure на Sentinel

После развертывания метки Azure в рабочей области Log Analytics необходимо подключить к ней источники данных.

Существуют соединители для служб Майкрософт и решения сторонних производителей из экосистемы продуктов безопасности. Вы также можете использовать общий формат событий (CEF), системный журнал или REST API для подключения источников данных к Azure Sentinel.

Для серверов и виртуальных машин можно установить агент Microsoft Monitoring Agent (MMA) или агент Sentinel Azure, который собирает журналы и перенаправит их в Azure Sentinel. Вы можете развернуть агент несколькими способами с помощью дуги Azure.

- [Управление расширениями](./arc-vm-extension-mma.md). Эта функция на серверах с поддержкой Arc Azure позволяет развертывать расширения виртуальных машин агента MMA на виртуальных машинах Windows или Linux без Azure. Вы можете использовать портал Azure, Azure CLI, шаблон ARM и скрипт PowerShell для управления развертыванием расширения на серверах с поддержкой Arc Azure.

- [Политика Azure](./arc-policies-mma.md). Вы можете назначить политику для аудита, если на сервере с поддержкой Arc Azure установлен агент MMA. Если агент не установлен, можно использовать функцию расширения, чтобы автоматически развернуть ее на виртуальной машине с помощью задачи исправления — процесса регистрации, который сравнивается с виртуальными машинами Azure.

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

1. Удалите виртуальные машины из каждой среды, используя инструкции по уничтожению, приведенные в следующих руководствах.

   - Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
   - [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
   - [VMware VSPHERE виртуальной машины Ubuntu](./vmware-terraform-ubuntu.md) и [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
   - [Vagrant Ubuntu](./local-vagrant-ubuntu.md) и [Vagrant Windows Box](./local-vagrant-windows.md)

2. Удалите рабочую область Log Analytics, выполнив следующий скрипт в Azure CLI. Укажите имя рабочей области, которое использовалось при создании рабочей области Log Analytics.

  ```console
  az monitor log-analytics workspace delete --resource-group <Name of the Azure resource group> --workspace-name <Log Analytics Workspace Name> --yes
  ```
