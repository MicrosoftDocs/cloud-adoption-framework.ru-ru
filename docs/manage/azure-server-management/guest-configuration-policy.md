---
title: Расширение гостевой настройки политики Azure
description: Используйте облачную платформу внедрения для Azure, чтобы узнать, как использовать расширение гостевой конфигурации политики Azure для аудита параметров конфигурации на виртуальной машине Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: internal
ms.openlocfilehash: 66e93f25101f29890cdcc367560e2ab8d996353e
ms.sourcegitcommit: b6f2b4f8db6c3b1157299ece1f044cff56895919
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97017077"
---
# <a name="azure-policy-guest-configuration-extension"></a>Расширение гостевой настройки политики Azure

Для аудита параметров конфигурации на виртуальной машине можно использовать [расширение гостевой настройки политики Azure](/azure/governance/policy/concepts/guest-configuration) . В настоящее время Гостевая конфигурация поддерживается только на виртуальных машинах Azure.

Чтобы найти список политик конфигурации гостей, выполните поиск **конфигурации гостя** на странице портала политики Azure или выполните этот командлет в окне PowerShell, чтобы найти список:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Функциональность гостевой настройки регулярно обновляется для поддержки дополнительных наборов политик. Периодически проверяйте наличие новых поддерживаемых политик и оцените, будут ли они полезны.

## <a name="deployment"></a>Развертывание

Используйте следующий пример скрипта PowerShell для развертывания этих политик в:

- Убедитесь, что параметры безопасности пароля на компьютерах Windows и Linux установлены правильно.
- Убедитесь, что сертификаты не близки к истечению срока действия на виртуальных машинах Windows.

 Перед выполнением этого скрипта используйте командлет [Connect-азаккаунт](/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) для входа. При запуске скрипта необходимо указать имя подписки, к которой будут применяться политики.

```powershell

    # Assign Guest Configuration policy.

    param (
        [Parameter(Mandatory=$true)]
        [string] $SubscriptionName
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
