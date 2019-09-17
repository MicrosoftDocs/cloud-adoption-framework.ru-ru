---
title: Рефакторинг развертывания Team Foundation Server и его перенос в Azure DevOps Services в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте, как Contoso выполняет рефакторинг локального развертывания TFS, перемещая его в Azure DevOps Services в Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: fc992a4c00a1acd99481d6090563ecef38c5fedb
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70832313"
---
# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Рефакторинг развертывания Team Foundation Server и его перенос в Azure DevOps Services

В этой статье показано, как вымышленная компания Contoso выполняет рефакторинг локального развертывания Team Foundation Server (TFS), переместив его в Azure DevOps Services в Azure. Команда разработчиков Contoso использовала TFS для совместной работы и контроля версий в течение последних пяти лет. Теперь они хотят перейти на облачное решение для разработки и тестирования, а также для управления версиями. Azure DevOps Services сыграет роль, когда они перейдут на модель Azure DevOps и разработают новые облачные приложения.

## <a name="business-drivers"></a>Бизнес-факторы

Команда ИТ-руководителей тесно сотрудничала с деловыми партнерами для определения будущих целей. Партнеры не слишком озабочены средствами и технологиями разработки, но они отметили следующие моменты:

- **Программное обеспечение.** Независимо от основного бизнеса, все компании теперь являются компаниями-разработчиками программного обеспечения, включая Contoso. Бизнес-руководство заинтересовано в том, как ИТ-специалисты могут помочь внедрить новые методы работы для пользователей и условия взаимодействия для своих клиентов.
- **Эффективность.** Contoso необходимо оптимизировать процесс и удалить ненужные процедуры для разработчиков и пользователей. Это позволит компании более эффективно выполнять требования клиентов. Компания нуждается в быстрой работе ИТ-отдела без потери времени или денег.
- **Гибкость.** ИТ-отдел Contoso должен отвечать потребностям бизнеса и реагировать быстрее, чем рынок, чтобы обеспечить успех в глобальной экономике. ИТ-отдел не должен быть препятствием для бизнеса.

## <a name="migration-goals"></a>Цели миграции

Группа, работающая над облачной инфраструктурой компании Contoso, определила цели этой миграции в Azure DevOps Services:

- Команде нужен инструмент для переноса данных в облако. Необходимо несколько процессов, выполняемых вручную.
- Данные рабочих элементов и история за последний год должны быть перенесены.
- Они не хотят создавать новые имена пользователей и пароли. Все текущие системные назначения должны быть сохранены.
- Они хотят отказаться от Team Foundation Version Control (TFVC) в пользу Git для управления версиями.
- Переключение на Git будет "переносом подсказок", при котором импортируется только последняя версия исходного кода. Это произойдет во время простоя, когда все операции будут остановлены по причине переноса базы кода. Они понимают, что после перемещения будет доступна только текущая история главной ветви.
- Они обеспокоены изменениями и хотят протестировать их, прежде чем выполнять полный переход. Они хотят сохранить доступ к TFS даже после перехода в Azure DevOps Services.
- Они имеют несколько коллекций и хотят начать с той, которая содержит всего несколько проектов, чтобы лучше понять процесс.
- Они понимают, что коллекции TFS поддерживают отношения "один к одному" с организациями Azure DevOps Services, поэтому у них будет несколько URL-адресов. Однако это соответствует их текущей модели разделения для баз кода и проектов.

## <a name="proposed-architecture"></a>Предлагаемая архитектура

- Contoso переместит свои проекты TFS в облако и больше не будет размещать свои проекты или систему управления версиями в локальной среде.
- TFS будут перенесены в Azure DevOps Services.
- Сейчас у компании Contoso есть одна коллекция TFS, `ContosoDev`, которая будет перенесена в организацию Azure DevOps Services, `contosodevmigration.visualstudio.com`.
- Проекты, рабочие элементы, ошибки и итерации с прошлого года будут перенесены в Azure DevOps Services.
- Contoso будет использовать свой экземпляр Azure Active Directory, который они настроили после [развертывания инфраструктуры Azure](contoso-migration-infrastructure.md) в начале планирования миграции.

