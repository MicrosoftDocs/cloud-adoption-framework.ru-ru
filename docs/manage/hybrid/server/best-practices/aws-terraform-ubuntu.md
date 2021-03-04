---
title: Использование плана terraform для развертывания экземпляра Amazon Web Services Amazon эластичного облака и подключения его к службе "Дуга Azure"
description: Используйте план terraform для развертывания экземпляра Amazon Web Services Amazon эластичного облака и подключения его к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 030c506e5a8485379116950e58e66ed386f5cab5
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102114580"
---
# <a name="use-a-terraform-plan-to-deploy-an-amazon-web-services-amazon-elastic-compute-cloud-instance-and-connect-it-to-azure-arc"></a>Использование плана terraform для развертывания экземпляра Amazon Web Services Amazon эластичного облака и подключения его к службе "Дуга Azure"

В этой статье приводятся рекомендации по использованию предоставленного плана [terraform](https://www.terraform.io/) для развертывания экземпляра Amazon Web Services (AWS) Amazon эластичного облака (EC2) и подключения его в качестве ресурса сервера с поддержкой ARC в Azure.

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

4. [Создание бесплатной учетной записи AWS](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

5. [Установка terraform >= 0,12](https://learn.hashicorp.com/tutorials/terraform/install-cli)

6. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину AWS к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

    ```console
    az login
    az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
    ```

    Пример:

    ```console
    az ad sp create-for-rbac -n "http://AzureArcAWS" --role contributor
    ```

    Выходные данные должны выглядеть следующим образом:

    ```json
    {
      "appId": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
      "displayName": "AzureArcAWS",
      "name": "http://AzureArcAWS",
      "password": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
      "tenant": "XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    }
    ```

    > [!NOTE]
    > Мы настоятельно рекомендуем ограничить субъект-службу определенной [подпиской Azure и группой ресурсов](/cli/azure/ad/sp).

## <a name="create-an-aws-identity"></a>Создание удостоверения AWS

Чтобы terraform мог создавать ресурсы в AWS, необходимо создать новую AWS роль IAM с соответствующими разрешениями и настроить terraform для ее использования.

1. Вход в [консоль управления AWS](https://console.aws.amazon.com/console/home)

2. После входа выберите раскрывающийся список **службы** в верхнем левом углу. В разделе **безопасность, идентификация и соответствие** выберите **IAM** для доступа к [странице Управление удостоверениями и доступом](https://console.aws.amazon.com/iam/home) .

    ![Снимок экрана облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-console.png)

    ![Снимок экрана управления удостоверениями и доступом в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-iam.png)

3. Щелкните **Пользователи** в меню слева и выберите **Добавить пользователя** , чтобы создать нового пользователя IAM.

    ![Снимок экрана создания нового пользователя в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-new-user-1.png)

4. На странице **Добавление пользователя** укажите имя пользователя `Terraform` и установите флажок **программный доступ** , а затем нажмите кнопку **Далее**.

    ![Второй снимок экрана создания пользователя в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-new-user-2.png)

5. На странице **Задание разрешений** установите флажок **присоединить существующие политики напрямую** , а затем установите флажок рядом с **AmazonEC2FullAccess** , как показано на снимке экрана, а затем нажмите кнопку **Далее**.

    ![Третий снимок экрана создания пользователя в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-new-user-3.png)

6. На странице **теги** назначьте тег с ключом `azure-arc-demo` и нажмите кнопку **Далее** , чтобы перейти на страницу **Проверка** .

    ![Снимок экрана тегов в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-tags.png)

7. Убедитесь, что все правильно, и выберите **создать пользователя** при готовности.

    ![Четвертый снимок экрана создания пользователя в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-new-user-4.png)

8. После создания пользователя вы увидите идентификатор ключа доступа пользователя и секретный ключ доступа. Скопируйте эти значения перед нажатием кнопки **Закрыть**. На следующей странице можно увидеть пример того, как он должен выглядеть. После получения этих ключей вы сможете использовать их с terraform для создания ресурсов AWS.

    ![Снимок экрана: успешное создание пользователя в облачной консоли AWS.](./media/aws-ubuntu/aws-ubuntu-new-user-5.png)

## <a name="configure-terraform"></a>Настройка Terraform

Перед выполнением плана terraform необходимо экспортировать переменные среды, которые будут использоваться планом. Эти переменные основаны на подписке и клиенте Azure, субъекте-службе Azure и пользователе и ключах AWS IAM, которые вы только что создали.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. План terraform создает ресурсы как в Microsoft Azure, так и в AWS. Затем он выполняет сценарий на виртуальной машине AWS EC2, чтобы установить агент ARC для Azure и все необходимые артефакты. Для этого скрипта требуются определенные сведения о средах AWS и Azure. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/ubuntu/terraform/scripts/vars.sh) и обновите каждую из переменных с помощью соответствующих значений.

    - `TF_VAR_subscription_id` — Идентификатор подписки Azure;
    - `TF_VAR_client_id` = Идентификатор приложения субъекта-службы Azure
    - `TF_VAR_client_secret` — Пароль субъекта-службы Azure.
    - `TF_VAR_tenant_id` — Идентификатор клиента Azure.
    - `AWS_ACCESS_KEY_ID` = AWS ключ доступа
    - `AWS_SECRET_ACCESS_KEY` = AWS секретный ключ

3. В Azure CLI перейдите в `azure_arc_servers_jumpstart/aws/ubuntu/terraform` Каталог клонированного репозитория.

4. Экспортируйте измененные переменные среды, выполнив [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/ubuntu/terraform/scripts/vars.sh) команду с исходным кодом, как показано ниже. Terraform требует, чтобы они были установлены для правильного выполнения плана. Обратите внимание, что этот скрипт также будет автоматически удален на виртуальной машине AWS в рамках развертывания terraform.

    ```console
    source ./scripts/vars.sh
    ```

5. Убедитесь, что ключи SSH доступны в *~/.SSH.* и имеют имена `id_rsa.pub` и `id_rsa` . Если вы прийдете к руководству по SSH-Keygen выше, чтобы создать ключ, это уже должно быть правильно настроено. В противном случае может потребоваться изменить, [`main.tf`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/ubuntu/terraform/main.tf) чтобы использовать ключ с другим путем.

6. Выполните `terraform init` команду, которая загрузит поставщик terraform AzureRM.

    ![Снимок экрана команды "terraform init".](./media/aws-ubuntu/aws-ubuntu-terraform-init.png)

## <a name="deployment"></a>Развертывание

1. Выполните `terraform apply --auto-approve` команду и дождитесь завершения плана. После завершения вы получите экземпляр AWS Amazon Linux 2 EC2, развернутый и подключенный как новый сервер с поддержкой ARC в Azure в новой группе ресурсов.

2. Откройте портал Azure и перейдите к `arc-aws-demo` группе ресурсов. Виртуальная машина, созданная в AWS, будет отображаться как ресурс.

    ![Снимок экрана, показывающий сервер с поддержкой дуги Azure в портал Azure.](./media/aws-ubuntu/aws-ubuntu-server.png)

    ![Снимок экрана консоли AWS, отображающей экземпляры EC2.](./media/aws-ubuntu/aws-ubuntu-ec2-instances.png)

## <a name="semi-automated-deployment-optional"></a>Частично автоматизированное развертывание (необязательно)

Как вы могли заметить, последний этап выполнения — зарегистрировать виртуальную машину в качестве нового ресурса сервера с поддержкой Arc Azure.

  ![Снимок экрана команды "азкмажент Connect".](./media/aws-ubuntu/aws-ubuntu-azcmagent-1.png)

Если вы хотите получить демонстрацию и управлять фактическим процессом регистрации, выполните следующие действия.

1. В [`install_arc_agent.sh.tmpl`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/ubuntu/terraform/scripts/install_arc_agent.sh.tmpl) шаблоне скрипта закомментируйте `run connect command` раздел и сохраните файл.

    ![Снимок экрана с комментарием "main.tf" для отключения автоматической адаптации агента Azure ARC.](./media/aws-ubuntu/aws-ubuntu-main-tf.png)

2. Получите общедоступный IP-адрес виртуальной машины AWS, выполнив `terraform output` .

    ![Снимок экрана terraform выходных данных.](./media/aws-ubuntu/aws-ubuntu-terraform.png)

3. Подключитесь к виртуальной машине по протоколу SSH, используя, `ssh ubuntu@xx.xx.xx.xx` где `xx.xx.xx.xx` — это IP-адрес узла.

    ![Снимок экрана ключа SSH, подключающегося к серверу EC2.](./media/aws-ubuntu/aws-ubuntu-ssh.png)

4. Экспортируйте все переменные среды в [`vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/ubuntu/terraform/scripts/vars.sh) .

    ![Снимок экрана экспортированных переменных среды в "vars.sh".](./media/aws-ubuntu/aws-ubuntu-export-variables.png)

5. Выполните следующую команду:

    ```console
    azcmagent connect --service-principal-id $TF_VAR_client_id --service-principal-secret $TF_VAR_client_secret --resource-group "arc-aws-demo" --tenant-id $TF_VAR_tenant_id --location "westus2" --subscription-id $TF_VAR_subscription_id
    ```

    ![Еще один снимок экрана команды "азкмажент Connect".](./media/aws-ubuntu/aws-ubuntu-azcmagent-2.png)

6. По завершении ваша виртуальная машина будет зарегистрирована в службе "Дуга Azure" и отобразится в группе ресурсов с помощью портал Azure.

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить все ресурсы, созданные в рамках этой демонстрации, используйте команду, `terraform destroy --auto-approve` как показано ниже.

  ![Снимок экрана команды "terraform Destroy".](./media/aws-ubuntu/aws-ubuntu-terraform-destroy.png)

Кроме того, экземпляр AWS EC2 можно удалить напрямую, заменив его на [консоли AWS](https://console.aws.amazon.com/ec2/v2/home). Обратите внимание, что для фактического удаления экземпляра может потребоваться несколько минут.

  ![Снимок экрана: завершение экземпляра в консоли AWS.](./media/aws-ubuntu/aws-ubuntu-terminate.png)

При удалении экземпляра вручную необходимо также удалить `*./scripts/install_arc_agent.sh` , который создается с помощью плана terraform.
