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
ms.openlocfilehash: 741a73bacadccc0ee7b06542b86b9958aa236982
ms.sourcegitcommit: 3669614902627f0ca61ee64d97621b2cfa585199
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2019
ms.locfileid: "73656313"
---
# <a name="guest-configuration-policy"></a>Политика конфигурации гостя

Для аудита параметров конфигурации на виртуальной машине можно использовать расширение [гостевой настройки](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) политики Azure. В настоящее время Гостевая конфигурация поддерживается только на виртуальных машинах Azure.

Чтобы найти список политик конфигурации гостей, выполните поиск по запросу "Конфигурация гостевой службы" на странице портала политики Azure. Или выполните этот командлет в окне PowerShell, чтобы найти список:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Функциональность гостевой настройки регулярно обновляется для поддержки дополнительных наборов политик. Периодически проверяйте наличие новых поддерживаемых политик и оцените, будут ли они полезны.

<!-- TODO: Update these links when available. 

By default, we recommend that you enable the following policies:

- [Preview]: Audit to verify that password-security settings are correct on Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Развертывание.

Используйте следующий пример скрипта PowerShell для развертывания этих политик в:

- Убедитесь, что параметры безопасности пароля на компьютерах Windows и Linux установлены правильно.
- Убедитесь, что сертификаты не близки к истечению срока действия на виртуальных машинах Windows.

 Перед выполнением этого скрипта используйте командлет [Connect-азаккаунт](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) для входа. При запуске скрипта необходимо указать имя подписки, к которой будут применяться политики.

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

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как [включить отслеживание изменений и предупреждения](./enable-tracking-alerting.md) для критически важных изменений файлов, служб, программ и реестра.

> [!div class="nextstepaction"]
> [Включение отслеживания и предупреждений для критических изменений](./enable-tracking-alerting.md)
