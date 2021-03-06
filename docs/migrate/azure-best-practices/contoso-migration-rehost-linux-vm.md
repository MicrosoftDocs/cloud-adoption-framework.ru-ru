---
title: Повторное размещение локального приложения Linux на виртуальных машинах Azure
description: Узнайте, как Contoso перемещает локальное приложение Linux путем перехода на виртуальные машины Azure.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: think-tank
ms.openlocfilehash: b98b90a7eb08fd5452050c7047825fa0788b724b
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101791740"
---
<!-- cSpell:ignore OSTICKETWEB OSTICKETMYSQL OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc osTicket binlog systemctl NSGs distros -->

# <a name="rehost-an-on-premises-linux-application-to-azure-vms"></a>Повторное размещение локального приложения Linux на виртуальных машинах Azure

В этой статье показано, как вымышленная компания Contoso повторно размещает двухуровневый приложение [на основе лампы](https://wikipedia.org/wiki/LAMP_software_bundle) , используя виртуальные машины Azure "инфраструктура как услуга" (IaaS).

Приложение службы поддержки, используемое в этом примере, Остиккет, предоставляется как программное обеспечение с открытым исходным кодом. Если вы хотите использовать его для тестирования, вы можете скачать его с сайта [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Бизнес-факторы

Совместными усилиями ИТ-руководство и деловые партнеры определили указанные ниже цели этой миграции.

- **Устраните бизнес-рост.** По мере развития компании Contoso растет нагрузка на локальные системы и инфраструктуру.
- **Ограничение риска.** Приложение службы поддержки является критически важным для компании Contoso Business. Поэтому компания Contoso хочет переместить его в Azure с минимальными рисками.
- **Расширений.** Contoso не хочет изменять приложение прямо сейчас. Он хочет обеспечить стабильность приложения.

## <a name="migration-goals"></a>Цели миграции

Группа Contoso Cloud заблокировала цели этой миграции, чтобы определить наилучший способ переноса:

- После миграции приложение в Azure должно иметь те же возможности производительности, что и сегодня в локальной среде VMware компании. Приложение будет оставаться критически важным в облаке, как и локально.
- Компания Contoso не хочет вкладываться в это приложение. Это важно для бизнеса, но в его текущей форме Contoso просто хочет безопасно переместить его в облако.
- Contoso не хочет изменять модель Ops для этого приложения. Он хочет взаимодействовать с приложением в облаке так же, как и сейчас.
- Contoso не хочет изменять функциональные возможности приложения. Изменится только расположение приложения.
- Если вы выполнили несколько миграций приложений Windows, компания Contoso хочет узнать, как использовать инфраструктуру на основе Linux в Azure.

## <a name="solution-design"></a>Архитектура решения

После фиксации целей и требований компания Contoso проектирует и изучает решение для развертывания и определяет процесс миграции. Службы Azure, которые компания Contoso будет использовать для миграции, также будут идентифицированы.

### <a name="current-application"></a>Текущее приложение

- Приложение Остиккет распределяется между двумя виртуальными машинами ( `OSTICKETWEB` и `OSTICKETMYSQL` ).
- Виртуальные машины расположены на узле VMware ESXi `contosohost1.contoso.com` (версии 6.5).
- Управление средой VMware осуществляется vCenter Server 6,5 ( `vcenter.contoso.com` ) и выполняется на виртуальной машине.
- Contoso имеет локальный центр обработки данных ( `contoso-datacenter` ) с локальным контроллером домена ( `contosodc1` ).

### <a name="proposed-architecture"></a>Предлагаемая архитектура

- Так как приложение является рабочей рабочей нагрузкой, виртуальные машины в Azure будут находиться в Рабочей группе ресурсов `ContosoRG` .
- Виртуальные машины будут перенесены в основной регион (Восточная часть США 2) и помещены в производственную сеть ( `VNET-PROD-EUS2` ):
  - Виртуальная машина веб-уровня будет находиться в интерфейсной подсети (`PROD-FE-EUS2`).
  - Виртуальная машина базы данных будет находиться в подсети базы данных ( `PROD-DB-EUS2` ).
- После завершения миграции локальные виртуальные машины в центре обработки данных Contoso будут выведены из эксплуатации.

![Схема архитектуры сценария.](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Проверка решения

Компания Contoso оценивает предлагаемую конструкцию, помещая вместе со списком достоинств и недостатков.

| Оценка | Сведения |
| --- | --- |
| **Преимущества** | Виртуальные машины приложений будут перемещены в Azure без изменений, что делает миграцию простой. <br><br> Поскольку компания Contoso использует подход с приближением и сдвигом для обеих виртуальных машин приложений, для базы данных приложения специальные средства настройки или миграции не требуются. <br><br> Contoso будет хранить полный контроль над виртуальными машинами приложений в Azure. <br><br> Виртуальные машины приложений работают под управлением Ubuntu 16,04-TLS, поддерживаемого дистрибутива Linux. Дополнительные сведения о рекомендуемых [дистрибутивах Linux в Azure](/azure/virtual-machines/linux/endorsed-distros). |
| **Недостатки** | Веб-узел и уровень данных приложения остаются едиными точками отработки отказа. <br><br> Contoso потребуется продолжить поддержку приложения в качестве виртуальных машин Azure, а не переходить в управляемую службу, например службу приложений Azure и базу данных Azure для MySQL. <br><br> Компания Contoso осознает, что благодаря простоте миграции виртуальных машин с переносом и сдвигом в компании не используются все преимущества функций, предоставляемых [базой данных Azure для MySQL](/azure/mysql/overview). Эти функции включают встроенную высокую доступность, прогнозируемую производительность, простое масштабирование, автоматическую архивацию и встроенную безопасность. |

### <a name="migration-process"></a>Процесс миграции

Порядок миграции в Contoso будет следующим:

- В качестве первого шага компания Contoso готовит и настраивает компоненты Azure для службы "миграция Azure": миграция серверов и подготовка локальной инфраструктуры VMware.
- В компании уже есть [инфраструктура Azure](./contoso-migration-infrastructure.md) , поэтому необходимо только настроить репликацию виртуальных машин с помощью средства миграции Azure "миграция сервера".
- Когда все будет подготовлено, Contoso сможет начать репликацию виртуальных машин.
- После того как репликация будет включена и начнет работать, Contoso перенесет виртуальную машину путем отработки отказа в Azure.

![Схема процесса миграции.](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Службы Azure

| Служба | Описание | Стоимость |
| --- | --- | --- |
| [Azure Migrate: Server Migration](../index.md) (Миграция Azure: миграция сервера). | Служба управляет миграцией локальных приложений и рабочих нагрузок, а также экземпляров виртуальных машин Amazon Web Services (AWS) и Google Cloud Platform (обеспечить). | Во время репликации в Azure взимается плата за службу хранилища Azure. При миграции создаются виртуальные машины Azure и взимается плата. Дополнительные сведения о [расходах и ценах](https://azure.microsoft.com/pricing/details/azure-migrate/). |

## <a name="prerequisites"></a>Предварительные требования

Ниже приведены действия компании Contoso, необходимые для этого сценария.

Требования | Сведения |
| --- | --- |
| **Подписка Azure.** | Специалисты Contoso создали подписки ранее в этой серии статей. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись Azure](https://azure.microsoft.com/free/). <br><br> Если вы создаете бесплатную учетную запись, вы являетесь администратором своей подписки и можете выполнять любые действия. <br><br> Если вы используете существующую подписку и вы не являетесь администратором, обратитесь к администратору, чтобы назначить вам разрешения владельца или участника. <br><br> Если вам нужны более детализированные разрешения, см. статью [Управление доступом Site Recovery с помощью управления доступом на основе ролей Azure (Azure RBAC)](/azure/site-recovery/site-recovery-role-based-linked-access-control). |
| **Инфраструктура Azure** | Узнайте [, как Contoso настраивает инфраструктуру Azure](./contoso-migration-infrastructure.md). <br><br> Дополнительные сведения о конкретных [предварительных требованиях](./contoso-migration-devtest-to-iaas.md#prerequisites) для службы "миграция Azure": миграция сервера. |
| **Локальные серверы** | Локальная vCenter Server должна работать под управлением версии 5,5, 6,0 или 6,5. <br><br> Узел ESXi с версией 5,5, 6,0 или 6,5. <br><br> Одна или несколько виртуальных машин VMware, которые выполняются на узле ESXi. |
| **Локальные виртуальные машины** | [Ознакомьтесь с дистрибутивовами Linux](/azure/virtual-machines/linux/endorsed-distros) , которые были одобрены для работы в Azure. |

## <a name="scenario-steps"></a>Шаги выполнения сценария

Миграция в Contoso будет осуществляться следующим образом:

> [!div class="checklist"]
>
> - **Шаг 1. Подготовка Azure для миграции Azure: миграция сервера.** Добавьте средство переноса Azure для миграции сервера в проект "миграция Azure".
> - **Шаг 2. Подготовка локальной среды VMware для миграции в Azure: миграция сервера.** Подготовка учетных записей для обнаружения виртуальных машин и подготовка к подключению к виртуальным машинам Azure после миграции.
> - **Шаг 3. репликация виртуальных машин.** Настройте репликацию и приступите к репликации виртуальных машин в службу хранилища Azure.
> - **Шаг 4. Миграция виртуальных машин с помощью службы "миграция Azure": миграция сервера.** Выполните тестовую миграцию, чтобы убедиться, что все работает, а затем запустите миграцию, чтобы переместить виртуальные машины в Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Шаг 1. Подготовка Azure к работе с миграцией Azure: средство миграции сервера

Ниже перечислены компоненты Azure, которые необходимы для миграции виртуальных машин компании Contoso в Azure.

- Виртуальная сеть, в которой будут находиться виртуальные машины Azure при их создании во время миграции.
- Средство миграции Azure: подготовка к переходу на сервер.

Эти компоненты настраиваются следующим образом.

1. Настройте сеть. Компания Contoso уже настроила сеть, которую можно использовать для миграции Azure: Перенос сервера при [развертывании инфраструктуры Azure](./contoso-migration-infrastructure.md) в компании

    - Приложение SmartHotel360 — это рабочее приложение. Виртуальные машины будут перенесены в рабочую сеть Azure ( `VNET-PROD-EUS2` ) в основном регионе ( `East US 2` ).
    - Обе виртуальные машины будут помещены в `ContosoRG` группу ресурсов, которая будет использоваться для рабочих ресурсов.
    - Клиентская виртуальная машина приложения ( `OSTICKETWEB` ) будет перенесена в интерфейсную подсеть ( `PROD-FE-EUS2` ) в рабочей сети.
    - Виртуальная машина базы данных приложений ( `OSTICKETMYSQL` ) будет перенесена в подсеть базы данных ( `PROD-DB-EUS2` ) в рабочей сети.

1. Выполните подготовку к работе средства миграции Azure: Server Migration Tool. После размещения сети и учетной записи хранения Contoso теперь создает хранилище служб восстановления ( `ContosoMigrationVault` ) и помещает его в `ContosoFailoverRG` группу ресурсов в основном регионе ( `East US 2` ).

    ![Снимок экрана, показывающий средство миграции сервера Azure Migration Server](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**Требуется дополнительная помощь?**

Узнайте [, как настроить средство миграции для Azure Migration](/azure/migrate/).

## <a name="step-2-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Шаг 2. Подготовка локальной среды VMware для миграции Azure: миграция сервера

После миграции в Azure компания Contoso хочет иметь возможность подключиться к реплицированным виртуальным машинам в Azure. Есть несколько вещей, которые требуются администраторам Contoso:

- Чтобы получить доступ к виртуальным машинам Azure через Интернет, следует включить SSH на локальных виртуальных машинах Linux перед миграцией. Для Ubuntu этот шаг можно выполнить с помощью следующей команды: `sudo apt-get ssh install -y` .
- Установка [агента Linux для Azure](/azure/virtual-machines/extensions/agent-linux)
- После выполнения миграции они могут проверить **диагностику загрузки** , чтобы просмотреть снимок экрана виртуальной машины.
- Если она не работает, необходимо проверить, запущена ли виртуальная машина, и ознакомиться с [рекомендациями по устранению неполадок](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Требуется дополнительная помощь?**

Узнайте, как [подготовить виртуальные машины для миграции](/azure/migrate/prepare-for-migration).

## <a name="step-3-replicate-the-on-premises-vms"></a>Шаг 3. Репликация локальных виртуальных машин

Чтобы можно было запустить миграцию в Azure, администраторам компании Contoso потребуется настроить и включить репликацию.

После завершения обнаружения Начните репликацию виртуальных машин VMware в Azure.

1. В проекте службы "миграция Azure" перейдите в раздел **серверы**  >  **Миграция Azure: миграция сервера** и выберите **репликация**.

    ![Снимок экрана, на котором показан параметр репликации.](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. В разделе Параметры **репликации**  >  **источника**  >  **виртуальные машины виртуализированы?** выберите **Да, с VMware vSphere**.

3. В поле **локальное устройство** выберите имя настроенного устройства для миграции Azure и нажмите кнопку **ОК**.

    ![Снимок экрана, на котором показана вкладка "Параметры источника".](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. В разделе **Виртуальные машины** выберите виртуальные машины, которые необходимо реплицировать.
    - Если вы выполнили оценку для виртуальных машин, вы можете применить рекомендации по выбору размера виртуальной машины и типу диска ("Премиум" или "Стандарт") из результатов оценки. В разделе **Импорт параметров миграции из оценки миграции Azure** выберите параметр **Да** .
    - Если вы не выполняли оценку или вы не хотите использовать параметры оценки, выберите параметр **нет** .
    - Если выбрано использование оценки, выберите группу виртуальных машин и имя оценки.

    ![Снимок экрана, показывающий выбор оценок.](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. В окне **виртуальные машины** выполните поиск виртуальных машин по мере необходимости и выберите каждую виртуальную машину, которую требуется перенести. Затем нажмите кнопку **Далее: целевые параметры**.

6. В поле **целевые параметры** выберите подписку и целевой регион для переноса. Укажите группу ресурсов, в которой будут размещаться виртуальные машины Azure после миграции. В поле **Виртуальная сеть** выберите виртуальную сеть или подсеть Azure, к которой будут присоединены виртуальные машины Azure после миграции.

7. Для параметра **Преимущество гибридного использования Azure**

    - выберите вариант **Нет**, если вы не хотите применять Преимущество гибридного использования Azure. Выберите **Далее**.
    - Выберите **Да** , если у вас есть компьютеры Windows Server, на которых распространяется действующая программа Software Assurance или подписки Windows Server, и вы хотите применить преимущества к компьютерам, которые вы будете переносить. Выберите **Далее**.

8. В разделе **Вычисления** просмотрите имя виртуальной машины, размер, тип диска ОС и группу доступности. Виртуальные машины должны соответствовать [требованиям Azure](/azure/migrate/migrate-support-matrix-vmware#vmware-requirements).

    - **Размер виртуальной машины:** Если вы используете рекомендации по оценке, раскрывающийся список размер виртуальной машины будет содержать рекомендуемый размер. В противном случае служба "миграция Azure" выбирает размер на основе ближайшей соответствия в подписке Azure. В качестве альтернативы выберите размер вручную в разделе **Размер виртуальной машины Azure**.
    - **Диск ОС:** Укажите диск операционной системы (загрузочный) для виртуальной машины. Диск ОС — это диск с загрузчиком операционной системы и установщиком.
    - **Группа доступности:** Если после миграции виртуальная машина должна находиться в группе доступности Azure, укажите набор. Группа должна находиться в целевой группе ресурсов, которую вы указываете для миграции.

9. В поле **диски** укажите, следует ли реплицировать диски виртуальной машины в Azure. Выберите тип диска (стандартный SSD/HDD или управляемые диски уровня "Премиум") в Azure. Выберите **Далее**.
    - Диски можно исключить из репликации.
    - Если вы исключите диски, они не будут присутствовать на виртуальной машине Azure после миграции.

10. На странице **Проверка и запуск репликации** проверьте параметры. Затем выберите **репликация** , чтобы запустить начальную репликацию для серверов.

> [!NOTE]
> Вы можете обновить параметры репликации в любое время, прежде чем репликация начнется в **управлении**  >  **реплицируемыми компьютерами**. Настройки невозможно изменить после начала репликации.

## <a name="step-4-migrate-the-vms"></a>Шаг 4. Миграция виртуальных машин

Администраторы Contoso выполняют быструю миграцию, а затем миграцию для перемещения виртуальных машин.

### <a name="run-a-test-migration"></a>Выполнение тестовой миграции

1. В списке **цели миграции**  >  **серверы**  >  **Миграция Azure: миграция сервера** выберите **тестировать перенесенные серверы**.

     ![Снимок экрана, на котором показан параметр "тестировать перенесенные серверы".](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

1. Выберите и удерживайте (или щелкните правой кнопкой мыши) виртуальную машину для проверки. Затем выберите **Тестовая миграция**.

    ![Снимок экрана, на котором показан элемент "Тестовая миграция".](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

1. В разделе **Тестовая миграция** выберите виртуальную сеть Azure, в которой будет находиться виртуальная машина Azure после миграции. Рекомендуется использовать виртуальную сеть непроизводства.
1. Запустится задание **Тестовая миграция**. Отслеживайте задание и уведомления на портале.
1. После завершения миграции просмотрите перенастроенную виртуальную машину Azure в разделе **Виртуальные машины** на портале Azure. Имя машины содержит суффикс **-Test**.
1. После завершения теста выберите и удерживайте (или щелкните правой кнопкой мыши) виртуальную машину Azure на странице **репликация компьютеров**. Затем выберите **очистить тестовую миграцию**.

    ![Снимок экрана, на котором показан элемент "Очистка тестовой миграции".](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Миграция виртуальных машин

Теперь администраторы Contoso выполняют полную миграцию для завершения перемещения.

1. В проекте службы "миграция Azure" перейдите в раздел **серверы**  >  **Миграция Azure: миграция сервера** и выберите **репликация серверов**.

    ![Снимок экрана, на котором показан параметр "Репликация серверов".](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

1. В области **репликация компьютеров** выберите и удерживайте (или щелкните правой кнопкой мыши) виртуальную машину и выберите **Миграция**.
1. В разделе **Миграция** > **Shut down virtual machines and perform a planned migration with no data loss** (Завершить работу виртуальных машин и выполнить запланированную миграцию без потери данных?) выберите вариант **Да** > **ОК**.
    - По умолчанию служба "миграция Azure" завершает работу локальной виртуальной машины и выполняет репликацию по требованию для синхронизации любых изменений виртуальной машины, произошедших с момента последней репликации. Это действие гарантирует отсутствие потери данных.
    - Если вы не хотите выключать виртуальную машину, выберите вариант **Нет**.
1. Запустится задание миграции виртуальной машины. Отслеживайте задание в уведомлениях Azure.
1. После завершения работы вы можете просматривать виртуальную машину и управлять ею на странице **Виртуальные машины**.

### <a name="connect-the-vm-to-the-database"></a>Подключение виртуальной машины к базе данных

В качестве последнего шага процесса миграции администраторы Contoso обновляют строку подключения приложения, чтобы она указывала на базу данных приложения, работающую на `OSTICKETMYSQL` виртуальной машине.

1. Установите SSH-подключение к виртуальной машине с помощью выводимого `OSTICKETWEB` или другого клиента SSH. Виртуальная машина является частной, поэтому подключитесь с помощью частного IP-адреса.

    ![Снимок экрана, показывающий область подключения к виртуальной машине.](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Снимок экрана, на котором показано соединение с базой данных.](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

1. Убедитесь, что `OSTICKETWEB` Виртуальная машина может обмениваться данными с `OSTICKETMYSQL` виртуальной машиной. В настоящее время Конфигурация жестко закодирована локальным IP-адресом `172.16.0.43` .

    **Перед обновлением:**

    ![Снимок экрана, показывающий IP-адрес перед обновлением.](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **После обновления:**

    ![Снимок экрана, показывающий IP-адрес после обновления.](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

1. Перезапустите службу с помощью **systemctl Restart apache2**.

    ![Снимок экрана, на котором показан перезапуск службы.](./media/contoso-migration-rehost-linux-vm/restart.png)

1. Наконец, обновите записи DNS для `OSTICKETWEB` и `OSTICKETMYSQL` на одном из контроллеров домена contoso.

    ![Снимок экрана, на котором показано обновление записи DNS.](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Снимок экрана, на котором показано обновление записи DNS.](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Требуется дополнительная помощь?**

- Узнайте, как [выполнить тестовую миграцию](/azure/migrate/tutorial-migrate-vmware#run-a-test-migration).
- Узнайте, как [выполнить миграцию виртуальных машин в Azure](/azure/migrate/tutorial-migrate-vmware#migrate-vms).

## <a name="clean-up-after-migration"></a>Очистка после миграции

После завершения миграции уровни приложений Остиккет теперь работают на виртуальных машинах Azure.

Теперь компания Contoso должна выполнить следующие задачи:

- Удалите локальные виртуальные машины из перечня в vCenter.
- Удалить локальные виртуальные машины из локальных заданий резервного копирования.
- Обновите внутреннюю документацию, чтобы отобразить новое расположение и IP-адреса для `OSTICKETWEB` и `OSTICKETMYSQL` .
- Проверьте все ресурсы, которые взаимодействуют с виртуальными машинами. Обновить все соответствующие параметры или документы согласно новой конфигурации.
- Contoso использовал службу "миграция Azure" с виртуальной машиной управления для оценки виртуальных машин для миграции. Администраторы должны удалить виртуальную машину и виртуальные машины миграции с VMware ESXi Server.

## <a name="review-the-deployment"></a>Проверка развертывания

Теперь, когда приложение работает, компания Contoso должна полностью эксплуатацию и защитить свою новую инфраструктуру.

### <a name="security"></a>Безопасность

Группа безопасности Contoso проверяет `OSTICKETWEB` `OSTICKETMYSQL` виртуальные машины и на наличие проблем безопасности.

- Чтобы можно было управлять доступом, команда проверяет группы безопасности сети (NSG) для виртуальных машин. NSG позволяют пропускать только разрешенный для приложения трафик.
- Группа также рассматривает защиту данных на дисках виртуальной машины с помощью шифрования дисков Azure и Azure Key Vault.

Дополнительные сведения см. в статье рекомендации [по обеспечению безопасности для рабочих нагрузок IaaS в Azure](/azure/security/fundamentals/iaas).

### <a name="business-continuity-and-disaster-recovery"></a>Непрерывность бизнес-процессов и аварийное восстановление

Чтобы обеспечить непрерывность бизнес-процессов и аварийное восстановление, специалисты компании Contoso выполняют указанные ниже действия.

- **Обеспечьте безопасность данных.** Contoso создает резервные копии данных на виртуальных машинах с помощью [резервного копирования виртуальных машин Azure](/azure/backup/backup-azure-vms-introduction).

- **Обеспечьте работоспособность приложений.** Contoso реплицирует виртуальные машины приложений в Azure в дополнительный регион с помощью Site Recovery. Дополнительные сведения см. [в разделе Краткое руководство. Настройка аварийного восстановления в дополнительном регионе Azure для виртуальной машины Azure](/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Лицензирование и оптимизация затрат

- После развертывания ресурсов Contoso назначает теги Azure в соответствии с определениями, заданными в ходе [развертывания инфраструктуры Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- У компании Contoso нет проблем с лицензированием серверов Ubuntu.
- Contoso будет использовать службу [управления затратами Azure и выставления счетов](/azure/cost-management-billing/cost-management-billing-overview) , чтобы гарантировать, что компания останется в бюджете, установленном ИТ – лидером.