![Архитектура сценария](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Процесс миграции

Порядок миграции в Contoso будет следующим:

1. Потребуется серьезная подготовка. В качестве первого шага компания Contoso должна обновить свою реализацию TFS до поддерживаемого уровня. В настоящее время компания Contoso использует TFS 2017 с обновлением 3, но для переноса базы данных им необходимо запустить поддерживаемую версию 2018 с последними обновлениями.
2. После обновления компания Contoso запустит средство миграции TFS и проведет проверку своей коллекции.
3. Contoso создаст набор файлов подготовки и выполнит пробный перенос для тестирования.
4. Затем специалисты Contoso выполнят другой перенос, на этот раз полный, включающий рабочие элементы, ошибки, спринты и код.
5. После миграции они переместят свой код из TFVC в Git.

![Процесс миграции](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Предварительные требования

Ниже показано, что необходимо сделать специалистам компании Contoso, чтобы реализовать этот сценарий.

<!-- markdownlint-disable MD033 -->

**Требования** | **Сведения**
--- | ---
**Подписка Azure.** | Специалисты Contoso создали подписки ранее в этой серии статей. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Если вы создаете бесплатную учетную запись, вы являетесь администратором своей подписки и можете выполнять любые действия.<br/><br/> Если вы используете существующую подписку, в которой не являетесь администратором, администратор должен назначить вам права владельца или участника.<br/><br/> Если вам требуются более детализированные разрешения, ознакомьтесь с [этой статьей](/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Инфраструктура Azure** | Contoso настраивает свою инфраструктуру Azure, как описано в статье [Развертывание инфраструктуры Azure для миграции в Contoso](contoso-migration-infrastructure.md).
**Локальный сервер TFS** | В локальной среде требуется установить Team Foundation Server 2018 с обновлением 2 или обновить до этой версии имеющийся сервер.

## <a name="scenario-steps"></a>Шаги выполнения сценария

Миграция в Contoso будет осуществляться следующим образом:

> [!div class="checklist"]
>
> - **Шаг 1. Создание учетной записи хранения Azure.** Эта учетная запись хранения будет использоваться во время процесса миграции.
> - **Шаг 2. Обновление TFS.** Специалисты Contoso обновят развертывание до TFS 2018 с обновлением 2.
> - **Шаг 3. Проверка коллекции.** Contoso проверит свою коллекцию TFS для подготовки к миграции.
> - **Шаг 4. Создание файла подготовки.** Специалисты Contoso создадут файлы миграции с помощью средства миграции TFS.

## <a name="step-1-create-a-storage-account"></a>Шаг 1. Создать учетную запись хранения

1. На портале Azure администраторы Contoso создадут учетную запись хранения (**contosodevmigration**).
2. Они размещают учетную запись в дополнительном регионе, который они используют для отработки отказа — "Центральная часть США". Они используют стандартную учетную запись общего назначения с локально избыточным хранилищем.

    ![Учетная запись хранения](./media/contoso-migration-tfs-vsts/storage1.png)

**Нужна дополнительная помощь?**

- [Общие сведения о службе хранилища Azure](/azure/storage/common/storage-introduction).
- [Создание учетной записи хранения](/azure/storage/common/storage-create-storage-account).

## <a name="step-2-upgrade-tfs"></a>Шаг 2. Обновление TFS

Администраторы Contoso обновляют сервер TFS до TFS 2018 с обновлением 2. Перед запуском:

- Они скачивают [TFS 2018 с обновлением 2](https://visualstudio.microsoft.com/downloads).
- Они проверяют [требования к оборудованию](/tfs/server/requirements), а также читают [заметки о выпуске](/visualstudio/releasenotes/tfs2018-relnotes) и [сложности при обновлении](/tfs/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).

Они выполняют обновление следующим образом:

1. Чтобы начать работу, они создают резервную копию своего сервера TFS (работает на виртуальной машине VMware) и делают моментальный снимок VMware.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png)

2. Установщик TFS запускается, и они выбирают место для установки. Установщику требуется доступ к Интернету.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png)

3. По завершении установки запустится мастер настройки сервера.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png)

4. После проверки мастер завершит обновление.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png)

