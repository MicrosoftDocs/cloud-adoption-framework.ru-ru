---
title: Подготовка к Moodle миграции
description: Узнайте, как подготовиться к Moodle миграции. См. раздел Резервное копирование файлов Moodle и создание ресурсов, необходимых для миграции.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 4a4a3ce829263aaac9806f03ee7b743f0e225016
ms.sourcegitcommit: 32e8e7a835a688eea602f2af1074aa926ab150c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2020
ms.locfileid: "97687711"
---
# <a name="how-to-prepare-for-a-moodle-migration"></a>Подготовка к Moodle миграции

Перед миграцией приложения Moodle из локальной среды в Azure необходимо экспортировать данные. В этом руководстве описываются шаги процесса экспорта.

## <a name="install-the-azure-cli"></a>Установка Azure CLI

Выполните следующие действия, чтобы настроить Azure CLI в локальной среде.

1. На узле, который можно использовать для задач Azure, введите следующую команду, чтобы установить Azure CLI:

   ```bash
   curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
   ```

1. В Azure CLI введите следующую команду, чтобы войти в учетную запись Azure:

   ```bash
   az login -u <username> -p <password>
   ```

1. Если Azure CLI открывает окно или вкладку браузера, войдите в Azure с помощью учетная запись Майкрософт. Если окно браузера не открывается, перейдите к [https://aka.ms/devicelogin](https://aka.ms/devicelogin) и введите код авторизации, отображаемый в терминале.

## <a name="create-a-subscription"></a>Создание подписки

Пропустите этот шаг, если у вас уже есть подписка Azure.

Если у вас нет подписки Azure, вы можете [создать ее бесплатно](https://azure.microsoft.com/free/). Можно также настроить [подписку с оплатой по мере](https://azure.microsoft.com/offers/ms-azr-0003p/)использования или создать подписку в портал Azure.

- Чтобы использовать портал Azure для создания подписки, откройте [подписки](https://ms.portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), выберите **Добавить** и введите необходимые сведения.

  ![Снимок экрана со страницей "подписки" в портал Azure.](./images/azure-subscriptions-page.png)

- Чтобы использовать Azure CLI для создания подписки, введите следующую команду:

  ```azurecli
  az account set --subscription '<subscription name>'
  ```

 Пример команды:

  `az account set --subscription 'ComputePM LibrarySub'`

## <a name="create-a-resource-group"></a>Создание группы ресурсов

После настройки подписки Azure создайте группу ресурсов в Azure. Для создания группы ресурсов можно использовать портал Azure **или** Azure CLI.

- Чтобы использовать портал Azure, выполните следующие действия.

  1. Откройте [группы ресурсов](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceGroups)и выберите **Добавить**.
  
  1. Введите имя подписки, имя группы ресурсов и регион. Список доступных регионов см. [в статье местонахождение данных в Azure](https://azure.microsoft.com/global-infrastructure/data-residency/) . Запишите имя введенной группы ресурсов, чтобы это имя можно было использовать в последующих шагах.
  
  1. Выберите **Review + create** (Просмотреть и создать).

  ![Снимок экрана: страница "Создание группы ресурсов" в полях "портал Azure", "Подписка", "Группа ресурсов" и "Проверка + создать".](./images/resource-group.png)

- Чтобы использовать Azure CLI для создания группы ресурсов, введите следующую команду:

  ```azurecli
  az group create -l <region> -n <resource group name> -s '<subscription name>'
  ```

  Например, введите:

  `az group create -l eastus -n manual_migration -s 'ComputePM LibrarySub'`

  Значение, предоставленное с помощью `-l` параметра, указывает расположение по умолчанию. Используйте то же расположение, которое использовалось на предыдущих шагах. Запишите имя создаваемой группы ресурсов и используйте это имя в последующих шагах.

## <a name="create-a-storage-account"></a>Создание учетной записи хранения

Затем создайте учетную запись хранения в только что созданной группе ресурсов. Эта учетная запись хранения будет использоваться для резервного копирования локальных данных Moodle.

Для создания учетной записи хранения можно либо использовать портал Azure, **либо** Azure CLI.

- Чтобы использовать портал Azure, выполните следующие действия.

  1. Откройте [создать учетную запись хранения](https://ms.portal.azure.com/#create/Microsoft.StorageAccount).

  1. Введите следующие сведения:

     - Имя подписки Azure.
     - Имя только что созданной группы ресурсов
     - Имя учетной записи хранения
     - Ваш регион
   
  1. В поле **тип учетной записи** выберите **блобстораже** из раскрывающегося списка.
  
  1. Для **репликации** выберите **геоизбыточное хранилище с доступом на чтение (RA-GRS)** из раскрывающегося списка.

  1. Выберите **Review + create** (Просмотреть и создать).

  ![Снимок экрана со страницей создания учетной записи хранения в портал Azure с несколькими полями ввода и кнопкой "Проверка и создание".](./images/create-storage-account.png)

- Чтобы использовать Azure CLI для создания учетной записи хранения, введите следующую команду:

  ```azurecli
  az storage account create -n <storage account name> -g <resource group name> --sku <storage account SKU> --kind <storage account type> -l <region>
  ```

  Пример команды:

  `az storage account create -n onpremisesstorage -g manual_migration --sku Standard_LRS --kind BlobStorage -l eastus`

  `--kind`Параметр указывает тип учетной записи хранения.

## <a name="back-up-on-premises-data"></a>Резервное копирование локальных данных

Перед резервным копированием локальных данных Moodle включите **режим обслуживания** на веб-сайте Moodle, выполнив следующие действия.

1. В экземпляре Moodle в локальной среде введите следующую команду:

   ```bash
   sudo /usr/bin/php admin/cli/maintenance.php --enable
   ```

2. Введите следующую команду, чтобы проверить состояние веб-сайта Moodle:

   ```bash
   sudo /usr/bin/php admin/cli/maintenance.php
   ```

При резервном копировании локальных файлов, конфигураций и баз данных Moodle и мудледата рекомендуется создавать резервные копии этих ресурсов в одном каталоге. Эта идея представлена на следующей схеме:

![Схема, показывающая структуру каталога хранилища резервных копий Moodle.](./images/directory-structure.png)

### <a name="create-a-storage-directory"></a>Создание каталога хранилища

Перед копированием данных создайте пустой каталог хранилища в любом нужном месте. Например, если расположение — `/home/azureadmin` , введите следующие команды:

  ```bash
  sudo -s
  cd /home/azureadmin
  mkdir storage
  ```

### <a name="back-up-moodle-directories"></a>Резервное копирование каталогов Moodle

В локальной среде `moodle` Каталог содержит содержимое HTML веб-сайта. `moodledata`Каталог содержит данные веб-сайта Moodle.

Введите эти команды, чтобы скопировать файлы из `moodle` `moodledata` каталогов и в каталог хранилища:

  ```bash
  cp -R /var/www/html/moodle /home/azureadmin/storage/
  cp -R /var/moodledata /home/azureadmin/storage/
  ```

### <a name="back-up-php-and-web-server-configurations"></a>Резервное копирование конфигураций PHP и веб-сервера

Чтобы создать резервную копию файлов конфигурации, выполните следующие действия.

1. Введите эти команды, чтобы создать новый каталог в каталоге хранилища:

   ```bash
   cd /home/azureadmin/storage
   mkdir configuration
   ```

2. Введите следующие команды, чтобы скопировать файлы конфигурации PHP и nginx:

   ```bash
   cp -R /etc/php /home/azureadmin/storage/configuration/
   cp -R /etc/nginx /home/azureadmin/storage/configuration/
   ```

   В `php` каталоге хранятся файлы конфигурации PHP, такие как `php-fpm.conf` , `php.ini` , `pool.d` и `conf.d` . В `nginx` каталоге хранятся конфигурации нгникс, такие как `nginx.conf` и `sites-enabled/dns.conf` .

### <a name="back-up-the-database"></a>Резервное копирование базы данных

Выполните следующие действия, чтобы создать резервную копию базы данных.

1. Введите следующие команды, чтобы проверить, установлен ли MySQL-Client:

   ```bash
   sudo -s
   mysql -V
   ```

2. Если MySQL-Client установлен, пропустите этот шаг. В противном случае введите следующую команду, чтобы установить MySQL-Client:

   ```bash
   sudo apt-get install mysql-client
   ```

3. Введите эту команду, чтобы создать резервную копию базы данных:

   ```bash
   mysqldump -h <database server name> -u <database user ID> -p<database password> <database name> > /home/azureadmin/storage/database.sql
   ```

   Для `<database server name>` , `<database user ID>` , `<database password>` и `<database name>` используйте значения, используемые локальной базой данных.

### <a name="create-an-archive"></a>Создание архива

Введите эту команду, чтобы создать файл архива `storage.tar.gz` для каталога резервного копирования:

```bash
cd /home/azureadmin/ tar -zcvf storage.tar.gz storage
```

## <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy

Введите следующие команды для установки AzCopy:

```bash
sudo -s
wget https://aka.ms/downloadazcopy-v10-linux
tar -xvf downloadazcopy-v10-linux
sudo rm /usr/bin/azcopy
sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
```

## <a name="copy-archived-files-to-azure-blob-storage"></a>Копирование архивных файлов в хранилище BLOB-объектов Azure

Выполните следующие действия, чтобы использовать AzCopy для копирования архивных локальных файлов в хранилище BLOB-объектов Azure.

### <a name="generate-a-security-token"></a>Создание маркера безопасности

Чтобы создать маркер подписанного URL-адрес (SAS) для AzCopy, выполните следующие действия.

1. В портал Azure перейдите на страницу созданной ранее учетной записи хранения.

1. На панели слева выберите **подпись общего доступа**.

   ![Снимок экрана страницы портал Azure учетной записи хранения с подписью общего доступа, выделенной на левой панели.](./images/new-storage-account-page.png)

1. В разделе **Разрешенные типы ресурсов** выберите **контейнер**.

1. В поле **Дата и время начала и окончания** введите время начала и окончания для маркера SAS.

1. Выберите действие **Создать SAS и строку подключения**.

   ![Снимок экрана портал Azure показывающей страницу подписанного URL-доступа для учетной записи хранения.](./images/shared-access-signature-page.png)

1. Создайте копию маркера SAS, который будет использоваться на последующих шагах.

### <a name="create-a-container"></a>Создание контейнера

Создайте контейнер в учетной записи хранения. Для этого шага можно либо использовать Azure CLI, либо портал Azure.

- Чтобы использовать Azure CLI, введите следующую команду:

  ```bash
  az storage container create --account-name <storage account name> --name <container name> --auth-mode login
  ```

  Пример команды:

  `az storage container create --account-name onpremisesstorage --name migration --auth-mode login`

  При использовании `--auth-mode` параметра со значением `login` Azure использует ваши учетные данные для проверки подлинности, а затем создает контейнер.

- Чтобы использовать портал Azure для создания контейнера, выполните следующие действия.

  1. На портале перейдите на страницу созданной ранее учетной записи хранения.

  1. Выберите **контейнер**, а затем щелкните **Добавить**.

  1. Введите имя для контейнера и нажмите кнопку **создать**.

     ![Снимок экрана диалогового окна в портал Azure для создания нового контейнера с полем имени и кнопкой "создать".](./images/new-container.png)

### <a name="copy-the-archive-file-to-azure-blob-storage"></a>Копирование файла архива в хранилище BLOB-объектов Azure

Введите эту команду, чтобы скопировать файл архива в контейнер, созданный в хранилище BLOB-объектов:

```bash
sudo azcopy copy /home/azureadmin/storage.tar.gz 'https://<storage account name>.blob.core.windows.net/<container name>/<SAS token>'
```

Пример команды:

`azcopy copy /home/azureadmin/storage.tar.gz 'https://onpremisesstorage.blob.core.windows.net/migration/?sv=2019-12-12&ss='`

Теперь ваша учетная запись хранилища BLOB-объектов должна содержать копию архива.

![Снимок экрана страницы в портал Azure, показывающей учетные записи хранения BLOB-объектов. Отображается сжатый ZIP-файл каталога хранилища.](./images/archive-in-blob-storage.png)

## <a name="next-steps"></a>Дальнейшие действия

Продолжайте [Moodle архитектуру и шаблоны миграции](./migration-arch.md).
