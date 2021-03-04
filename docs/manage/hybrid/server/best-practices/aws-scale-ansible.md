---
title: Использование Ansible для масштабирования Amazon Web Services Amazon эластичное вычисление облачных экземпляров в Azure Arc
description: Использование Ansible для масштабирования Amazon Web Services Amazon эластичное вычисление облачных экземпляров в Azure Arc
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 58b8355659779ef4258dd9d2935e8b09d3d9559b
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101797670"
---
# <a name="use-ansible-to-scale-onboarding-amazon-web-services-amazon-elastic-compute-cloud-instances-to-azure-arc"></a>Использование Ansible для масштабирования Amazon Web Services Amazon эластичное вычисление облачных экземпляров в Azure Arc

В этой статье приводятся рекомендации по использованию [Ansible](https://www.ansible.com/) для масштабирования экземпляров Amazon Web Services (AWS) Amazon эластичного облака (Amazon EC2) в дугу Azure.

В этом учебнике предполагается, что у вас есть базовое понимание Ansible. Предоставляется базовый Ansible сборник тренировочных заданий и конфигурация, которая использует [`amazon.aws.aws-ec2`](https://docs.ansible.com/ansible/latest/collections/amazon/aws/aws_ec2_inventory.html) подключаемый модуль для динамической загрузки данных инвентаризации EC2 Server.

Это руководством можно использовать, даже если у вас еще нет тестовой среды Ansible и он содержит план terraform, который создаст пример AWS EC2 Server Inventory, состоящий из четырех серверов Windows Server 2019 и четырех серверов Ubuntu с простой конфигурацией CentOS 7 Ansible Control Server.

> [!WARNING]
> В указанной образце книги Ansible для настройки серверов под управлением Windows используется WinRM с проверкой подлинности с помощью пароля и HTTP. Это не рекомендуется для рабочих сред. Если вы планируете использовать Ansible с узлами Windows в рабочей среде, следует использовать [WinRM по протоколу HTTPS](/troubleshoot/windows-client/system-management-components/configure-winrm-for-https) с сертификатом.

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

5. [Установка terraform >= V 0,13](https://learn.hashicorp.com/tutorials/terraform/install-cli)

   - Создайте субъект-службу Azure.

      Чтобы подключить виртуальную машину AWS к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

      ```console
      az login
      az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
      ```
  
      Пример.
  
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

    ![Снимок экрана облачной консоли AWS.](./media/aws-scale-ansible/ansible-aws-console.png)

    ![Снимок экрана управления удостоверениями и доступом в облачной консоли AWS.](./media/aws-scale-ansible/ansible-iam.png)

3. В меню слева выберите **Пользователи** , а затем щелкните **Добавить пользователя** , чтобы создать нового пользователя IAM.

    ![Снимок экрана нового пользователя в облачной консоли AWS.](./media/aws-scale-ansible/ansible-new-user-1.png)

4. На странице **Добавление пользователя** назовите пользователя **terraform** и установите флажок **программный доступ** , а затем нажмите кнопку **Далее** .

    ![Второй снимок экрана нового пользователя, создаваемого в консоли AWS Cloud.](./media/aws-scale-ansible/ansible-new-user-2.png)

5. На следующей странице **Задайте разрешения**, установите флажок **присоединить существующие политики напрямую** , установите флажок рядом с **AmazonEC2FullAccess** , как показано на снимке экрана, а затем нажмите кнопку **Далее**.

    ![Третий снимок экрана нового пользователя, создаваемого в консоли AWS Cloud.](./media/aws-scale-ansible/ansible-new-user-3.png)

6. На странице **теги** назначьте тег с ключом `azure-arc-demo` и нажмите кнопку **Далее** , чтобы перейти на страницу **Проверка** .

    ![Снимок экрана тегов в облачной консоли AWS.](./media/aws-scale-ansible/ansible-tags.png)

7. Убедитесь, что все правильно, и нажмите кнопку **создать пользователя**.

    ![Четвертый снимок экрана нового пользователя в облачной консоли AWS.](./media/aws-scale-ansible/ansible-new-user-4.png)

8. После создания пользователя вы увидите идентификатор ключа доступа пользователя и секретный ключ доступа. Перед выбором кнопки " **Закрыть**" скопируйте эти значения. На следующей странице можно увидеть пример того, как он должен выглядеть. После получения этих ключей вы сможете использовать их с terraform для создания ресурсов AWS.

    ![Снимок экрана: успешное создание пользователя в облачной консоли AWS.](./media/aws-scale-ansible/ansible-new-user-5.png)

## <a name="option-1-create-a-sample-aws-server-inventory-and-ansible-control-server-using-terraform-and-onboard-the-servers-to-azure-arc"></a>Вариант 1. Создание примера AWS Server Inventory и Ansible Control Server с помощью terraform и подключение серверов к службе "Дуга Azure"

> [!NOTE]
> Если у вас уже есть существующий сервер AWS Server Inventory и Ansible, перейдите к варианту 2.

### <a name="configure-terraform"></a>Настройка Terraform

Перед выполнением плана terraform необходимо экспортировать переменные среды, которые будут использоваться планом. Эти переменные основаны на подписке и клиенте Azure, субъекте-службе Azure и пользователе и ключах AWS IAM, которые вы только что создали.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. План terraform создает ресурсы как в Microsoft Azure, так и в AWS. Затем он выполняет сценарий на виртуальной машине AWS EC2 для установки Ansible и всех необходимых артефактов. Для этого плана terraform требуются определенные сведения о средах AWS и Azure, к которым он обращается с использованием переменных среды. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform/scripts/vars.sh) и обновите каждую из переменных с помощью соответствующих значений.

   - `TF-VAR-subscription-id` — Идентификатор подписки Azure;
   - `TF-VAR-client-id` = Идентификатор приложения субъекта-службы Azure
   - `TF-VAR-client-secret` — пароль субъекта-службы Azure.
   - `TF-VAR-tenant-id` — Идентификатор клиента Azure.
   - `AWS-ACCESS-KEY-ID` = AWS ключ доступа
   - `AWS-SECRET-ACCESS-KEY` = AWS секретный ключ

3. В оболочке перейдите в `azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform` Каталог клонированного репозитория.

4. Экспортируйте измененные переменные среды, выполнив [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform/scripts/vars.sh) команду с исходным кодом, как показано ниже. Terraform требует, чтобы они были установлены для правильного выполнения плана.

    ```console
    source ./scripts/vars.sh
    ```

5. Убедитесь, что ключи SSH доступны в `~/.ssh` и с именами `id-rsa.pub` и `id-rsa` . Если вы вошли в руководством по SSH Keygen выше, чтобы создать ключ, он уже должен быть правильно настроен. В противном случае может потребоваться изменить, [`aws-infrastructure.tf`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform/aws_infra.tf) чтобы использовать ключ с другим путем.

6. Выполните `terraform init` команду, которая будет скачивать необходимые поставщики terraform.

    ![Снимок экрана команды "terraform init".](./media/aws-scale-ansible/terraform-init.png)

### <a name="deploy-server-infrastructure"></a>Развертывание инфраструктуры сервера

1. В `azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform` каталоге запустите `terraform apply --auto-approve` и дождитесь завершения плана. После успешного завершения вы получите четыре сервера Windows Server 2019, четыре сервера Ubuntu и один сервер управления CentOS 7 Ansible.

2. Откройте консоль AWS и убедитесь, что созданные серверы доступны.

    ![Снимок экрана консоли AWS, отображающей экземпляры EC2.](./media/aws-scale-ansible/ec2-instances.png)

### <a name="run-the-ansible-playbook-to-onboard-the-aws-ec2-instances-as-azure-arc-enabled-servers"></a>Запустите Ansible сборник тренировочных заданий, чтобы подключить экземпляры AWS EC2 в качестве серверов с поддержкой ARC в Azure.

1. После завершения плана terraform отображает общедоступный IP-адрес сервера управления Ansible в выходной переменной с именем `ansible-ip` . Подключитесь к серверу Ansible по протоколу SSH, выполнив `ssh centos@xx.xx.xx.xx` , где `xx.xx.xx.xx` заменяется на IP-адрес сервера Ansible.

    ![Снимок экрана ключа SSH, подключающегося к удаленному серверу с помощью Ansible.](./media/aws-scale-ansible/ansible-ssh.png)

2. Перейдите в каталог `ansible` , выполнив `cd ansible` . Эта папка содержит пример конфигурации Ansible и сборник тренировочных заданий, которые будут использоваться для подключения серверов к службе "Дуга Azure".

    ![Снимок экрана сценария оболочки со списком файла "".](./media/aws-scale-ansible/ansible-cfg.png)

3. `aw-ec2`Подключаемому модулю Ansible требуются учетные данные AWS для динамического чтения данных инвентаризации сервера AWS. Мы будем экспортировать их как переменные среды. Выполните следующие команды, заменив значения для `AWS-ACCESS-KEY-ID` и на `AWS-SECRET-ACCESS-KEY` учетные данные AWS, которые были созданы ранее.

    ```console
    export AWS-ACCESS-KEY-ID="XXXXXXXXXXXXXXXXX"
    export AWS-SECRET-ACCESS-KEY="XXXXXXXXXXXXXXX"
    ```

4. Замените значения заполнителей для идентификатора клиента Azure и идентификатора подписки в [`group-vars/all.yml`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform/ansible_config/group_vars/all.yml) файле соответствующими значениями для вашей среды.

    ![Снимок экрана переменных в файле YAML.](./media/aws-scale-ansible/yml-variables.png)

5. Запустите Ansible сборник тренировочных заданий, выполнив следующую команду, заменив идентификатор субъекта-службы Azure и секрет субъекта-службы.

    ```console
    ansible-playbook arc-agent.yml -i ansible-plugins/inventory-uswest2-aws-ec2.yml --extra-vars '{"service-principal-id": "XXXXXXX-XXXXX-XXXXXXX", "service-principal-secret": "XXXXXXXXXXXXXXXXXXXXXXXX"}'
    ```

    Если выполнение сборник тренировочных заданий успешно, вы увидите результат, аналогичный приведенному ниже снимку экрана.

    ![Снимок экрана с Ansible сборник тренировочных заданий.](./media/aws-scale-ansible/ansible-playbook.png)

6. Откройте портал Azure и перейдите к группе ресурсов Arc-AWS-Demo. Вы должны увидеть список серверов с поддержкой дуги Azure.

    ![Снимок экрана портал Azure адаптации серверов с поддержкой дуги Azure.](./media/aws-scale-ansible/onboarding-servers.png)

### <a name="clean-up-environment-by-deleting-resources"></a>Очистка окружения путем удаления ресурсов

Чтобы удалить все ресурсы, созданные в рамках этой демонстрации, используйте `terraform destroy --auto-approve` команду, как показано ниже.

![Снимок экрана команды "terraform Destroy".](./media/aws-scale-ansible/terraform-destroy.png)

## <a name="option-2-onboarding-an-existing-aws-server-inventory-to-azure-arc-using-your-own-ansible-control-server"></a>Вариант 2. Подключение существующего каталога AWS Server к службе "Дуга Azure" с помощью собственного сервера управления Ansible

> [!NOTE]
> Если у вас нет существующего сервера AWS Server Inventory и Ansible, вернитесь к варианту 1.

### <a name="review-provided-ansible-configuration-and-playbook"></a>Ознакомьтесь с предоставленной конфигурацией Ansible и сборник тренировочных заданий

1. Перейдите в `ansible-config` каталог и просмотрите указанную конфигурацию. Указанная конфигурация содержит базовый `ansible.cfg` файл. Этот файл включает [`amazon.aws.aws-ec2`](https://docs.ansible.com/ansible/latest/collections/amazon/aws/aws-ec2-inventory.html) подключаемый модуль Ansible, который динамически загружает инвентаризацию сервера с помощью роли AWS IAM. Убедитесь, что используемая роль IAM имеет достаточные привилегии для доступа к инвентаризации, которую вы хотите подключить.

    ![Снимок экрана, показывающий сведения о файле "ansible. cfg".](./media/aws-scale-ansible/ansible-cfg-details.png)

2. Этот файл [`inventory-uswest2-aws-ec2.yml`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/aws/scaled_deployment/ansible/terraform/ansible_config/ansible_plugins/inventory_uswest2_aws_ec2.yml) настраивает `aws-ec2` подключаемый модуль для извлечения запасов из `uswest2` региона и ресурсов группы по примененным тегам. При необходимости настройте этот файл для поддержки адаптации инвентаризации сервера, например для изменения региона или настройки групп или фильтров.

   Файлы в `./ansible-config/group-vars` должны быть изменены для предоставления учетных данных, которые будут использоваться для подключения различных групп узлов Ansible.

3. После корректировки указанной конфигурации для поддержки среды запустите Ansible сборник тренировочных заданий, выполнив следующую команду, заменив идентификатор субъекта-службы Azure и секрет субъекта-службы.

    ```console
    ansible-playbook arc-agent.yml -i ansible-plugins/inventory-uswest2-aws-ec2.yml --extra-vars '{"service-principal-id": "XXXXXXX-XXXXX-XXXXXXX", "service-principal-secret": "XXXXXXXXXXXXXXXXXXXXXXXX"}'
    ```

    Как и раньше, при успешном выполнении сборник тренировочных заданий вы увидите выходные данные, аналогичные следующему снимку экрана:

      ![Снимок экрана с Ansible сборник тренировочных заданий.](./media/aws-scale-ansible/ansible-playbook.png)

    Как и ранее, откройте портал Azure и перейдите к группе ресурсов Arc-AWS-Demo. Вы должны увидеть список серверов с поддержкой дуги Azure.

    ![Снимок экрана портал Azure, показывающей серверы с поддержкой дуги Azure.](./media/aws-scale-ansible/onboarding-servers.png)