5. Специалисты компании проверяют установку TFS, просматривая проекты, рабочие элементы и код.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Некоторым обновлениям TFS необходимо запустить мастер настройки компонентов после завершения обновления. [Узнайте больше](/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).

**Нужна дополнительная помощь?**

Ознакомьтесь с дополнительными сведениями об [обновлении TFS](/tfs/server/upgrade/get-started).

## <a name="step-3-validate-the-tfs-collection"></a>Шаг 3. Проверка коллекции TFS

Администраторы Contoso запускают средство миграции TFS в базе данных коллекции ContosoDev для ее проверки перед переносом.

1. Специалисты Contoso скачивают и распаковывают [средство миграции TFS](https://www.microsoft.com/download/details.aspx?id=54274). Важно скачать версию для обновления TFS, которое выполняется. Версию можно проверить в консоли администратора.

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. Они запускают средство для выполнения проверки, указав URL-адрес коллекции проектов:

        `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

3. В средстве отображается ошибка.

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

4. Они обнаружили, что файлы журналов находятся в папке `Logs` непосредственно перед папкой инструмента. Файл журнала создается для каждой основной проверки. `TfsMigration.log` содержит основную информацию.

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

5. Специалисты компании находят эту запись, связанную с удостоверением.

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

6. Они выполняют команду `TfsMigrator validate /help` в командной строке и видят, что для проверки удостоверений требуется команда `/tenantDomainName`.

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

7. Они снова выполняют команду проверки и включают это значение вместе с именем Azure AD: `TfsMigrator validate /collection: http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

8. Появляется окно входа в Azure AD, где они вводят учетные данные глобального администратора.

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

9. Проверка проходит и подтверждается средством.

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-create-the-migration-files"></a>Шаг 4. Создание файлов миграции

После завершения проверки администраторы Contoso могут использовать средство миграции TFS для создания файлов миграции.

1. Они выполняют этап подготовки в средстве.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Подготовка](./media/contoso-migration-tfs-vsts/prep1.png)

    Во время подготовки выполняется следующее:
    - Коллекция проверяется для поиска списка всех пользователей, и заполняется журнал схемы идентификации (**IdentityKapLog.csv**).
    - Подготавливается соединение с Azure Active Directory, чтобы найти соответствие для каждого идентификатора.
    - Специалисты Contoso уже развернули Azure AD и синхронизировали его с помощью Azure AD Connect, поэтому во время подготовки соответствующие идентификаторы будут найдены и помечены как активные.

2. Появляется окно входа в Azure AD, где они вводят учетные данные глобального администратора.

    ![Подготовка](./media/contoso-migration-tfs-vsts/prep2.png)

3. Подготовка завершается, и средство сообщает, что файлы импорта были успешно созданы.

    ![Подготовка](./media/contoso-migration-tfs-vsts/prep3.png)

4. Теперь они могут видеть, что файлы IdentityMapLog.csv и import.json были созданы в новой папке.

    ![Подготовка](./media/contoso-migration-tfs-vsts/prep4.png)

