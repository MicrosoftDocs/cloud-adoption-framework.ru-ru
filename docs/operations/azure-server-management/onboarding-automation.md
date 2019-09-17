---
title: Автоматизация настройки адаптации и оповещений
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Автоматизация настройки адаптации и оповещений
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 86997d8c433c23d6ecbe5d3ac124623d318099c0
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833093"
---
# <a name="automate-onboarding"></a>Автоматизация адаптации

Чтобы повысить эффективность развертывания служб управления сервером Azure, рассмотрите возможность автоматизации развертывания служб управления с помощью рекомендаций, описанных в предыдущих разделах этого руководства. Скрипт и примеры шаблонов, приведенные в следующих разделах, являются начальными точками для разработки собственной автоматизации процессов адаптации.

## <a name="onboarding-by-using-automation"></a>Адаптация с помощью службы автоматизации

В этом руководстве содержится поддерживаемый репозиторий GitHub с примером кода [клаудадоптионфрамеворк](https://aka.ms/CAF/manage/automation-samples), который содержит примеры сценариев и шаблоны Azure Resource Manager, помогающие автоматизировать развертывание служб управления сервером Azure.

В этих примерах файлов показано, как использовать командлеты Azure PowerShell для автоматизации следующих задач:

1. Создайте [рабочую область log Analytics](/azure/azure-monitor/platform/manage-access) (или используйте существующую рабочую область, если она соответствует требованиям&mdash;, см. раздел [планирование рабочей области](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

2. Создайте учетную запись службы автоматизации (или используйте существующую учетную запись, если&mdash;она соответствует требованиям в разделе [планирование рабочей области](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

3. Свяжите учетную запись службы автоматизации и рабочую область Log Analytics (не требуется при подключении через портал).

4. Включите Управление обновлениями и Отслеживание изменений и инвентаризацию для рабочей области.

5. Подключение виртуальных машин Azure с помощью политики Azure (политика устанавливает агент Log Analytics и Dependency Agent на виртуальных машинах Azure).

6. Подключите локальные серверы, установив на них агент Log Analytics.

В этом примере используются файлы, описанные в следующей таблице, и их можно настроить для поддержки собственных сценариев развертывания.

| Имя файла | Описание |
|-----------|-------------|
| Нев-амсдеплоймент. ps1 | Главный, координирующий сценарий, автоматизирующий подключение. Для этого скрипта PowerShell требуется существующая подписка, но при этом будут созданы группы ресурсов, расположение, Рабочая область и учетные записи автоматизации, если они не существуют. |
| Workspace-Аутоматионаккаунт. JSON | Шаблон диспетчер ресурсов, который развертывает ресурсы рабочей области и учетной записи службы автоматизации. |
| Воркспацесолутионс. JSON | Шаблон диспетчер ресурсов, который позволяет создавать необходимые решения в рабочей области Log Analytics. |
| Скопеконфиг. JSON | Шаблон диспетчер ресурсов, использующий модель согласия для локальных серверов с решением для отслеживания изменений. Использовать модель согласия необязательно. |
| Енабле-вминсигхтсперфкаунтерс. ps1 | Сценарий PowerShell, который включает Вминсигхт для серверов и настраивает счетчики производительности. |
| Отслеживания изменений-filelist. JSON | Шаблон диспетчер ресурсов, определяющий список файлов, которые будут отслеживаться Отслеживание изменений. |

Вы можете запустить Нев-амсдеплоймент. ps1 с помощью следующей команды:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Следующие шаги

Узнайте, как настроить базовые оповещения для уведомления команды о событиях и проблемах управления ключами.

> [!div class="nextstepaction"]
> [Настройка основных оповещений](./setup-alerts.md)