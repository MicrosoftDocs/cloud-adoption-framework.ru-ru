---
title: Использование плана terraform для развертывания экземпляра Google Cloud Platform Ubuntu и его подключения к службе "Дуга Azure"
description: Используйте план terraform, чтобы развернуть экземпляр Google Cloud Platform Ubuntu и подключить его к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: ba39a2e2b8bd9e226c8d81599de1920b9878b9e0
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101799183"
---
# <a name="use-a-terraform-plan-to-deploy-a-google-cloud-platform-ubuntu-instance-and-connect-it-to-azure-arc"></a>Использование плана terraform для развертывания экземпляра Google Cloud Platform Ubuntu и его подключения к службе "Дуга Azure"

В этой статье приводятся рекомендации по использованию предоставленного плана [terraform](https://www.terraform.io/) для развертывания экземпляра Google Cloud Platform (обеспечить) и его подключения в качестве ресурса сервера с поддержкой дуги Azure.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. [Создание ключа SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (или использование существующего ключа SSH)

4. [Создать учетную запись бесплатной Google Cloud Platform](https://cloud.google.com/free)

5. [Установка terraform >= 0,12](https://learn.hashicorp.com/tutorials/terraform/install-cli)

6. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину обеспечить к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

    ```console
    az login
    az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
    ```

    Пример.

    ```console
    az ad sp create-for-rbac -n "http://AzureArcGCP" --role contributor
    ```

    Выходные данные должны выглядеть следующим образом:

    ```json
    {
      "appId": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
      "displayName": "AzureArcGCP",
      "name": "http://AzureArcGCP",
      "password": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
      "tenant": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    }
    ```

    > [!NOTE]
    > Мы настоятельно рекомендуем ограничить субъект-службу определенной [подпиской Azure и группой ресурсов](/cli/azure/ad/sp).

<!-- docutune:casing "Compute Engine API" -->

## <a name="create-a-new-gcp-project"></a>Создание нового проекта обеспечить

1. Перейдите к [консоли Google API](https://console.developers.google.com) и войдите в нее с помощью учетной записи Google. После входа [Создайте новый проект](https://cloud.google.com/resource-manager/docs/creating-managing-projects) с именем `Azure Arc demo` . После его создания обязательно скопируйте идентификатор проекта, так как он обычно отличается от имени проекта.

    ![Первый снимок страницы * * новый проект * * в консоли обеспечить.](./media/gcp-ubuntu/ubuntu-new-project-1.png)

    ![Второй снимок страницы * * новый проект * * в консоли обеспечить.](./media/gcp-ubuntu/ubuntu-new-project-2.png)

2. После создания и выбора нового проекта в раскрывающемся списке в верхней части страницы необходимо включить доступ к API ядра вычислений для проекта. Щелкните **+ включить интерфейсы API и службы** и выполните поиск *подсистемы вычислений*. Затем выберите **включить** , чтобы включить доступ через API.

    ![Первый снимок экрана: * * API ядра вычислений * * в консоли обеспечить.](./media/gcp-ubuntu/ubuntu-comp-eng-api-1.png)

    ![Второй снимок экрана: * * API ядра вычислений * * в консоли обеспечить.](./media/gcp-ubuntu/ubuntu-comp-eng-api-2.png)

3. Затем настройте ключ учетной записи службы, который terraform будет использовать для создания ресурсов и управления ими в проекте обеспечить. Перейдите на [страницу Создание ключа учетной записи службы](https://console.cloud.google.com/apis/credentials/serviceaccountkey). Выберите в раскрывающемся списке пункт **создать учетную запись службы** , присвойте ему имя, затем выберите проект, а затем — владелец в качестве типа ключа и щелкните **создать**. При этом будет скачан JSON-файл со всеми учетными данными, необходимыми для terraform управления ресурсами. Скопируйте скачанный файл JSON в `azure_arc_servers_jumpstart/gcp/ubuntu/terraform` каталог.

    ![Снимок экрана создания учетной записи службы в консоли обеспечить.](./media/gcp-ubuntu/ubuntu-svc-account.png)

4. Наконец, убедитесь, что ключи SSH доступны в `~/.ssh` и с именами `id-rsa.pub` и `id-rsa` . Если вы прийдете к руководству по SSH-Keygen выше, чтобы создать ключ, это уже должно быть правильно настроено. В противном случае может потребоваться изменить, [`main.tf`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/ubuntu/terraform/main.tf) чтобы использовать ключ с другим путем.

## <a name="deployment"></a>Развертывание

Перед выполнением плана terraform необходимо экспортировать переменные среды, которые будут использоваться планом. Эти переменные основаны на только что созданном субъекте-службе Azure, вашей подписке Azure и клиенте, а также имени проекта обеспечить.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. План terraform создает ресурсы как в Microsoft Azure, так и в Google Cloud Platform. Затем он выполняет сценарий на виртуальной машине обеспечить, чтобы установить агент Arc Azure и все необходимые артефакты. Для этого скрипта требуются определенные сведения о средах обеспечить и Azure. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/ubuntu/terraform/scripts/vars.sh) и обновите каждую из переменных с помощью соответствующих значений.

    - `TF-VAR-subscription-id`— Идентификатор подписки Azure;
    - `TF-VAR-client-id` = Идентификатор приложения субъекта-службы Azure
    - `TF-VAR-client-secret` — пароль субъекта-службы Azure.
    - `TF-VAR-tenant-id` — Идентификатор клиента Azure.
    - `TF-VAR-gcp-project-id` = ИДЕНТИФИКАТОР проекта обеспечить
    - `TF-VAR-gcp-credentials-filename` = Имя файла JSON учетных данных обеспечить

3. В интерфейсе командной строки перейдите в `azure_arc_servers_jumpstart/gcp/ubuntu/terraform` Каталог клонированного репозитория.

4. Экспортируйте измененные переменные среды, выполнив [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/ubuntu/terraform/scripts/vars.sh) команду с исходным кодом, как показано ниже. Terraform требует, чтобы они были установлены для правильного выполнения плана. Обратите внимание, что этот скрипт также будет автоматически удален на виртуальной машине обеспечить в рамках развертывания terraform.

    ```console
    source ./scripts/vars.sh
    ```

5. Выполните `terraform init` команду, которая загрузит поставщик terraform AzureRM.

    ![Снимок экрана команды "terraform init".](./media/gcp-ubuntu/ubuntu-terraform-init.png)

6. Затем выполните `terraform apply --auto-approve` команду и дождитесь завершения плана. После завершения вы получите виртуальную машину обеспечить Ubuntu, развернутую и подключенную как новый сервер с поддержкой ARC в Azure в новой группе ресурсов.

7. Откройте портал Azure и перейдите к `arc-gcp-demo` группе ресурсов. Виртуальная машина, созданная в обеспечить, будет отображаться как ресурс.

    ![Снимок экрана сервера с поддержкой дуги Azure в портал Azure.](./media/gcp-ubuntu/ubuntu-server.png)

## <a name="semi-automated-deployment-optional"></a>Частично автоматизированное развертывание (необязательно)

Как вы могли заметить, последний этап выполнения — зарегистрировать виртуальную машину в качестве нового ресурса сервера с поддержкой Arc Azure.

![Снимок экрана: запуск команды "азкмажент Connect".](./media/gcp-ubuntu/ubuntu-azcmagent-connect.png)

Если вы хотите получить демонстрацию и управлять фактическим процессом регистрации, выполните следующие действия.

1. В [`install_arc_agent.sh.tmpl`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/ubuntu/terraform/scripts/install_arc_agent.sh.tmpl) шаблоне скрипта закомментируйте `run connect command` раздел и сохраните файл.

    ![Снимок экрана с комментарием "main.tf" для отключения автоматической адаптации агента Azure ARC.](./media/gcp-ubuntu/ubuntu-main-tf.png)

2. Получите общедоступный IP-адрес виртуальной машины обеспечить, выполнив `terraform output` .

    ![Снимок экрана terraform выходных данных.](./media/gcp-ubuntu/ubuntu-terraform.png)

3. Подключитесь к виртуальной машине по протоколу SSH, используя, `ssh arcadmin@xx.xx.xx.xx` где `xx.xx.xx.xx` — это IP-адрес узла.

    ![Снимок экрана ключа SSH, подключающегося к серверу обеспечить.](./media/gcp-ubuntu/ubuntu-ssh.png)

4. Экспортируйте все переменные среды в [`vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/ubuntu/terraform/scripts/vars.sh)

    ![Снимок экрана переменных среды, экспортирующих с помощью "vars.sh".](./media/gcp-ubuntu/ubuntu-export-variables.png)

5. Выполните следующую команду:

    ```console azcmagent connect --service-principal-ID $tf-VAR-client-ID --service-principal-secret $tf-VAR-client-secret --resource-group "Azure Arc gcp-demo" --tenant-ID $tf-VAR-tenant-ID --location "westus2" --subscription-ID $tf-VAR-subscription-ID
    ```

    ![Снимок экрана команды "азкмажент Connect" успешно завершен.](./media/gcp-ubuntu/ubuntu-azcmagent.png)

6. По завершении ваша виртуальная машина будет зарегистрирована в службе "Дуга Azure" и отобразится в группе ресурсов с помощью портал Azure.

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить все ресурсы, созданные в рамках этой демонстрации, используйте команду, `terraform destroy --auto-approve` как показано ниже.

![Снимок экрана команды "terraform Destroy".](./media/gcp-ubuntu/ubuntu-terraform-destroy.png)

Кроме того, виртуальную машину обеспечить можно удалить непосредственно из [консоли обеспечить](https://console.cloud.google.com/compute/instances).

![Снимок экрана, показывающий, как удалить виртуальную машину из консоли обеспечить.](./media/gcp-ubuntu/ubuntu-delete-vm.png)