5. Файл import.json предоставляет параметры импорта. Он включает в себя информацию, такую ​​как имя требуемой организации и данные учетной записи хранения. Большинство полей заполнены автоматически. Некоторым полям потребовался ввод пользователя. Contoso открывает файл и добавляет созданное имя организации Azure DevOps Services: **contosodevmigration**. С этим именем URL-адрес Azure DevOps Services будет таким: **contosodevmigration.visualstudio.com**.

    ![Подготовка](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > Организацию нужно создать до миграции. После завершения миграции ее можно изменить.

6. Они просматривают файл журнала схемы идентификации, в котором отображаются учетные записи, которые будут перенесены в Azure DevOps Services во время импорта.

    - Активные идентификаторы станут пользователями в Azure DevOps Services после импорта.
    - В Azure DevOps Services эти идентификаторы будут лицензированы и отображаться в качестве пользователя в организации после миграции.
    - Эти идентификаторы отмечены как **Активные** в столбце **Expected Import Status** (Ожидаемое состояние импорта) в файле.

    ![Подготовка](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Шаг 5. Миграция в Azure DevOps Services

После подготовки администраторы Contoso могут сосредоточиться на миграции. После выполнения миграции они перейдут с использования TFVC на Git для контроля версий.

Прежде чем начать, администраторы планируют время простоя с командой разработчиков, чтобы перевести коллекцию в автономный режим для миграции. Ниже приведены шаги процесса миграции.

1. **Отключение коллекции.** Данные идентификаторов коллекции находятся в базе данных конфигурации сервера TFS, когда коллекция подключена и находится в оперативном режиме. Когда коллекция отключается от сервера TFS, она делает копию этих данных идентификации и упаковывает ее в коллекцию для переноса. Без этих данных операция импорта идентификаторов не может быть выполнена. Рекомендуется, чтобы коллекция была отключена до тех пор, пока импорт не будет завершен, так как невозможно импортировать изменения, произошедшие во время импорта.
2. **Создание резервной копии.** Следующим шагом процесса миграции является создание резервной копии, которую можно импортировать в Azure DevOps Services. Пакет приложения уровня данных (DACPAC) — это функция SQL Server, которая позволяет вносить изменения в базу данных в один файл для развертывания в других экземплярах SQL. Пакет также может быть восстановлен непосредственно в Azure DevOps Services, и поэтому используется как способ упаковки для переноса данных коллекции в облако. Contoso будет использовать средство SqlPackage.exe для создания DACPAC. Это средство включено в средства SQL Server Data Tools.
3. **Передача в хранилище.** При создании DACPAC они отправляют его в службу хранилища Azure. После его загрузки они получают подписанный URL-адрес (SAS), чтобы разрешить средству миграции TFS доступ к хранилищу.
4. **Заполнение полей импорта.** Contoso может заполнить недостающие поля в файле импорта, включая параметры DACPAC. Для начала нужно указать, что требуется **пробный** импорт, чтобы перед полной миграцией проверить, работает ли все должным образом.
5. **Пробное выполнение.** Помогает при пробном переносе коллекции. Пробное выполнение имеет ограниченный срок службы и удаляется до того, как начнется перенос. Их данные автоматически удаляются через заданный период времени. Напоминание о том, когда пробное выполнение будет удалено, включается в сообщение электронной почты, полученное после завершения импорта. Примите его к сведению и планируйте соответствующим образом.
6. **Завершение рабочей миграции.** По завершении пробной миграции администраторы Contoso выполняют заключительную миграцию, обновив файл **import.json** и снова запустив импорт.

### <a name="detach-the-collection"></a>Отключение коллекции

До запуска администраторы Contoso берут локальную резервную копию SQL Server и моментальный снимок VMware сервера TFS, прежде чем отключить коллекцию.

1. В консоли администратора TFS они выбирают коллекцию, которую хотят отключить (**ContosoDev**).

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate1.png)

2. На вкладке **Общие** они выбирают **Отсоединить коллекцию**.

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate2.png)

3. В мастере "Отсоединение коллекции командных проектов" в поле **Сообщение обслуживания** они вводят сообщение для пользователей, которые могут попытаться подключиться к проектам в коллекции.

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate3.png)

4. В окне **Ход выполнения отсоединения** они отслеживают ход выполнения и нажимают кнопку **Далее**, когда процесс завершается.

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate4.png)

5. По завершении проверки они нажимают кнопку **Отсоединить** в окне **Проверки готовности**.

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate5.png)

6. Они нажимают кнопку **Закрыть**, чтобы завершить процесс.

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate6.png)

