---
title: Использование Управление обновлениями в службе автоматизации Azure для управления обновлениями операционной системы для серверов с поддержкой ARC в Azure
description: Узнайте, как подключить серверы с поддержкой ARC в Azure для Управление обновлениями в службе автоматизации Azure.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: ca1ae4422dbfc245fe85befa8fd66762808b5565
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102112251"
---
# <a name="use-update-management-in-azure-automation-to-manage-operating-system-updates-for-azure-arc-enabled-servers"></a>Использование Управление обновлениями в службе автоматизации Azure для управления обновлениями операционной системы для серверов с поддержкой ARC в Azure

В этой статье приводятся рекомендации по подключению серверов с поддержкой ARC в Azure к [Управление обновлениями в службе автоматизации Azure](/azure/automation/update-management/overview), чтобы можно было управлять обновлениями операционной системы для серверов с поддержкой дуги Azure под управлением Windows или Linux.

В следующих процедурах вы создадите и настроите учетную запись службы автоматизации Azure и Log Analytics рабочую область для поддержки Управление обновлениями для серверов с поддержкой ARC в Azure, выполнив следующие действия.

- Настройка новой рабочей области Log Analytics и учетной записи службы автоматизации Azure.
- Включение Управление обновлениями на серверах с поддержкой дуги Azure.

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

2. Как уже упоминалось, это руководства начинается в том месте, где вы уже развернули и подключили виртуальные машины или серверы без операционной системы в дугу Azure. В этом сценарии мы используем экземпляр EC2 Amazon Web Services (AWS), который уже подключен к службе "Дуга Azure" и отображается как ресурс в Azure.

    ![Снимок экрана EC2 в облачной консоли Amazon Web Services.](./media/arc-update-management/aws-ec2-instance.png)

    ![Снимок экрана сервера с поддержкой дуги Azure в портал Azure.](./media/arc-update-management/arc-enabled-server.png)

3. [Установите или обновите Azure CLI](/cli/azure/install-azure-cli). Azure CLI должна работать под управлением версии 2,14 или более поздней. Используйте `az --version` для проверки текущей установленной версии.

## <a name="configure-update-management"></a>Настройка Управление обновлениями

Управление обновлениями использует агент Log Analytics для сбора файлов журналов Windows и Linux Server, а собираемые данные хранятся в Log Analytics рабочей области.

1. Создайте Log Analytics рабочую область с помощью этого [шаблона Azure Resource Manager (шаблон ARM)](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/updateManagement/law-template.json). При этом создается новая Рабочая область Log Analytics, определяется Управление обновлениями решение и включается для рабочей области.

2. Создайте новую группу ресурсов для рабочей области Log Analytics, выполнив следующую команду, заменив значения в квадратных скобках собственными.

    ```console
    az group create --name <Name for your resource group> \
    --location <Location for your resources> \
    --tags "Project=jumpstart_azure_arc_servers"
    ```

    ![Снимок экрана команды "az Group Create".](./media/arc-update-management/az-group-create.png)

3. Измените [файл параметров](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/updateManagement/law-template.parameters.json)шаблона ARM, указав имя рабочей области log Analytics, расположение и имя учетной записи службы автоматизации Azure. Также необходимо указать имя сервера с поддержкой дуги Azure и имя группы ресурсов, содержащей сервер с поддержкой дуги Azure, как показано в следующем примере:

    ![Снимок экрана шаблона ARM.](./media/arc-update-management/arm-template.png)

