---
title: Создание расписаний обновления
description: Используйте платформу внедрения облаков для Azure, чтобы узнать, как управлять расписаниями обновлений с помощью портал Azure или новых модулей командлетов PowerShell.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: internal
ms.openlocfilehash: c4d177b427724cd9c3eb7573e8a0efe62435a454
ms.sourcegitcommit: 9d76f709e39ff5180404eacd2bd98eb502e006e0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/17/2021
ms.locfileid: "100631871"
---
# <a name="create-update-schedules"></a>Создание расписаний обновления

Вы можете управлять расписаниями обновления с помощью портал Azure или новых модулей командлетов PowerShell.

Сведения о создании расписания обновления с помощью портал Azure см. в разделе [Планирование развертывания обновлений](/azure/automation/update-management/deploy-updates#schedule-an-update-deployment).

`Az.Automation`Теперь модуль поддерживает настройку Управление обновлениями с помощью Azure PowerShell. Командлет [New-азаутоматионупдатеманажементазурекуери](/powershell/module/az.automation/new-azautomationupdatemanagementazurequery) позволяет использовать теги, расположение и сохраненные поисковые запросы для настройки расписаний обновлений для гибкой группы компьютеров.

## <a name="example-script"></a>Пример сценария

В примере сценария в этом разделе показано использование тегов и запросов для создания динамических групп компьютеров, к которым можно применить расписания обновления. Он выполняет следующие действия. При создании собственных скриптов можно обращаться к реализациям конкретных действий.

- Создает расписание обновления службы автоматизации Azure, которое выполняется каждую субботу в 8:00 AM.
- Создает запрос для всех компьютеров, соответствующих следующим условиям:
  - Развернут в `westus` , `eastus` или в `eastus2` расположении Azure.
  - Имеет `Owner` тег, которому присвоено значение `JaneSmith` .
  - Имеет `Production` тег, которому присвоено значение `true` .
- Применяет расписание обновления к запрашиваемым компьютерам и устанавливает интервал в два часа обновления.

Перед запуском примера скрипта необходимо выполнить вход с помощью командлета [Connect-азаккаунт](/powershell/module/az.accounts/connect-azaccount) . При запуске скрипта укажите следующие сведения.

- Идентификатор целевой подписки
- Целевая группа ресурсов
- Имя рабочей области Log Analytics
- Имя учетной записи службы автоматизации Azure

```powershell

    <#
        .SYNOPSIS
            This script orchestrates the deployment of the solutions and the agents.
        .Parameter SubscriptionName
        .Parameter WorkspaceName
        .Parameter AutomationAccountName
        .Parameter ResourceGroupName

    #>

    param (
        [Parameter(Mandatory=$true)]
        [string] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [string] $ResourceGroupName,

        [Parameter(Mandatory=$true)]
        [string] $WorkspaceName,

        [Parameter(Mandatory=$true)]
        [string] $AutomationAccountName,

        [Parameter(Mandatory=$false)]
        [string] $scheduleName = "SaturdayCriticalSecurity"
    )

    Import-Module Az.Automation

    $startTime = ([DateTime]::Now).AddMinutes(10)
    $schedule = New-AzAutomationSchedule -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -StartTime $startTime `
        -Name $scheduleName `
        -Description "Saturday patches" `
        -DaysOfWeek Saturday `
        -WeekInterval 1 `
        -ForUpdateConfiguration

    # Using AzAutomationUpdateManagementAzureQuery to create dynamic groups.

    $queryScope = @("/subscriptions/$SubscriptionID/resourceGroups/")

    $query1Location =@("westus", "eastus", "eastus2")
    $query1FilterOperator = "Any"
    $ownerTag = @{ "Owner"= @("JaneSmith") }
    $ownerTag.Add("Production", "true")

    $DGQuery = New-AzAutomationUpdateManagementAzureQuery -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Scope $queryScope `
        -Tag $ownerTag

    $AzureQueries = @($DGQuery)

    $UpdateConfig = New-AzAutomationSoftwareUpdateConfiguration -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Schedule $schedule `
        -Windows `
        -Duration (New-TimeSpan -Hours 2) `
        -AzureQuery $AzureQueries `
        -IncludedUpdateClassification Security,Critical
```

## <a name="next-steps"></a>Дальнейшие действия

См. Примеры реализации [общих политик в Azure](./common-policies.md) , которые могут помочь в управлении серверами.

> [!div class="nextstepaction"]
> [Пользовательские политики в Azure](./common-policies.md)
