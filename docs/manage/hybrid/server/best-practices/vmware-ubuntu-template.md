---
title: Создание шаблона VMware vSphere для Ubuntu Server 18,04
description: Создайте шаблон VMware vSphere для Ubuntu Server 18,04.
author: likamrat
ms.author: brblanch
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: think-tank, e2e-hybrid
ms.openlocfilehash: 1fac9dcacad7ff5f6230cdfdc9e18910a9792109
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101798548"
---
# <a name="create-a-vmware-vsphere-template-for-ubuntu-server-1804"></a>Создание шаблона VMware vSphere для Ubuntu Server 18,04

В этой статье приводятся рекомендации по созданию шаблона виртуальной машины Ubuntu Server 18,04 VMware vSphere.

## <a name="prerequisites"></a>Предварительные требования

> [!NOTE]
> В этом учебнике предполагается, что у вас есть несколько VMware vSphere знакомство. Кроме того, он не предназначен для просмотра рекомендаций по VMware или Ubuntu.

- [Скачайте последний ISO-файл Ubuntu Server 18,04](https://releases.ubuntu.com/18.04/)

- VMware vSphere 6,5 и выше

- Хотя его можно использовать локально, для ускорения развертывания отправьте файл в хранилище данных vSphere или в библиотеку содержимого vCenter.

## <a name="creating-ubuntu-1804-vm-template"></a>Создание шаблона виртуальной машины Ubuntu 18,04

### <a name="deploying-and-installing-ubuntu"></a>Развертывание и Установка Ubuntu

- Развернуть новую виртуальную машину

    ![Снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-1.png)

    ![Второй снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-2.png)

    ![Третий снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-3.png)

    ![Четвертый снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-4.png)

    ![Пятый снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-5.png)

    ![Шестой снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-6.png)

- Убедитесь, что в качестве гостевой ОС выбрано **Ubuntu Linux (64-бит)** .

    ![Снимок экрана Ubuntu Linux гостевой ОС (64-разрядная).](./media/vmware-template/ubuntu-template-guest-os.png)

- Укажите расположение ISO-файла Ubuntu Server.

    ![Седьмой снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-7.png)

    ![Восьмой снимок экрана создания новой VMware vSphere виртуальной машины.](./media/vmware-template/ubuntu-template-new-vm-8.png)

- Включите виртуальную машину и запустите установку Ubuntu. Здесь нет никаких специальных инструкций, но:

  - Используемых Рассмотрите возможность использования статического IP-адреса
  - Установка сервера OpenSSH

    ![Первый снимок экрана установки Ubuntu](./media/vmware-template/ubuntu-template-installation-1.png)

    ![Второй снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-2.png)

    ![Третий снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-3.png)

    ![Четвертый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-4.png)

    ![Пятый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-5.png)

    ![Шестой снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-6.png)

    ![Седьмой снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-7.png)

    ![Восьмой снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-8.png)

    ![Девятый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-9.png)

    ![Десятый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-10.png)

    ![Одиннадцатый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-11.png)

    ![Двенадцатый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-12.png)

    ![Снимок экрана тринадцатого установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-13.png)

    ![Снимок экрана четырнадцатого установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-14.png)

    ![Пятнадцатый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-15.png)

    ![Шестнадцатая снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-16.png)

    ![Снимок экрана семнадцатого установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-17.png)

    ![Снимок экрана восемнадцатого установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-18.png)

    ![Снимок экрана девятнадцатого установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-19.png)

    ![Двадцатый снимок экрана установки Ubuntu.](./media/vmware-template/ubuntu-template-installation-20.png)

    ![Снимок экрана установки Ubuntu на двадцать первых.](./media/vmware-template/ubuntu-template-installation-21.png)

### <a name="post-installation"></a>После установки

Перед преобразованием виртуальной машины в шаблон требуется выполнить несколько действий.

- Лучше использовать пакеты ОС в актуальном состоянии

    ```console
    sudo apt-get update
    sudo apt-get upgrade -y
    ```

- Запретить клаудконфиг сохранить исходное имя узла и сбросить имя узла

    ```console
    sudo sed -i 's/preserve_hostname: false/preserve_hostname: true/g' /etc/cloud/cloud.cfg
    sudo truncate -s0 /etc/hostname
    sudo hostnamectl set-hostname localhost
    ```

- Удалить текущую конфигурацию сети

    ```console
    sudo rm /etc/netplan/50-cloud-init.yaml
    ```

- Очистите журнал оболочки и завершите работу виртуальной машины

    ```console
    cat /dev/null > ~/.bash_history && history -c
    sudo shutdown now
    ```

### <a name="convert-to-template"></a>Преобразовать в шаблон

Сократите число ЦП виртуальной машины и ресурсы памяти до минимального значения и преобразуйте виртуальную машину в шаблон, переключайте дисковод CD/DVD на клиентское устройство, а также отключите его и преобразуйте виртуальную машину в шаблон.

![Снимок экрана, посвященный уменьшению количества ЦП и памяти виртуальной машины.](./media/vmware-template/ubuntu-template-reduce.png)

![Снимок экрана, посвященный преобразованию виртуальной машины в шаблон.](./media/vmware-template/ubuntu-template-convert.png)
