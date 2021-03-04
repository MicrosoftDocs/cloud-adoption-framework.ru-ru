---
title: Создание шаблона VMware vSphere для Windows Server 2019
description: Создайте шаблон VMware vSphere для Windows Server 2019.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 16a110dd380149aaa72cbb316cbb549eec12ef42
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102114274"
---
# <a name="create-a-vmware-vsphere-template-for-windows-server-2019"></a>Создание шаблона VMware vSphere для Windows Server 2019

В этой статье приводятся рекомендации по созданию шаблона виртуальной машины Windows Server 2019 VMware vSphere.

## <a name="prerequisites"></a>Предварительные требования

> [!NOTE]
> В этом руководство предполагается, что у вас есть несколько VMware vSphere знакомых, и вы знаете, как установить Windows Server. В нем также не рассмотрены рекомендации по использованию VMware или Windows.

- [Скачайте последнюю версию ISO-файла Windows Server](https://www.microsoft.com/windows-server/trial)

- VMware vSphere 6,5 и выше

- Хотя его можно использовать локально, для ускорения развертывания рекомендуется передать файл в хранилище данных vSphere или в библиотеку содержимого vCenter.

## <a name="creating-windows-server-2019-vm-template"></a>Создание шаблона виртуальной машины Windows Server 2019

### <a name="deploying-and-installing-windows-server"></a>Развертывание и установка Windows Server

1. Разверните новую виртуальную машину.

    ![Снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-1.png)

    ![Второй снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-2.png)

    ![Третий снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-3.png)

    ![Четвертый снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-4.png)

    ![Пятый снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-5.png)

    ![Шестой снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-6.png)

2. В качестве гостевой ОС обязательно выберите **Microsoft Windows Server 2016 или более поздней версии (64-bit)** .

    ![Снимок экрана гостевой ОС Windows Server.](./media/vmware-template/windows-template-guest-os.png)

3. Укажите расположение ISO-файла Windows Server.

    ![Седьмой снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-7.png)

    ![Восьмой снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/windows-template-new-vm-8.png)

- Включите виртуальную машину и запустите установку Windows Server.

    ![Первый снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-1.png)

    ![Второй снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-2.png)

    ![Третий снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-3.png)

    ![Четвертый снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-4.png)

    ![Пятый снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-5.png)

    ![Шестой снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-6.png)

    ![Седьмой снимок экрана установки Windows Server.](./media/vmware-template/windows-template-installation-7.png)

### <a name="post-installation"></a>После установки

Перед преобразованием виртуальной машины в шаблон необходимо выполнить несколько действий.

1. Установите средства VMware и перезапустите систему.

    ![Первый снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-1.png)

    ![Второй снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-2.png)

    ![Третий снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-3.png)

    ![Четвертый снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-4.png)

    ![Пятый снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-5.png)

    ![Шестой снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-6.png)

    ![Седьмой снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-7.png)

    ![Восьмой снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-8.png)

    ![Девятый снимок экрана установки средств VMware.](./media/vmware-template/windows-template-tools-9.png)

2. Выполнение обновлений Windows.

3. Измените политику выполнения PowerShell на `Bypass` , выполнив `Set-ExecutionPolicy -ExecutionPolicy Bypass` команду в PowerShell (ее можно настроить позже с помощью групповой политики или сценария PowerShell).

4. Разрешите подключение WinRM к операционной системе, запустив [`allow_winrm`](https://github.com/microsoft/azure_arc/blob/main/azure_arc_servers_jumpstart/vmware/winsrv/terraform/scripts/allow_winrm.ps1) сценарий PowerShell.

5. Ни один из приведенных ниже не является обязательным, но его следует учитывать для шаблона Windows:

    - Отключение контроля учетных записей (может быть позднее настроено с помощью групповой политики или сценария PowerShell)
    - Отключить брандмауэр защитника Windows (можно позднее настроить с помощью групповой политики или сценария PowerShell)
    - Отключение конфигурации усиленной безопасности Internet Explorer (ESC) (можно позднее настроить с помощью групповой политики или сценария PowerShell)
    - Включите удаленный рабочий стол.
    - В PowerShell установите [шоколад](https://chocolatey.org/install)

      ```powershell
      Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
      ```

    - Установите все базовые приложения, которые может потребоваться включить в шаблон.

### <a name="convert-to-template"></a>Преобразовать в шаблон

Сократите число ЦП виртуальной машины и ресурсы памяти до минимального значения и преобразуйте виртуальную машину в шаблон, переключайте дисковод CD/DVD на клиентское устройство, а также отключите его и преобразуйте виртуальную машину в шаблон.

![Снимок экрана, посвященный уменьшению количества ЦП и памяти виртуальной машины.](./media/vmware-template/windows-template-reduce.png)

![Снимок экрана, посвященный преобразованию виртуальной машины в шаблон.](./media/vmware-template/windows-template-convert.png)
