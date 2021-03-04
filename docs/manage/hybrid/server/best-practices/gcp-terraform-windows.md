---
title: Использование плана terraform для развертывания экземпляра Google Cloud Platform Windows и его подключения к службе "Дуга Azure"
description: Используйте план terraform, чтобы развернуть экземпляр Google Cloud Platform Windows и подключить его к службе "Дуга Azure".
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 90ffa0737316616754fd8c8df0e530ea1539371a
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102114444"
---
# <a name="use-a-terraform-plan-to-deploy-a-google-cloud-platform-windows-instance-and-connect-it-to-azure-arc"></a>Использование плана terraform для развертывания экземпляра Google Cloud Platform Windows и его подключения к службе "Дуга Azure"

В этой статье приводятся рекомендации по использованию предоставленного плана [terraform](https://www.terraform.io/) для развертывания экземпляра Windows Server обеспечить и его подключения в качестве ресурса сервера с поддержкой дуги Azure.

## <a name="prerequisites"></a>Предварительные требования

1. Клонировать репозиторий Azure ARC.

    ```console
    git clone https://github.com/microsoft/azure_arc.git
    ```

2. [Установите или обновите Azure CLI до версии 2,7 и более поздней](/cli/azure/install-azure-cli). Используйте следующую команду, чтобы проверить текущую установленную версию.

    ```console
    az --version
    ```

3. [Установка terraform >= 0,12](https://learn.hashicorp.com/tutorials/terraform/install-cli)

4. **Учетная запись Google Cloud с включенным выставлением счетов:** [Создайте бесплатную пробную учетную запись](https://cloud.google.com/free). Для создания виртуальных машин Windows Server необходимо обновить учетную запись, чтобы включить выставление счетов. В меню выберите пункт **выставление счетов** и щелкните **Обновить** в правом нижнем углу.

    ![Первое снимок экрана, показывающий, как включить выставление счетов для учетной записи обеспечить.](./media/gcp-windows/billing-1.png)

    ![Второй снимок экрана, показывающий, как включить выставление счетов для учетной записи обеспечить.](./media/gcp-windows/billing-2.png)

    ![На третьем снимке экрана показано, как включить выставление счетов для учетной записи обеспечить.](./media/gcp-windows/billing-3.png)

    **Заявление об отказе:** Чтобы избежать непредвиденных расходов, следуйте указаниям в разделе "Удаление развертывания" в конце этой статьи.

5. Создайте субъект-службу Azure.

    Чтобы подключить виртуальную машину обеспечить к службе "Дуга Azure", требуется субъект-служба Azure, назначенная с ролью участника. Чтобы создать его, войдите в учетную запись Azure и выполните следующую команду. Эту команду также можно выполнить в [Azure Cloud Shell](https://shell.azure.com/).

    ```console
    az login
    az ad sp create-for-rbac -n "<Unique SP Name>" --role contributor
    ```

    Пример:

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

## <a name="create-a-new-gcp-project"></a>Создание нового проекта обеспечить

1. Перейдите к [консоли Google API](https://console.cloud.google.com) и войдите в нее с помощью учетной записи Google. После входа [Создайте новый проект](https://cloud.google.com/resource-manager/docs/creating-managing-projects) с именем `Azure Arc demo` . После создания необходимо скопировать идентификатор проекта, так как он обычно отличается от имени проекта.

    ![Первый снимок страницы * * новый проект * * в консоли обеспечить.](./media/gcp-windows/new-project-1.png)

    ![Второй снимок страницы * * новый проект * * в консоли обеспечить.](./media/gcp-windows/new-project-2.png)

2. После создания и выбора нового проекта в раскрывающемся списке в верхней части страницы необходимо включить доступ к API ядра вычислений для проекта. Щелкните **+ включить интерфейсы API и службы** и выполните поиск *подсистемы вычислений*. Затем выберите **включить** , чтобы включить доступ через API.

    ![Первый снимок экрана: * * API ядра вычислений * * в консоли обеспечить.](./media/gcp-windows/comp-eng-api-1.png)

    ![Второй снимок экрана: * * API ядра вычислений * * в консоли обеспечить.](./media/gcp-windows/comp-eng-api-2.png)

3. Затем настройте ключ учетной записи службы, который terraform будет использовать для создания ресурсов и управления ими в проекте обеспечить. Перейдите на [страницу Создание ключа учетной записи службы](https://console.cloud.google.com/apis/credentials/serviceaccountkey). Выберите в раскрывающемся списке пункт **создать учетную запись службы** , присвойте ему имя, затем выберите проект, а затем — владелец в качестве типа ключа и щелкните **создать**. При этом загружается JSON-файл со всеми учетными данными, необходимыми для terraform управления ресурсами. Скопируйте скачанный файл JSON в `azure_arc_servers_jumpstart/gcp/windows/terraform` каталог.

    ![Снимок экрана создания учетной записи службы в консоли обеспечить.](./media/gcp-windows/svc-account.png)

## <a name="deployment"></a>Развертывание

Перед выполнением плана terraform необходимо задать и экспортировать переменные среды, которые будут использоваться планом. Эти переменные основаны на только что созданном субъекте-службе Azure, вашей подписке Azure и клиенте, а также имени проекта обеспечить.

1. Получите идентификатор подписки Azure и идентификатор клиента с помощью `az account list` команды.

2. План terraform создает ресурсы как в Microsoft Azure, так и в Google Cloud Platform. Затем он выполняет сценарий на виртуальной машине обеспечить, чтобы установить агент Arc Azure и все необходимые артефакты. Для этого скрипта требуются определенные сведения о средах обеспечить и Azure. Измените [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/windows/terraform/scripts/vars.sh) и обновите каждую из переменных с помощью соответствующих значений.

    - `TF_VAR_subscription_id` — Идентификатор подписки Azure;
    - `TF_VAR_client_id` = Идентификатор приложения субъекта-службы Azure
    - `TF_VAR_client_secret` — пароль субъекта-службы Azure.
    - `TF_VAR_tenant_id` — Идентификатор клиента Azure.
    - `TF_VAR_gcp_project_id` = ИДЕНТИФИКАТОР проекта обеспечить
    - `TF_VAR_gcp_credentials_filename` = Имя файла JSON учетных данных обеспечить

3. В интерфейсе командной строки перейдите в `azure_arc_servers_jumpstart/gcp/windows/terraform` Каталог клонированного репозитория.

4. Экспортируйте измененные переменные среды, выполнив [`scripts/vars.sh`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/windows/terraform/scripts/vars.sh) команду с исходным кодом, как показано ниже. Terraform требует, чтобы они были установлены для правильного выполнения плана.

    ```console
    source ./scripts/vars.sh
    ```

5. Выполните `terraform init` команду, которая загрузит поставщик terraform AzureRM.

    ![Снимок экрана команды "terraform init".](./media/gcp-windows/terraform-init.png)

6. Затем выполните `terraform apply --auto-approve` команду и дождитесь завершения плана. После завершения сценария terraform вы развернете виртуальную машину обеспечить Windows Server 2019 и запустили сценарий для загрузки агента Arc Azure на виртуальную машину и подключения виртуальной машины в качестве нового сервера с поддержкой дуги Azure в новой группе ресурсов Azure. Завершение подготовки агента займет несколько минут, поэтому вы получите кофе.

    ![Снимок экрана команды "terraform Apply".](./media/gcp-windows/terraform-apply.png)

7. Через несколько минут вы сможете открыть портал Azure и перейти к `arc-gcp-demo` группе ресурсов. Виртуальная машина Windows Server, созданная в обеспечить, будет отображаться как ресурс.

    ![Снимок экрана сервера с поддержкой дуги Azure в портал Azure.](./media/gcp-windows/server.png)

## <a name="semi-automated-deployment-optional"></a>Частично автоматизированное развертывание (необязательно)

План terraform автоматически устанавливает агент Arc Azure и подключает виртуальную машину к Azure в качестве управляемого ресурса, выполняя сценарий PowerShell при первой загрузке виртуальной машины.

![Снимок экрана команды "азкмажент Connect".](./media/gcp-windows/azcmagent-connect.png)

Если вы хотите получить демонстрацию и управлять фактическим процессом регистрации, выполните следующие действия.

1. Перед выполнением `terraform apply` команды откройте [`main.tf`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/gcp/windows/terraform/main.tf) и закомментируйте `windows-startup-script-ps1 = local-file.install_arc_agent-ps1.content` строку и сохраните файл.

    ![Снимок экрана с комментарием "main.tf" для отключения автоматической адаптации агента Azure ARC.](./media/gcp-windows/main-tf.png)

2. Выполните команду `terraform apply --auto-approve` , как описано выше.

3. Откройте консоль обеспечить и перейдите на страницу « [вычислительный экземпляр](https://console.cloud.google.com/compute/instances)», а затем выберите СОЗДАНную виртуальную машину.

    ![Снимок экрана сервера в консоли обеспечить.](./media/gcp-windows/gcp-server.png)

    ![Снимок экрана, показывающий, как сбросить пароль для Windows Server в консоли обеспечить.](./media/gcp-windows/reset-password.png)

4. Создайте пользователя и пароль для виртуальной машины, выбрав **задать пароль** и указав имя пользователя.

    ![Снимок экрана, показывающий, как задать имя пользователя и пароль для Windows Server в консоли обеспечить.](./media/gcp-windows/name-pword.png)

5. Подключитесь к виртуальной машине по ПРОТОКОЛу RDP, нажав кнопку RDP на странице виртуальной машины в консоли обеспечить и выполнив вход с использованием только что созданного имени пользователя и пароля.

    ![Снимок экрана, показывающий, как выполнить RDP в экземпляре обеспечить.](./media/gcp-windows/gcp-rdp.png)

6. После входа откройте интегрированную среду сценариев PowerShell **от имени администратора**. Убедитесь, что вы используете 64-разрядную версию интегрированной среды сценариев PowerShell, а не версию x86. После открытия выберите **файл > создать** , чтобы создать пустой `.ps1` файл. Затем вставьте все содержимое `./scripts/install_arc_agent.ps1` . Нажмите кнопку Воспроизведение, чтобы выполнить скрипт. По завершении вы увидите выходные данные, показывающие успешность адаптации компьютера.

    ![Снимок экрана, показывающий интегрированную среду сценариев Windows PowerShell с скриптом подключения агента Arc Azure.](./media/gcp-windows/ise-script.png)

## <a name="delete-the-deployment"></a>Удаление развертывания

Чтобы удалить все ресурсы, созданные в рамках этой демонстрации, используйте команду, `terraform destroy --auto-approve` как показано ниже.

  ![Снимок экрана команды "terraform Destroy".](./media/gcp-windows/terraform-destroy.png)

Кроме того, виртуальную машину обеспечить можно удалить непосредственно из [консоли обеспечить](https://console.cloud.google.com/compute/instances).

  ![Снимок экрана, показывающий, как удалить виртуальную машину из консоли обеспечить.](./media/gcp-windows/delete-vm.png)
