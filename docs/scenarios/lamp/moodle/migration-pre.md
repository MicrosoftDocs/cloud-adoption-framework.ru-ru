---
title: Подготовка к Moodle миграции
description: Узнайте, как подготовиться к Moodle миграции.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 71990470e04f68f78b0bfffc2b1d837c7f0f29ad
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714786"
---
# <a name="how-to-prepare-for-a-moodle-migration"></a>Подготовка к Moodle миграции

## <a name="pre-migration-tasks"></a>Задачи, выполняемые перед миграцией

Экспорт данных из локальной среды в Azure включает следующие задачи.

- Установите Azure CLI.
- Создание подписки.
- Создайте группу ресурсов.
- Создайте учетную запись хранения.
- Резервное копирование локальных данных.
- Скачайте и установите AzCopy.
- Скопируйте архивные файлы в большой двоичный объект Azure.

## <a name="install-the-azure-cli"></a>Установка Azure CLI

- Установите Azure CLI на узле в локальной инфраструктуре для всех задач, связанных с Azure.

  ```bash
   curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
  ```

- Войдите в свою учетную запись Azure.

  ```bash
  az login
  ```

- Команда AZ login: Azure CLI, скорее всего, запустит экземпляр или вкладку в веб-браузере по умолчанию и предложит войти в Azure с помощью учетная запись Майкрософт. Если запуск обозревателя не происходит, откройте новую страницу в [https://aka.ms/devicelogin](https://aka.ms/devicelogin) и введите код авторизации, отображаемый в терминале.

- Чтобы использовать командную строку, введите следующую команду:

  ```bash
  az login -u <username> -p <password>
  ```

## <a name="create-a-subscription"></a>Создание подписки

Пропустите этот шаг, если у вас есть подписка. Если у вас нет подписки, вы можете [создать ее в портал Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) или выбрать подписку с [оплатой по мере](https://azure.microsoft.com/offers/ms-azr-0003p/) использования.

- Чтобы создать подписку с портал Azure, перейдите к разделу **подписки** в разделе " **Домашняя страница** ".

  ![Подписки Azure.](./images/subscriptions.png)

- Эта команда задает подписку:

  ```bash
  az account set --subscription "Subscription Name"

  Example: az account set --subscription "ComputePM LibrarySub"
  ```

## <a name="create-a-resource-group"></a>Создание группы ресурсов

После настройки подписки необходимо создать группу ресурсов. Один из вариантов — использовать портал Azure, чтобы создать его. Перейдите к разделу **Домашняя страница** , найдите **группу ресурсов**, выберите ее, заполните обязательные поля и выберите **создать**.

![Группы ресурсов. Создайте группу ресурсов.](./images/resource-group.png)

Кроме того, можно использовать Azure CLI для создания группы ресурсов.

- Укажите то же расположение по умолчанию из предыдущих шагов.

  ```bash
  az group create -l location -n name -s Subscription_NAME_OR_ID
  ```

- Обновите снимок экрана и имя подписки с помощью образца тестовой учетной записи.

  Пример: `az group create -l eastus -n manual_migration -s ComputePM LibrarySub`

- На предыдущем шаге группа ресурсов создается как "manual_migration". Используйте одну и ту же группу ресурсов в дальнейших шагах.

Дополнительные сведения см. в обзоре [расположения в Azure](https://azure.microsoft.com/global-infrastructure/data-residency/) .

## <a name="create-a-storage-account"></a>Создание учетной записи хранения

Следующим шагом является [Создание учетной записи хранения](https://ms.portal.azure.com/#create/Microsoft.StorageAccount) в созданной группе ресурсов. Учетные записи хранения можно создавать с помощью портал Azure или Azure CLI.

- Чтобы создать портал, перейдите к нему, найдите учетную запись хранения и нажмите кнопку **Добавить** . После заполнения обязательных полей выберите **создать**.

  ![Создание учетной записи хранения.](./images/create-storage-account.png)

- Кроме того, можно использовать Azure CLI:

  ```bash
  az storage account create -n storageAccountName -g resourceGroupName --sku Standard_LRS --kind BlobStorage -l location
  ```

  Пример: `az storage account create -n onpremisesstorage -g manual_migration --sku Standard_LRS --kind BlobStorage -l eastus`

- В предыдущей команде `--kind` указывает тип учетной записи хранения. После `onpremisesstorage` создания учетной записи она становится назначением для локальной резервной копии.

## <a name="back-up-on-premises-data"></a>Резервное копирование локальных данных

- Перед резервным копированием локальных данных Включите **режим обслуживания** для сайта Moodle. Выполните следующую команду из локальной виртуальной машины:

  ```bash
  sudo /usr/bin/php admin/cli/maintenance.php --enable
  ```

- Выполните следующую команду, чтобы проверить состояние сайта Moodle:

  ```bash
  sudo /usr/bin/php admin/cli/maintenance.php
  ```

- При резервном копировании локальных файлов, конфигураций и баз данных Moodle и мудледата можно создать резервную копию в одном каталоге. Следующая схема обобщает следующее:

  ![Структура каталога резервного копирования Moodle.](./images/directory-structure.png)

- Чтобы скопировать все данные, создайте пустой каталог хранилища в любом нужном месте:

  ```bash
  sudo -s
  ```

  Например, расположением является `/home/azureadmin` .

  ```bash
  cd /home/azureadmin
  mkdir storage
  ```

### <a name="back-up-moodle-and-moodledata"></a>Резервное копирование Moodle и мудледата

- Каталог Moodle состоит из содержимого HTML сайта. Мудледата содержит данные сайта Moodle.

- Команды для копирования Moodle и мудледата:

  ```bash
  cp -R /var/www/html/moodle /home/azureadmin/storage/
  cp -R /var/moodledata /home/azureadmin/storage/
  ```

### <a name="backup-php-and-web-server-configurations"></a>Резервное копирование PHP и конфигурации веб-сервера

- Скопируйте файлы конфигурации PHP, например,, `php-fpm.conf` `php.ini` и, `pool.d` `conf.d` в `phpconfig` каталог `configuration` в каталоге.

- Скопируйте конфигурации нгникс, например `nginx.conf` и, `sites-enabled/dns.conf` в `nginxconfig` каталог в `configuration` каталоге.

  ```bash
  cd /home/azureadmin/storage mkdir configuration
  ```

- Ниже приведены команды для копирования конфигураций nginx и PHP.

  ```bash
  cp -R /etc/nginx /home/azureadmin/storage/configuration/nginx
  cp -R /etc/php /home/azureadmin/storage/configuration/php
  ```

### <a name="create-a-backup-of-the-database"></a>Создание резервной копии базы данных

- Если у вас уже установлен MySQL-Client, пропустите этот шаг, чтобы установить его. Если у вас нет MySQL-Client, установите его сейчас:

  ```bash
  sudo -s
  ```

- Выполните следующую команду, чтобы проверить, установлен ли MySQL-Client:

  ```bash
  mysql -V
  ```

- Если MySQL-Client не установлен, выполните следующую команду:

  ```bash
  sudo apt-get install mysql-client
  ```

- Эта команда позволит вам создать резервную копию базы данных:

  ```bash
  mysqldump -h dbServerName -u dbUserId -pdbPassword dbName > /home/azureadmin/storage/database.sql
  ```

- Замените Дбсервернаме, Дбусерид, Дбпассворд и dbName на сведения о локальной базе данных.

- Создайте архивный `storage.tar.gz` файл каталога резервных копий:

  ```bash
  cd /home/azureadmin/ tar -zcvf storage.tar.gz storage
  ```

## <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy

Выполните следующие команды для установки AzCopy:

  ```bash
  sudo -s
  wget https://aka.ms/downloadazcopy-v10-linux
  tar -xvf downloadazcopy-v10-linux
  sudo rm /usr/bin/azcopy
  sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
  ```

## <a name="copy-archived-files-to-azure-blob"></a>Копирование архивных файлов в большой двоичный объект Azure

Используйте AzCopy для копирования архивных локальных файлов в большой двоичный объект Azure.

- Чтобы использовать AzCopy, сначала создайте маркер SAS. Перейдите к созданному **ресурсу учетной записи хранения** и перейдите к **подписанному общему доступу** на панели слева.

  ![Пример учетной записи хранения.](./images/storage-account-created.png)

- Выберите **контейнер** и флажки и задайте дату начала и окончания срока действия маркера SAS. Выберите действие **Создать SAS и строку подключения**.

  ![Создание маркера SAS.](images/SAS-token-generation.png)

- Скопируйте и сохраните маркер SAS для будущего использования.

- Команда для создания контейнера в учетной записи хранения:

  ```bash
  az storage container create --account-name <storageAccountName> --name <containerName> --auth-mode login
  ```

  Пример: `az storage container create --account-name onpremisesstorage --name migration --auth-mode login`

  `--auth-mode login` означает режим проверки подлинности при входе. После входа в систему контейнер будет создан.

- Контейнер также можно создать с помощью портал Azure. Перейдите к той же созданной учетной записи хранения, выберите контейнер, а затем нажмите кнопку **Добавить** .

- После ввода имени обязательного контейнера нажмите кнопку **создать** .

  ![Новый контейнер.](images/new-container.png)

- Команда для копирования файла архива в учетную запись BLOB-объекта Azure:

  ```bash
  sudo azcopy copy /home/azureadmin/storage.tar.gz 'https://<storageAccountName>.blob.core.windows.net/<containerName>/<SAStoken>'
  ```

  Пример: `azcopy copy /home/azureadmin/storage.tar.gz 'https://onpremisesstorage.blob.core.windows.net/migration/?sv=2019-12-12&ss='`

  ![Архив в большом двоичном объекте Azure.](images/archive-in-blob.png)

- Теперь в учетной записи BLOB-объектов Azure должна быть копия архива.

## <a name="next-steps"></a>Следующие шаги

Продолжайте [Moodle задачи миграции, архитектуру и шаблон](./migration-arch.md) для получения дополнительных сведений о процессе миграции Moodle.
