---
title: Общие примеры политики Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Общие примеры политики Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9eee6f81922c88304c0ca5bf7edd6572daf493d8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029893"
---
# <a name="common-azure-policy-examples"></a>Общие примеры политики Azure

[Политика Azure](https://docs.microsoft.com/azure/governance/policy/overview) поможет вам применить управление к облачным ресурсам. Эта служба поможет вам создать снятие, обеспечивающую соответствие требованиям политики управления в масштабах всей Организации. Чтобы создать политики, используйте командлеты портал Azure или PowerShell. В этой статье приведены примеры командлетов PowerShell.

> [!NOTE]
> С помощью политики Azure политики принудительного применения (**deployIfNotExists**) не развертываются автоматически на существующих виртуальных машинах. Для обеспечения соответствия этих виртуальных машин необходимо исправление. Дополнительные сведения см. в статье [исправление ресурсов, которые не соответствуют требованиям, с помощью политики Azure](https://docs.microsoft.com/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Примеры общих политик

В следующих разделах описываются некоторые часто используемые политики.

### <a name="restrict-resource-regions"></a>Ограничить регионы ресурсов

Нормативные требования и соответствие политике часто зависят от управления физическим расположением, в котором развертываются ресурсы. Вы можете использовать встроенную политику, позволяющую пользователям создавать ресурсы только в список разрешений регионах Azure. Эту политику можно найти на портале, выполнив поиск по слову "расположение" на странице определения политики.

Также можно выполнить этот командлет, чтобы найти политику.

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*location*") }
```

В следующем сценарии показано, как назначить политику. Чтобы использовать скрипт, измените `$SubscriptionID` значение так, чтобы оно указывало на подписку, которой нужно назначить политику. Перед выполнением скрипта необходимо выполнить вход с помощью командлета [Connect-азаккаунт](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) .

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{"listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyparam
```

Этот же скрипт можно использовать для применения других политик, обсуждаемых в этой статье. Просто замените GUID в строке, которая задает `$AllowedLocationPolicy` идентификатор GUID политики, которую необходимо применить.

### <a name="block-certain-resource-types"></a>Блокировать определенные типы ресурсов

Другая распространенная политика, используемая для управления затратами, позволяет блокировать определенные типы ресурсов. Эту политику можно найти на портале, выполнив поиск по фразе "разрешенные типы ресурсов" на странице Определение политики.

Также можно выполнить этот командлет, чтобы найти политику.

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

Определив политику, которую вы хотите использовать, можно изменить пример PowerShell в разделе [ограничение области ресурсов](#restrict-resource-regions) , чтобы назначить политику.

### <a name="restrict-vm-size"></a>Ограничение размера виртуальной машины

Azure предлагает широкий спектр размеров виртуальных машин для поддержки различных типов рабочих нагрузок. Для управления бюджетом можно создать политику, которая допускает только подмножество размеров виртуальных машин в ваших подписках.

### <a name="deploy-antimalware"></a>Развертывание антивредоносной программы

С помощью этой политики можно развернуть расширение Microsoft IaaSAntimalware с конфигурацией по умолчанию для виртуальных машин, не защищенных с помощью антивредоносной программы.

GUID политики — `2835b622-407b-4114-9198-6f7064cbe0dc`.

В следующем сценарии показано, как назначить политику. Чтобы использовать скрипт, измените `$SubscriptionID` значение так, чтобы оно указывало на подписку, которой нужно назначить политику. Перед выполнением скрипта необходимо выполнить вход с помощью командлета [Connect-азаккаунт](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) .

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location “eastus” with the value you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Следующие шаги

Узнайте о других доступных средствах и службах управления сервером.

> [!div class="nextstepaction"]
> [Средства и службы управления сервером Azure](./tools-services.md)
