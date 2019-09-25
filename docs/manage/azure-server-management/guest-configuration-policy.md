---
title: Политика конфигурации гостя
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Политика конфигурации гостя
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c43d07c6cfdea0152559d7a13fec7dde148b1530
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221567"
---
# <a name="guest-configuration-policy"></a>Политика конфигурации гостя

Модуль [настройки гостевой конфигурации](/azure/governance/policy/concepts/guest-configuration) политики Azure позволяет выполнять аудит параметров конфигурации на виртуальной машине. В настоящее время Гостевая конфигурация поддерживается только на виртуальных машинах Azure.

Список политик конфигурации гостевой системы можно найти, выполнив поиск по категории "Гостевая конфигурация" на странице портала политики Azure. Список можно также найти, запустив этот командлет в окне PowerShell:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Функциональность гостевой настройки регулярно обновляется для поддержки дополнительных наборов политик. Периодически проверяйте наличие новых поддерживаемых политик и оцените их полезность.

<!-- TODO: Update these links when available. 

By default, we recommend enabling the following policies:

- [Preview]: Audit to verify password security settings are set correctly inside Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Развертывание

Для развертывания этих политик можно использовать следующий пример скрипта PowerShell:

- Убедитесь, что параметры безопасности пароля на компьютерах Windows и Linux установлены правильно.
- Убедитесь, что сертификаты не близки к истечению срока действия на виртуальных машинах Windows.

 Перед запуском этого скрипта необходимо выполнить вход с помощью командлета [Connect-азаккаунт](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . При запуске скрипта необходимо указать имя подписки, к которой необходимо применить политики.

```powershell

    #Assign Guest Configuration policy.
    param (
        [Parameter(Mandatory=$true)]
        [string]$SubscriptionName
    )

    $Subscription = Get-AzSubscription -SubscriptionName $SubscriptionName
    $scope = "/subscriptions/" + $Subscription.Id

    $PasswordPolicy = Get-AzPolicySetDefinition -Name "3fa7cbf5-c0a4-4a59-85a5-cca4d996d5a6"
    $CertExpirePolicy = Get-AzPolicySetDefinition -Name "b6f5e05c-0aaa-4337-8dd4-357c399d12ae"

    New-AzPolicyAssignment -Name "PasswordPolicy" -DisplayName "[Preview]: Audit that password security settings are set correctly inside Linux and Windows machines" -Scope $scope -PolicySetDefinition $PasswordPolicy -AssignIdentity -Location eastus

    New-AzPolicyAssignment -Name "CertExpirePolicy" -DisplayName "[Preview]: Audit that certificates are not expiring on Windows VMs" -Scope $scope -PolicySetDefinition $CertExpirePolicy -AssignIdentity -Location eastus

```

## <a name="next-steps"></a>Следующие шаги

Узнайте, как [включить отслеживание изменений и предупреждения](./enable-tracking-alerting.md) для критически важных изменений файлов, служб, программ и реестра.

> [!div class="nextstepaction"]
> [Включение отслеживания и предупреждений для критических изменений](./enable-tracking-alerting.md)
