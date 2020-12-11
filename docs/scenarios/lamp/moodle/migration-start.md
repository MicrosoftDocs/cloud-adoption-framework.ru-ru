---
title: Действия по миграции Moodle вручную
description: Выполните следующие действия, чтобы импортировать Архив локального резервного копирования Moodle в ресурсы Azure и настроить приложение Moodle.
author: UmakanthOS
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: internal
ms.openlocfilehash: 905c1bff0dc31615c7b736f58beaf7aa51956054
ms.sourcegitcommit: b6f2b4f8db6c3b1157299ece1f044cff56895919
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97025611"
---
# <a name="moodle-manual-migration-steps"></a>Действия по миграции Moodle вручную

В этой статье описаны действия по импорту локального архива Moodle в базу данных Azure для MySQL, а также настройке приложения Azure Moodle.

Перед началом этого процесса обязательно выполните все действия, описанные в следующих статьях:

- [Подготовка к Moodle миграции](migration-pre.md)
- [Архитектура и шаблоны миграции Moodle](migration-arch.md)
- [Создание шлюза виртуальной сети и подключение к виртуальным машинам](vpn-gateway.md)

После завершения развертывания шаблона Azure Resource Manager (ARM) Войдите в [портал Azure](https://portal.azure.com/), перейдите к группе ресурсов, созданному шаблоном, и просмотрите все созданные ресурсы инфраструктуры. Созданные ресурсы будут выглядеть примерно так, как показано на следующем рисунке, в зависимости от используемого шаблона ARM.

![Снимок экрана, показывающий ресурсы инфраструктуры, созданные в группе ресурсов миграции Moodle.](images/resource-creation-overview.png)

## <a name="copy-the-moodle-archive"></a>Копирование архива Moodle

Скопируйте архив резервной копии Moodle из хранилища BLOB-объектов Azure в виртуальную машину контроллера (ВМ).

### <a name="sign-in-to-the-controller-virtual-machine"></a>Вход в виртуальную машину контроллера

1. Используйте бесплатный, эмулятор терминала с открытым исходным кодом или средство последовательной консоли [, например, для входа на](https://www.putty.org/) виртуальную машину контроллера (ВМ).

1. В поле **Конфигурация** выводимых данных введите общедоступный IP-адрес виртуальной машины контроллера в качестве **имени узла**.

1. В области навигации слева разверните узел **SSH**.

   ![Снимок экрана со страницей конфигурации выводимых данных.](images/putty-configuration.png)

1. Выберите **Проверка подлинности** и найдите файл ключа SSH, который использовался для развертывания инфраструктуры Azure с помощью шаблона ARM.

1. Выберите **Открыть**. В поле имя пользователя введите **azureadmin**, так как оно жестко запрограммировано в шаблоне.

   ![Снимок экрана с параметрами проверки подлинности SSH на странице "Конфигурация".](images/putty-ssh-key.png)

Дополнительные сведения о выводимых данных см. в разделе Общие вопросы и [ответы об устранении неполадок](https://documentation.help/PuTTY/faq.html).

### <a name="download-and-install-azcopy-on-the-controller-vm"></a>Скачайте и установите AzCopy на виртуальной машине контроллера.

После входа в виртуальную машину контроллера выполните следующие команды, чтобы установить AzCopy:

  ```bash
  sudo -s
  wget https://aka.ms/downloadazcopy-v10-linux
  tar -xvf downloadazcopy-v10-linux
  sudo rm /usr/bin/azcopy
  sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
  ```

### <a name="copy-the-archive-to-the-controller-vm"></a>Копирование архива на виртуальную машину контроллера

1. Выполните следующие команды, чтобы скачать сжатый `storage.tar.gz` файл резервной копии из хранилища BLOB-объектов Azure в каталог виртуальных машин контроллера `/home/azureadmin/` :

   ```bash
   sudo -s
   cd /home/azureadmin/
   azcopy copy 'https://<storageaccount>.blob.core.windows.net/container/BlobDirectoryName<SAStoken>' '/home/azureadmin/'
   ```

Замените учетную запись хранения и значения токенов SAS. Пример.

   `azcopy copy 'https://onpremisesstorage.blob.core.windows.net/migration/storage.tar.gz?sv=2019-12-12&ss=' /home/azureadmin/storage.tar.gz`

1. Извлеките сжатый файл в каталог.

   ```bash
   d /home/azureadmin
   ar -zxvf storage.tar.gz
   ```

### <a name="back-up-the-current-configuration"></a>Создание резервной копии текущей конфигурации

Перед миграцией создайте резервную копию текущей конфигурации. Каталог резервного копирования извлекается `storage` по адресу `home/azureadmin` . Этот `storage` Каталог содержит `moodle` `moodledata` каталоги конфигурации, и, а также файл резервной копии базы данных, который копируется в нужные расположения.

1. Создайте каталог резервного копирования:

   ```bash
   cd /home/azureadmin/
   mkdir -p backup
   mkdir -p backup/moodle
   mkdir -p backup/moodle/html
   ```

1. Создайте резервные копии `moodle` `moodledata` каталогов и.

   ```bash
   mv /moodle/html/moodle /home/azureadmin/backup/moodle/html/moodle
   mv /moodle/moodledata /home/azureadmin/backup/moodle/moodledata
   ```

1. Скопируйте `moodle` каталоги и `moodledata` в общую папку `/moodle` .

   ```bash
   cp -rf /home/azureadmin/storage/moodle /moodle/html/
   cp -rf /home/azureadmin/storage/moodledata /moodle/moodledata
   ```

## <a name="import-the-moodle-database-to-azure"></a>Импорт базы данных Moodle в Azure

Подключитесь к базе данных Azure для сервера MySQL и импортируйте Архив локальной базы данных Moodle в базу данных Azure для MySQL.

### <a name="connect-to-the-mysql-server"></a>Подключение к серверу MySQL

Экземпляры базы данных Azure для MySQL защищены брандмауэром. По умолчанию все соединения с сервером и базами данных, расположенными на сервере, отклоняются. Прежде чем подключиться к базе данных Azure для MySQL в первый раз, настройте брандмауэр для разрешения доступа к общедоступному IP-адресу или диапазону IP-адресов виртуальной машины контроллера.

Брандмауэр можно настроить с помощью командной строки Azure (Azure CLI) или портал Azure.

Выполните следующую команду Azure CLI, заменив собственные значения заполнителей:

```azurecli
az mysql server firewall-rule create --resource-group <myresourcegroup> --server <mydemoserver> --name <AllowMyIP> --start-ip-address <192.168.0.1> --end-ip-address <192.168.0.1>
```

На портал Azure выберите сервер базы данных Azure для MySQL из развернутых ресурсов инфраструктуры Moodle. На левой панели навигации на странице сервера выберите **Безопасность подключения**.

Вы можете добавить разрешенные IP-адреса и настроить правила брандмауэра. После создания правил нажмите кнопку **сохранить** .

![Снимок экрана: панель "безопасность подключения" для сервера базы данных Azure для MySQL.](images/database-connection-security.png)

Теперь вы можете подключиться к серверу MySQL с помощью программы командной строки [MySQL](https://dev.mysql.com/doc/refman/8.0/en/mysql.html) или [MySQL Workbench](https://dev.mysql.com/doc/workbench/en/).

![Снимок экрана: Установка нового подключения в MySQL Workbench.](images/database-connection.png)

Чтобы получить сведения о подключении, перейдите на страницу **обзора** сервера MySQL в портал Azure. Используйте значки копирования рядом с каждым полем, чтобы скопировать **имя сервера** и **имя входа администратора сервера**.

Например, имя сервера может быть `mydemoserver.mysql.database.azure.com` , а имя входа администратора сервера — `myadmin@mydemoserver` .

Вам также потребуется пароль. Если необходимо сбросить пароль, в строке меню выберите **Сброс пароля** .

Используйте сведения о сервере базы данных в следующих разделах.

### <a name="import-the-moodle-database-to-azure-database-for-mysql"></a>Импорт базы данных Moodle в базу данных Azure для MySQL

1. Создайте базу данных MySQL для импорта локальной базы данных в:

   ```bash
   mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "CREATE DATABASE $moodledbname CHARACTER SET utf8;"
   ```

1. Назначьте правильные разрешения для базы данных:

   ```bash
   mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "GRANT ALL ON $moodledbname.* TO '$server_admin_login_name' IDENTIFIED BY '$admin_password';"
   ```

1. Импортируйте базу данных:

   ```bash
   mysql -h $server_name -u $server_admin_login_name -p$admin_password $moodledbname < /home/azureadmin/storage/database.sql
   ```

## <a name="update-configurations"></a>Обновить конфигурации

После импорта архива локальной базы данных Moodle в базу данных Azure для MySQL при необходимости обновите следующие конфигурации на виртуальной машине контроллера:

- Обновите файл конфигурации Moodle.
- Настройте разрешения для каталога.
- Настройка веб-серверов PHP и nginx.
- Обновите DNS-имя и другие переменные.
- Установите все отсутствующие расширения PHP.
- Перезапустите, а затем закройте веб-серверы.
- Скопируйте файлы конфигурации в общую папку для копирования в масштабируемые наборы виртуальных машин.

### <a name="update-the-moodle-config-file"></a>Обновление файла конфигурации Moodle

Обновите параметры сведений о базе данных в файле конфигурации Moodle `/moodle/config.php` .

Чтобы получить DNS-имя для этой задачи, сделайте следующее:

1. В портал Azure выберите **Load Balancer общедоступный IP-адрес** из развернутых ресурсов инфраструктуры Moodle.

1. На странице **Обзор** щелкните значок копирования рядом с **DNS-именем**. Чтобы обновить `config.php` файл, выполните следующие действия.

1. Введите следующие команды для редактирования `config.php` в `nano` редакторе:

   ```bash
   cd /moodle/html/moodle/
   nano config.php
   ```

1. Обновите сведения о базе данных в файле, используя значения, скопированные из портал Azure:

   ```php
   $CFG->dbhost    = 'localhost';                // Change 'localhost' to the server name.
   $CFG->dbname    = 'moodle';                   // Change 'moodle' to the newly created database name.
   $CFG->dbuser    = 'root';                     // Change 'root' to the server admin login name.
   $CFG->dbpass    = 'password';                 // Change 'password' to the server admin login password.
   $CFG->wwwroot   = 'https://on-premises.com';  // Change 'on-premises' to the DNS name.
   $CFG->dataroot  = '/var/moodledata';          // Change the path to '/moodle/moodledata'.
   ```

1. После внесения изменений нажмите клавиши CTRL + O, чтобы сохранить файл, и CTRL + X, чтобы выйти из редактора.

Локальный каталог можно сохранить `dataroot` в любом расположении.

### <a name="configure-directory-permissions"></a>Настройка разрешений для каталога

- Назначьте в каталог разрешения 755 и www-data owner: Group `moodle` .

  ```bash
  sudo chmod 755 /moodle/html/moodle sudo chown -R www-data:www-data /moodle/html/moodle
  ```

- Назначьте в каталог разрешения 770 и www-data owner: Group `moodledata` .

  ```bash
  sudo chmod 770 /moodle/moodledata sudo chown -R www-data:www-data /moodle/moodledata
  ```

### <a name="update-web-config-files"></a>Обновление файлов веб-конфигурации

Создайте резервную копию и обновите `conf` файл nginx:

```bash
sudo mv /etc/nginx/sites-enabled/*.conf /home/azureadmin/backup/
cd /home/azureadmin/storage/configuration/
sudo cp -rf nginx/sites-enabled/*.conf /etc/nginx/sites-enabled/
```

Создайте резервную копию и обновите `www.conf` файл PHP:

```bash
_PHPVER='/usr/bin/php -r "echo PHP_VERSION;" | /usr/bin/cut -c 1,2,3'
echo $_PHPVER
sudo mv /etc/php/$_PHPVER/fpm/pool.d/www.conf /home/azureadmin/backup/www.conf
sudo cp -rf /home/azureadmin/storage/configuration/php/$_PHPVER/fpm/pool.d/www.conf /etc/php/$_PHPVER/fpm/pool.d/
```

### <a name="update-nginx-configuration-variables"></a>Обновление переменных конфигурации nginx

Обновите DNS-имя облака Azure, чтобы оно было DNS-именем локального приложения Moodle.

1. Откройте файл конфигурации nginx:

   ```bash
   nano /etc/nginx/sites-enabled/*.conf
   ```

1. При развертывании шаблона ARM для сервера nginx устанавливается порт 81. Обновите `SERVER_PORT` файл в файле до 81, если он не равен 81.

1. Обновите `server_name` . Например, для `server_name on-premises.com` обновите `on-premises.com` с помощью DNS-имени. В большинстве случаев DNS-имя не изменяется при миграции.

1. Обновите `root` расположение каталога HTML. Например, измените `root /var/www/html/moodle;` на `root /moodle/html/moodle;`. Локальный корневой каталог может находиться в любом расположении.

1. После внесения изменений нажмите клавиши CTRL + O, чтобы сохранить файл и CTRL + X для выхода.

### <a name="install-any-missing-php-extensions"></a>Установка отсутствующих расширений PHP

Шаблоны развертывания ARM устанавливают следующие расширения PHP: FPM, CLI, парные, ZIP, груши, mbstring, dev, мкрипт, SOAP, JSON, Redis, бкмас, GD, MySQL, ксмлрпк, Intl, XML и bz2. Если локальное приложение Moodle имеет какие-либо расширения PHP, которые отсутствуют на виртуальной машине контроллера, их можно установить вручную.

Чтобы получить список расширений PHP в локальном приложении, выполните:

```bash
php -m
```

Чтобы установить недостающие расширения, выполните команду:

```bash
sudo apt-get install -y php-<extension>
```

### <a name="restart-and-stop-the-web-servers"></a>Перезапуск и завершение веб-серверов

1. Перезапустите веб-серверы.

   ```bash
   sudo systemctl restart nginx
   sudo systemctl restart php$_PHPVER-fpm
   ```

1. Останавливает веб-серверы.

   ```bash
   sudo systemctl stop nginx
   sudo systemctl stop php$_PHPVER-fpm
   ```

Когда запрос достигает Azure Load Balancer, он перенаправляется к экземплярам масштабируемого набора виртуальных машин, а не к виртуальной машине контроллера.

### <a name="copy-configuration-files"></a>Копировать файлы конфигурации

Скопируйте файлы конфигурации PHP и веб-сервера в общее расположение для последующего копирования в экземпляры масштабируемых наборов виртуальных машин.

Чтобы создать каталог для файлов конфигурации в общем расположении, выполните:

```bash
mkdir -p /moodle/config
mkdir -p /moodle/config/php
mkdir -p /moodle/config/nginx
```

Чтобы скопировать файлы конфигурации PHP и веб-сервера в общий каталог, выполните команду:

```bash
cp /etc/nginx/sites-enabled/* /moodle/config/nginx
cp /etc/php/$_PHPVER/fpm/pool.d/www.conf /moodle/config/php
```

## <a name="next-steps"></a>Дальнейшие действия

Продолжайте [настраивать экземпляр контроллера Moodle и рабочие узлы](azure-infra-config.md) для следующих шагов в процессе миграции Moodle.