7. В консоли администратора TFS больше не используется ссылка на коллекцию.

    ![Перенос](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Создание пакета DACPAC

Contoso создает резервную копию (DACPAC) для импорта в Azure DevOps Services.

- SqlPackage.exe в SQL Server Data Tools используется для создания DACPAC. Существует несколько версий SqlPackage.exe, установленных со средствами SQL Server Data Tools, расположенными в папках с такими именами, как 120, 130 и 140. Для подготовки DACPAC важно использовать правильную версию.
- При импорте TFS 2018 должен использоваться SqlPackage.exe из папки с номером 140 или выше. Для CONTOSOTFS этот файл находится в папке: **C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140**.

Администраторы Contoso создают DACPAC следующим образом:

1. Они открывают командную строку и переходят в расположение SQLPackage.exe. Они вводят следующую команду для создания DACPAC:

    ``` console
    SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory
    ```

    ![Архивация](./media/contoso-migration-tfs-vsts/backup1.png)

2. После запуска команды появляется следующее сообщение.

    ![Архивация](./media/contoso-migration-tfs-vsts/backup2.png)

3. Они проверяют свойства файла DACPAC.

    ![Архивация](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a>Обновление файла в хранилище

После создания DACPAC специалисты Contoso загружают его в хранилище Azure.

1. Они скачивают и устанавливают [Обозреватель службы хранилища Azure](https://azure.microsoft.com/features/storage-explorer).

    ![Отправьте](./media/contoso-migration-tfs-vsts/backup5.png)

2. Они подключаются к своей подписке и определяют учетную запись хранения, которую создали для миграции (**contosodevmigration**). Они создают контейнер больших двоичных объектов **azuredevopsmigration**.

    ![Отправьте](./media/contoso-migration-tfs-vsts/backup6.png)

3. Они указывают файл DACPAC для передачи в виде блочного BLOB-объекта.

    ![Отправьте](./media/contoso-migration-tfs-vsts/backup7.png)

4. После передачи файла они щелкают имя файла и выбирают **Создать SAS**. Они расширяют контейнеры больших двоичных объектов в рамках учетной записи хранения, выбирают контейнер с файлами импорта и щелкают **Получить подписанный URL-адрес**.

    ![Отправьте](./media/contoso-migration-tfs-vsts/backup8.png)

5. Они принимают значения по умолчанию и нажимают кнопку **Создать**. Таким образом они получают доступ на 24 часа.

    ![Отправьте](./media/contoso-migration-tfs-vsts/backup9.png)

6. Они копируют URL-адрес SAS, чтобы его можно было использовать в средстве миграции TFS.

    ![Отправьте](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> Миграция должна произойти раньше в пределах разрешенного временного окна, или срок действия разрешений истечет.
> Не создавайте ключ SAS на портале Azure. Создаваемые таким образом ключи основаны на учетной записи и не будут работать с импортом.

### <a name="fill-in-the-import-settings"></a>Заполнение параметров импорта

Ранее администраторы Contoso частично заполняли файл спецификации импорта (import.json). Теперь нужно добавить остальные параметры.

Откройте файл import.json и заполните следующие поля.

- **Расположение:** расположение ключа SAS, созданного выше.
- **Dacpac:** укажите имя файла DACPAC, который вы передали в учетную запись хранения. Включите расширение ".dacpac".
- **ImportType:** в этом случае установите значение DryRun.

![Импорт параметров](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="do-a-dry-run-migration"></a>Выполнение пробной миграции

Администраторы Contoso выполняют тестовую миграцию, позволяющую убедиться в правильной работе всех компонентов.

1. Они открывают командную строку и переходят в расположение TfsMigration (`C:\TFSMigrator`).
2. В качестве первого шага они проверяют файл импорта. Они хотят убедиться, что файл имеет правильный формат и что ключ SAS работает.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

3. Проверка возвращает ошибку, так как для ключа SAS требуется более длительный срок действия.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test1.png)

4. Они используют Обозреватель службы хранилища Azure для создания нового ключа SAS с 7-дневным сроком действия.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test2.png)

5. Они обновляют файл `import.json` и снова запускают проверку. На этот раз она завершается успешно.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test3.png)

6. Они инициируют пробный запуск:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

7. Чтобы подтвердить миграцию выдается соответствующее сообщение. Обратите внимание на время, в течение которого промежуточные данные будут сохраняться после пробного запуска.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test4.png)

8. Появится окно входа в Azure AD, где следует ввести учетные данные администратора Contoso.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test5.png)

9. В сообщении отображается информация об импорте.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test6.png)

10. Через 15 минут они переходят по URL-адресу и видят следующую информацию:

     ![Пробный запуск](./media/contoso-migration-tfs-vsts/test7.png)

11. После завершения миграции команда разработчиков Contoso входит в Azure DevOps Services, чтобы проверить, работает ли пробный запуск. После проверки подлинности Azure DevOps Services необходимы некоторые сведения для подтверждения организации.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test8.png)

