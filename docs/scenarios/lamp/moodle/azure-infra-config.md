---
title: Настройка рабочих узлов Moodle
description: Узнайте, как настроить масштабируемый набор виртуальных машин для Moodle. Узнайте, как получить доступ к масштабируемому набору из контроллера, используя частный IP-адрес.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 902c7b93e88725ec7c37ddaac09f92db8287af49
ms.sourcegitcommit: 32e8e7a835a688eea602f2af1074aa926ab150c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2020
ms.locfileid: "97687646"
---
# <a name="how-to-set-up-moodle-worker-nodes"></a>Настройка рабочих узлов Moodle

Выполните следующие действия, чтобы настроить масштабируемый набор виртуальных машин или рабочие узлы для Moodle.

## <a name="virtual-machine-scale-set-instances"></a>Экземпляры масштабируемых наборов виртуальных машин

Экземпляру масштабируемого набора виртуальных машин назначается частный IP-адрес. Доступ к этому IP-адресу можно получить только с помощью виртуальной машины контроллера, которая находится в той же виртуальной сети, что и IP-адрес. В этой статье описывается, как настроить этот IP-адрес, а затем настроить масштабируемый набор виртуальных машин Azure, создаваемый при миграции Moodle.

### <a name="access-the-virtual-machine-scale-set"></a>Доступ к масштабируемому набору виртуальных машин

Чтобы получить доступ к масштабируемому набору виртуальных машин, выполните следующие действия.

1. Определите частный IP-адрес, используемый Azure для экземпляра масштабируемого набора виртуальных машин:

   1. Войдите в [портал Azure](https://ms.portal.azure.com/#home)и выберите группу ресурсов, созданную развертыванием.

   1. Откройте страницу для ресурса масштабируемого набора виртуальных машин.

   1. На панели слева выберите **экземпляры**.

   1. Откройте выполняющийся экземпляр. В разделе **Обзор** скопируйте частный IP-адрес, связанный с этим экземпляром.

1. Введите следующие команды для входа в масштабируемый набор виртуальных машин из виртуальной машины контроллера:

   ```bash
   sudo -s
   sudo ssh azureadmin@<private IP address>
   ```

   В команде `<private IP address>` — это частный IP-адрес масштабируемого набора виртуальных машин. Например, введите:

   ```bash
   sudo -s
   sudo ssh azureadmin@172.31.X.X
   ```

### <a name="create-a-backup-directory"></a>Создание каталога резервного копирования

На [предыдущем этапе процесса миграции файлы резервной копии были извлечены](./migration-start.md#back-up-the-current-configuration) в каталог, указанный `storage` в `/home/azureadmin` . Этот `storage` Каталог содержит `moodle` каталоги и `moodledata` , каталог конфигурации и файл резервной копии базы данных. После входа в экземпляр виртуальной машины масштабируемого набора введите следующие команды, чтобы создать каталог резервного копирования для этих файлов:

```bash
cd /home/azureadmin/
mkdir -p backup
mkdir -p backup/moodle
```

### <a name="configure-the-php-and-web-server"></a>Настройка PHP и веб-сервера
Чтобы настроить PHP и веб-сервер, сделайте следующее:

1. Задайте в качестве версии PHP переменную:

   ```bash
   _PHPVER=`/usr/bin/php -r "echo PHP_VERSION;" | /usr/bin/cut -c 1,2,3`
   echo $_PHPVER
   ```

1. Создайте резервную копию конфигураций PHP и веб-сервера:

   ```bash
   sudo mv /etc/nginx/sites-enabled/*.conf /home/azureadmin/backup/
   sudo mv /etc/php/$_PHPVER/fpm/pool.d/www.conf /home/azureadmin/backup/www.conf  
   ```

1. Скопируйте файлы конфигурации PHP и веб-сервера:

   ```bash
   sudo cp /moodle/config/nginx/*.conf  /etc/nginx/sites-enabled/
   sudo cp /moodle/config/php/www.conf /etc/php/$_PHPVER/fpm/pool.d/
   ```

### <a name="install-missing-extensions"></a>Установить недостающие расширения

Выполните следующие действия, чтобы установить недостающие расширения:

1. Чтобы получить список расширений PHP, установленных в локальной среде, введите следующую команду на локальной виртуальной машине:

   ```bash
   php -m
   ```

1. Используйте шаблон Azure Resource Manager для установки следующих расширений PHP: FPM, CLI, мкрипт, ZIP, груши, mbstring, dev,, SOAP, JSON, Redis, бкмас, GD, MySQL, ксмлрпк, Intl, XML и bz2.

1. Если в локальном приложении Moodle есть дополнительные расширения PHP, которые отсутствуют на виртуальной машине контроллера, установите их вручную с помощью следующей команды:

   ```bash
   sudo apt-get install -y php-<extension name>
   ```

## <a name="next-steps"></a>Дальнейшие действия

Перейдите к [дальнейшим действиям после Moodle миграции](./migration-post.md).