4. Разверните шаблон Resource Manager. Перейдите в [папку развертывания](https://github.com/microsoft/azure_arc/tree/main/azure_arc_servers_jumpstart/updateManagement) и выполните следующую команду:

    ```console
    az deployment group create --resource-group <Name of the Azure resource group you created> \
        --template-file law-template.json \
        --parameters law-template.parameters.json
    ```

   ![Снимок экрана команды "az Deployment Group".](./media/arc-update-management/az-deployment-group.png)

5. После завершения развертывания вы увидите группу ресурсов с Log Analytics рабочей областью, учетной записью службы автоматизации и Управление обновлениями решением из портал Azure. При переходе на вкладку **решения** log Analytics рабочей области вы увидите **Управление обновлениями** решение.

    ![Снимок экрана Log Analytics рабочей области в портал Azure.](./media/arc-update-management/log-analytics-workspace.png)

## <a name="confirm-that-the-update-management-solution-is-deployed-on-your-azure-arc-enabled-server"></a>Убедитесь, что решение Управление обновлениями развернуто на сервере с поддержкой Arc Azure.

1. Щелкните **решения** в рабочей области log Analytics, а затем выберите решение " **обновления** " из списка, чтобы проверить ход оценки Управление обновлениями.

    ![Снимок экрана вкладки Solutions (решения) рабочей области Log Analytics.](./media/arc-update-management/solutions-tab.png)

   Управление обновлениями для получения достаточного объема данных может потребоваться несколько часов, чтобы отобразить оценку виртуальной машины. На следующей странице можно увидеть, что выполняется оценка.

   ![Снимок экрана с вкладкой обзора и представлением обновлений в рабочей области Log Analytics.](./media/arc-update-management/overview-tab.png)

   После завершения оценки вы увидите параметр **Просмотр сводки** на вкладке Управление обновлениями.

   ![Снимок экрана сводки представления обновлений в Log Analytics рабочей области.](./media/arc-update-management/updates-summary.png)

2. Выберите **Просмотреть сводку**, а затем щелкните еще раз для детализации оценки Управление обновлениями. В следующем примере можно увидеть, что на сервере с поддержкой Arc Azure отсутствуют обновления.

    ![Снимок экрана с обновлениями, отсутствующими на сервере с поддержкой дуги Azure.](./media/arc-update-management/updates-missing.png)

## <a name="schedule-an-update"></a>Планирование обновления

Теперь, когда мы настроили решение Управление обновлениями, вы можете развернуть обновления по заданному расписанию для сервера с поддержкой Arc Azure.

1. Перейдите к созданной ранее учетной записи службы автоматизации и выберите вкладку Управление обновлениями, как показано на следующем снимке экрана. Вы должны увидеть список серверов с поддержкой Arc Azure.

    ![Снимок экрана учетной записи службы автоматизации Azure.](./media/arc-update-management/azure-automation-account.png)

1. Выберите **запланировать развертывание обновлений**. На следующей странице Выберите операционную систему, которую использует сервер с поддержкой дуги Azure, а затем выберите **компьютеры для обновления** , как показано на следующем снимке экрана.

    ![Снимок экрана: планирование обновления с развертыванием обновлений.](./media/arc-update-management/schedule-an-update.png)

1. В раскрывающемся списке **тип** выберите **Компьютеры**, а затем выберите свой сервер и нажмите кнопку **ОК**.

    ![Снимок экрана типа и сервера, выбранных для запланированного обновления с развертыванием обновлений.](./media/arc-update-management/type-update.png)

1. Щелкните **Параметры расписания** , а затем укажите нужное расписание.

    ![Снимок экрана поля для настройки параметров расписания в развертывании обновлений.](./media/arc-update-management/config-schedule-settings.png)

    ![Снимок экрана с полями для параметров расписания в развертывании обновлений.](./media/arc-update-management/schedule-settings.png)

1. Наконец, укажите имя развертывания и нажмите кнопку **создать**.

    ![Снимок экрана с именем обновления в развертывании обновлений.](./media/arc-update-management/naming-update.png)

1. На вкладке Управление обновлениями учетной записи службы автоматизации вы сможете просмотреть запланированное развертывание обновлений на вкладке **расписания развертывания** .

    ![Снимок экрана запланированного обновления в управлении обновлениями.](./media/arc-update-management/scheduled-update.png)

Это Управление обновлениями решение обновит серверы с поддержкой ARC в Azure в окне развертывания на основе заданного вами расписания. [Управление обновлениями](/azure/automation/update-management/overview) , которые выходят за рамки этого сценария, можно сделать гораздо больше. Дополнительные сведения см. в [документации](/azure/automation/update-management/overview) .

## <a name="clean-up-your-environment"></a>Очистка среды

Выполните следующие действия, чтобы очистить среду.

1. Удалите виртуальные машины из каждой среды, следуя инструкциям по уничтожению, приведенным в каждом из руководств.

    - Экземпляр [обеспечить Ubuntu](./gcp-terraform-ubuntu.md) и [экземпляр обеспечить Windows](./gcp-terraform-windows.md)
    - [Экземпляр EC2 Ubuntu AWS](./aws-terraform-ubuntu.md)
    - [VMware VSPHERE виртуальной машины Ubuntu](./vmware-terraform-ubuntu.md) и [VMware vSphere виртуальной машины Windows Server](./vmware-terraform-windows.md)
    - [Vagrant Ubuntu](./local-vagrant-ubuntu.md) и [Vagrant Windows Box](./local-vagrant-windows.md)

1. Удалите ее.

    ```console
    az group delete --name <Name of your resource group>
    ```

    ![Снимок экрана команды "az Group Delete".](./media/arc-update-management/az-group-delete.png)