12. В Azure DevOps Services руководитель группы разработчиков может увидеть, что проекты перенесены в Azure DevOps Services. Появится уведомление о том, что организация будет удалена через 15 дней.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test9.png)

13. Руководитель разработчиков открывает один из проектов и щелкает **Рабочие элементы** > **Назначено мне**. Будет показано, что данные рабочих элементов были перенесены вместе с идентификатором.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test10.png)

14. Руководитель разработки также проверяет другие проекты и код, чтобы подтвердить, что исходный код и журнал были перенесены.

    ![Пробный запуск](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Выполнение миграции рабочей среды

После завершения пробного запуска администраторы Contoso переходят к миграции рабочей среды. Они удаляют данные пробного выполнения, обновляют параметры импорта и снова запускают импорт.

1. На портале Azure DevOps Services они удаляют организацию пробного запуска.
2. Они обновляют файл import.json, чтобы установить для параметра **ImportType** значение **ProductionRun**.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full1.png)

3. Они начинают миграцию так же, как и пробное выполнение: `TfsMigrator import /importFile:C:\TFSMigrator\import.json`
4. Появится сообщение с подтверждением миграции и предупреждением, что данные могут храниться в безопасном расположении в качестве промежуточной области на срок до семи дней.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full2.png)

5. На странице входа в Azure AD они указывают учетные данные администратора Contoso.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full3.png)

6. В сообщении отображается информация об импорте.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full4.png)

7. Через 15 минут они переходят по URL-адресу и видят следующую информацию:

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full5.png)

8. После завершения миграции руководитель группы разработчиков Contoso входит в Azure DevOps Services, чтобы проверить, работает ли миграция. После входа в систему он может увидеть, что проекты были перенесены.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full6.png)

9. Руководитель разработчиков открывает один из проектов и щелкает **Рабочие элементы** > **Назначено мне**. Будет показано, что данные рабочих элементов были перенесены вместе с идентификатором.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full7.png)

10. Руководитель разработки проверяет данные других рабочих элементов для подтверждения.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full8.png)

11. Руководитель разработки также проверяет другие проекты и код, чтобы подтвердить, что исходный код и журнал были перенесены.

    ![Рабочая среда](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Перемещение системы управления версиями из TFVC в Git

После завершения миграции Contoso хочет перейти с использования TFVC на Git для управления исходным кодом. Специалистам компании необходимо импортировать исходный код в организации Azure DevOps Services в качестве репозиториев Git в той же организации.

1. На портале Azure DevOps Services они открывают один из репозиториев TFVC ( **$/PolicyConnect**) и просматривают его.

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. В раскрывающемся списке **Источник** они щелкают **Импорт**.

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. На вкладке **Тип источника** они выбирают **TFVC** и указывают путь к репозиторию. Они решают не переносить историю.

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > Из-за различий в хранении информации о контроле версий в TFVC и Git компании Contoso рекомендуется не переносить историю. Это тот подход, который корпорация Майкрософт предприняла при переносе Windows и других продуктов из системы централизованного управления версиями в Git.

4. После импорта администраторы проверяют код.

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. Они повторяют процесс для второго репозитория ( **$/SmartHotelContainer**).

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. После изучения источника руководители группы разработки соглашаются с тем, что миграция в Azure DevOps Services завершена. Теперь Azure DevOps Services становится источником для всех операций разработки в командах, участвующих в миграции.

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)

**Нужна дополнительная помощь?**

[Дополнительные сведения](/azure/devops/repos/git/import-from-TFVC?view=vsts) об импорте из TFVC.

## <a name="clean-up-after-migration"></a>Очистка после миграции

После завершения миграции Contoso необходимо выполнить следующие действия:

- Ознакомиться со сведениями о дополнительных операциях [после импорта](/azure/devops/articles/migration-post-import?view=vsts).
- Удалите репозитории TFVC или сделайте их доступными в режиме только для чтения. Базы кода не должны использоваться, но на них можно ссылаться для просмотра истории.

## <a name="post-migration-training"></a>Обучение после переноса данных

Компании Contoso понадобиться провести обучение работе с Azure DevOps Services и Git для соответствующих участников команды.