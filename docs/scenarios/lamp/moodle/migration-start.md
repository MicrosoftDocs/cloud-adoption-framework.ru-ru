---
title: Запуск Moodle миграции вручную
description: Узнайте, как начать Moodle миграцию вручную.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 2fbaf59de2effb689d160aa22a41c51ed291b98e
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714681"
---
# <a name="how-to-start-a-manual-moodle-migration"></a>Запуск Moodle миграции вручную

Чтобы начать миграцию Moodle, войдите в [Azure](https://portal.azure.com/) после завершения развертывания. Перейдите к созданной группе ресурсов и найдите все созданные ресурсы. На следующем рисунке показано, как будут создаваться ресурсы:

[Обзор ресурсов](./images/resource-creation-overview.png)

## <a name="controller-virtual-machine"></a>Виртуальная машина контроллера

- Для входа на компьютер контроллера используйте бесплатный эмулятор терминала с открытым исходным кодом или средство последовательной консоли.
- Скопируйте общедоступный IP-адрес виртуальной машины контроллера, который будет использоваться в качестве имени узла.
- Разверните узел **SSH** на панели навигации, выберите **Проверка подлинности** и найдите файл ключа SSH из раздела Развертывание инфраструктуры Azure с помощью шаблона Azure Resource Manager.
- Щелкните **Open**(Открыть). Вам будет предложено ввести имя пользователя. Введите **azureadmin**, так как он жестко запрограммирован в шаблоне.

[Страница выводимого имени входа.](./images/putty-login.png)

[Критерии выводимых ключей.](./images/putty-key-criteria.png)

- Найдите и выберите ключ SSH, а затем нажмите кнопку Открыть.

Просмотрите [Общие вопросы и ответы об устранении неполадок](https://documentation.help/PuTTY/faq.html) , чтобы узнать больше о выводимых сведениях.

После входа выполните следующий набор команд для миграции.

## <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy

Выполните следующие команды для установки AzCopy:

  ```bash
  sudo -s
  wget https://aka.ms/downloadazcopy-v10-linux
  tar -xvf downloadazcopy-v10-linux
  sudo rm /usr/bin/azcopy
  sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
  ```

## <a name="copy-the-backup"></a>Копирование резервной копии

Чтобы скопировать архив резервной копии в экземпляр виртуальной машины контроллера из развертывания Azure Resource Manager:

- Скачайте сжатый файл резервной копии (Storage. tar. gz) из хранилища BLOB-объектов на виртуальную машину контроллера в расположении/Хоме/азуреадмин/.

  ```bash
  sudo -s
  cd /home/azureadmin/
  azcopy copy `https://storageaccount.blob.core.windows.net/container/BlobDirectoryName<SASToken>` `/home/azureadmin/`
  ```

  Пример: `azcopy copy 'https://onpremisesstorage.blob.core.windows.net/migration/storage.tar.gz?sv=2019-12-12&ss=' /home/azureadmin/storage.tar.gz`

- Извлеките сжатое содержимое в каталог.

  ```bash
  d /home/azureadmin
  ar -zxvf storage.tar.gz
  ```

## <a name="how-to-migrate-and-configure-a-moodle-application"></a>Как перенести и настроить приложение Moodle

Перед миграцией создайте резервную копию текущей конфигурации. Каталог резервного копирования извлекается как `storage/at/home/azureadmin` . Этот каталог хранения содержит каталоги Moodle, мудледата и конфигурации и файл резервной копии базы данных. Они будут скопированы в нужные расположения.

- Создайте каталог резервного копирования.

  ```bash
  cd /home/azureadmin/
  mkdir -p backup
  mkdir -p backup/moodle
  mkdir -p backup/moodle/html
  ```

- Создайте резервную копию каталогов Moodle и мудледата.

  ```bash
  mv /moodle/html/moodle /home/azureadmin/backup/moodle/html/moodle
  mv /moodle/moodledata /home/azureadmin/backup/moodle/moodledata
  ```

- Скопируйте локальные каталоги Moodle и мудледата в общее расположение ( `/moodle` ).

  ```bash
  cp -rf /home/azureadmin/storage/moodle /moodle/html/
  cp -rf /home/azureadmin/storage/moodledata /moodle/moodledata
  ```

- Импортируйте базу данных Moodle в Azure. Экземпляры базы данных Azure для MySQL защищены брандмауэром. По умолчанию все подключения к серверу и базам данных на сервере отклоняются. Прежде чем подключиться к базе данных Azure для MySQL в первый раз, настройте брандмауэр, добавив IP-адрес или диапазон IP-адресов общедоступного клиентского компьютера.

  ```bash
  az mysql server firewall-rule create --resource-group myresourcegroup --server mydemoserver --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1
  ```

- Выберите новый сервер MySQL, а затем — **Безопасность подключения**.

![Выберите * * безопасность подключения * *.](./images/database-connection-security.png)

- Вы можете добавить IP-адрес или настроить правила брандмауэра здесь. После создания правил нажмите кнопку **сохранить** .

Теперь можно подключиться к серверу с помощью программы командной строки MySQL или средства MySQL Workbench. Чтобы получить сведения о подключении, скопируйте **имя сервера** и **имя входа администратора сервера** на странице **ресурсов сервера MySQL** . Для этого можно нажать кнопку Копировать рядом с каждым полем.

![Настройка нового подключения.](images/database-connection.png)

Например, если имя сервера — `mydemoserver.mysql.database.azure.com` , а имя для входа администратора сервера — `myadmin@mydemoserver` .

- Перед импортом базы данных убедитесь, что сведения о базе данных Azure для сервера MySQL готовы.
- Перейдите к портал Azure и перейдите к созданной группе ресурсов.
- Выберите ресурс сервера базы данных Azure для MySQL.
- На панели Обзор найдите сведения о сервере базы данных Azure для MySQL, такие как имя сервера, имя для входа администратора сервера.
- Сбросьте пароль, нажав кнопку Сбросить пароль в верхней части страницы.

Используйте следующие сведения о сервере базы данных для следующих команд:

- Импортируйте локальную базу данных в базу данных Azure для MySQL.

- Создайте базу данных для импорта локальной базы данных.

  ```bash
  mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "CREATE DATABASE $moodledbname CHARACTER SET utf8;"
  ```

- Назначение прав доступа к базе данных.

  ```bash
  mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "GRANT ALL ON $moodledbname.* TO `$server_admin_login_name` IDENTIFIED BY `$admin_password`;"
  ```

- Импортируйте базу данных.

  ```bash
  mysql -h $server_name -u $server_admin_login_name -p$admin_password $moodledbname < /home/azureadmin/storage/database.sql
  ```

- Обновите сведения о базе данных в файле конфигурации Moodle (/мудле/конфиг.ФП).

Обновление параметров в файле config. php. Обязательно сохраните DNS-имя для этой задачи:

- Перейдите к портал Azure и найдите группу ресурсов.

- Выберите **общедоступный IP-адрес Load Balancer** и получите DNS-имя на панели " **Обзор** ":

  дбхост, dbname, дбусер, дбпасс, root и wwwroot

  ```bash
  cd /moodle/html/moodle/
  nano config.php

- Update the database details, and save the file.

  For example:

  - $CFG->dbhost    = `localhost`;                - Change `localhost` to the server name.
  - $CFG->dbname    = `moodle`;                   - Change `moodle` to the newly created database name.
  - $CFG->dbuser    = `root`;                     - Change `root` to the server admin login name.
  - $CFG->dbpass    = `password`;                 - Change `password` to the server admin login password.
  - $CFG->wwwroot   = `https://on-premises.com`;  - Change `on-premises` to the DNS name.
  - $CFG->dataroot  = `/var/moodledata`;          - Change the path to `/moodle/moodledata`.

The on-premises `dataroot` directory can be stored at any location. After making the changes, save the file. Press `CTRL+O` to save and `CTRL+X` to exit.

Configure directory permissions.

- Set 755 and www-data owner:group permissions to the Moodle directory.

  ```bash
  sudo chmod 755 /moodle/html/moodle sudo chown -R www-data:www-data /moodle/html/moodle
   ```

- Установите разрешения 770 и www-data owner: Group в каталог мудледата.

  ```bash
  sudo chmod 770 /moodle/moodledata sudo chown -R www-data:www-data /moodle/moodledata
  ```

- Обновите файл nginx CONF.

  ```bash
  sudo mv /etc/nginx/sites-enabled/*.conf /home/azureadmin/backup/
  cd /home/azureadmin/storage/configuration/
  sudo cp -rf nginx/sites-enabled/*.conf /etc/nginx/sites-enabled/
  ```

- Обновите файл конфигурации PHP.

  ```bash
  _PHPVER=`/usr/bin/php -r "echo PHP_VERSION;" | /usr/bin/cut -c 1,2,3`
  echo $_PHPVER
  sudo mv /etc/php/$_PHPVER/fpm/pool.d/www.conf /home/azureadmin/backup/www.conf
  sudo cp -rf /home/azureadmin/storage/configuration/php/$_PHPVER/fpm/pool.d/www.conf /etc/php/$_PHPVER/fpm/pool.d/
  ```

- Установите отсутствующие расширения PHP. Шаблоны Azure Resource Manager устанавливают следующие расширения PHP: FPM, CLI, мкрипт, ZIP, груша, mbstring, dev,, SOAP, JSON, Redis, бкмас, GD, MySQL, ксмлрпк, Intl, XML и bz2. Чтобы получить список расширений PHP, установленных в локальной среде, выполните следующую команду:

  ```bash
  php -m
  ```

- Если в локальной среде есть дополнительные расширения PHP, отсутствующие в виртуальной машине контроллера, их можно установить вручную.

  ```bash
  sudo apt-get install -y php-<extensionName>
  ```

- Обновите DNS-имя и расположение корневого каталога. Обновите DNS-имя облака Azure с помощью локального DNS-имени. Эта команда открывает файл конфигурации:

  ```bash
  nano /etc/nginx/sites-enabled/*.conf
  ```

- Azure Resource Manager развертывании шаблона задаст сервер nginx через порт 81. Обновите порт сервера до 81, если он не равен 81.

- Обновите имя сервера. Например, если server_name on-premises.com, обновите on-premises.com, указав DNS-имя. В большинстве случаев DNS может остаться в процессе миграции.

- Обновите расположение корневого каталога HTML. Например, если необходимо `root /var/www/html/moodle;` , обновите его до `root /moodle/html/moodle;` .

- Локальный корневой каталог может находиться в любом расположении.

- После внесения изменений нажмите, `CTRL+O` чтобы сохранить файл и `CTRL+X` выйти.

- Перезапустите веб-серверы.

  ```bash
  sudo systemctl restart nginx
  sudo systemctl restart php$_PHPVER-fpm  
  ```

- Останавливает веб-серверы. Когда запрос достигает Azure Load Balancer, он будет перенаправлен на экземпляры масштабируемого набора виртуальных машин, но не на виртуальную машину контроллера.

  ```bash
  sudo systemctl stop nginx
  sudo systemctl stop php$_PHPVER-fpm  
  ```

## <a name="how-to-copy-configuration-files"></a>Копирование файлов конфигурации

Скопируйте файлы конфигурации PHP и веб-сервера в общее расположение. Файлы конфигурации можно копировать в экземпляры масштабируемых наборов виртуальных машин из общего расположения.

Чтобы создать каталог для конфигурации в общем расположении, выполните следующие действия.

```bash
mkdir -p /moodle/config
mkdir -p /moodle/config/php
mkdir -p /moodle/config/nginx
```

Чтобы скопировать файлы конфигурации PHP и веб-сервера в каталог конфигурации, выполните следующие действия.

```bash
cp /etc/nginx/sites-enabled/* /moodle/config/nginx
cp /etc/php/$_PHPVER/fpm/pool.d/www.conf /moodle/config/php
```

## <a name="next-steps"></a>Следующие шаги

Перейдите к статье о [том, как настроить экземпляр контроллера Moodle и рабочие узлы (конфигурация инфраструктуры Azure)](./azure-infra-config.md) , чтобы получить сведения о дальнейших действиях в процессе миграции Moodle.
