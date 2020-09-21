---
title: Рекомендации по реализации корпоративного масштаба
description: Узнайте о рекомендациях по реализации корпоративного масштаба в инфраструктуре внедрения Microsoft Cloud для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 25467593af277cf5955fc9656e23f9d01fa8926b
ms.sourcegitcommit: 4e12d2417f646c72abf9fa7959faebc3abee99d8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90776437"
---
<!-- cSpell:ignore interdomain VMSS VWAN -->

# <a name="enterprise-scale-implementation-guidelines"></a>Рекомендации по реализации корпоративного масштаба

В этой статье описывается, как приступить к работе с архитектурой корпоративного уровня, собственной платформой и целями проектирования структуры.

Чтобы реализовать архитектуру корпоративного уровня, необходимо учесть следующие категории действий.

<!-- docutune:disable -->

1. **Что должно быть верно для архитектуры корпоративного масштабирования:** Охватывает действия, которые должны выполняться администраторами Azure и Azure Active Directory (Azure AD) для установки начальной конфигурации. Эти действия помещаются последовательно и обычно являются одноразовыми действиями.

2. **Включить новый регион (файл > новый > регион):** Охватывает действия, которые требуются при необходимости расширить корпоративную платформу в новом регионе Azure.

3. **Разверните новую целевую зону (файл > новая > Главная зона):** Это повторяющиеся действия, необходимые для создания новой целевой зоны.

<!-- docutune:enable -->

Чтобы эксплуатацию в масштабе, эти действия должны следовать принципам "инфраструктура как код" (IaC) и должны быть автоматизированы с помощью конвейеров развертывания.

## <a name="what-must-be-true-for-an-enterprise-scale-landing-zone"></a>Что должно быть верно для целевой зоны корпоративного уровня

В следующих разделах перечислены действия по выполнению этой категории действий в инфраструктуре внедрения Microsoft Cloud для Azure.

### <a name="enterprise-agreement-enrollment-and-azure-ad-tenants"></a>Регистрация Соглашение Enterprise и клиенты Azure AD

1. Настройка администратора Соглашение Enterprise (EA) и учетной записи уведомления.

2. Создание подразделений: Бизнес-домены, географические или организационные.

3. Создайте учетную запись EA в отделе.

4. Настройте Azure AD Connect для каждого клиента Azure AD, если удостоверение должно быть синхронизировано из локальной среды.

5. Установите нулевой доступ к ресурсам Azure и JIT-доступ через Azure AD Privileged Identity Management (PIM).

### <a name="management-group-and-subscription"></a>Группа управления и подписка

1. Создайте иерархию группы управления, следуя рекомендациям в [группе управления и организации подписки](./management-group-and-subscription-organization.md#define-a-management-group-hierarchy).

2. Определите критерии для подготовки подписки и обязанности владельца подписки.

3. Создание подписок на управление, подключение и идентификацию для управления платформой, глобальных сетей, а так же ресурсов подключения и удостоверений, как Active Directory контроллеров домена.

4. Настройте репозиторий Git для размещения IaC и субъектов-служб для использования с конвейером платформы для непрерывной интеграции и непрерывного развертывания.

5. Создание пользовательских определений ролей и управление назначениями с помощью Azure AD PIM для областей подписки и групп управления.

6. Создайте назначения политик Azure в следующей таблице для целевых зон.

  | Имя                  |     Описание                                                                                     |
  |-----------------------|-----------------------------------------------------------------------------------------------|
  | [`Deny-PublicEndpoints`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policySetDefinitions-Deny-PublicEndpoints.parameters.json) | Запрещает создание служб с общедоступными конечными точками во всех целевых зонах. |
  | [`Deploy-VM-Backup`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/Landing%20Zones%20(landingzones)/.AzState/Microsoft.Authorization_policyAssignments-Deploy-VM-Backup.parameters.json) | Обеспечивает настройку и развертывание резервной копии на всех виртуальных машинах в целевых зонах. |
  | [`Deploy-VNet`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Гарантирует, что на всех целевых зонах развернута виртуальная сеть, и что она является одноранговым по отношению к региональному виртуальному концентратору. |

### <a name="global-networking-and-connectivity"></a>Глобальные сетевые подключения и подключение

1. Выделите соответствующий диапазон CIDR виртуальной сети для каждого региона Azure, в котором будут развернуты виртуальные концентраторы и виртуальные сети.

2. Если вы решили создать сетевые ресурсы с помощью политики Azure, назначьте в подписке подключения политики, перечисленные в следующей таблице. При этом политика Azure гарантирует, что ресурсы в следующем списке будут созданы на основе указанных параметров.
   - Создайте экземпляр виртуальной глобальной сети Azure Standard.
   - Создайте виртуальный концентратор виртуальной сети Azure для каждого региона. Убедитесь, что на виртуальном концентраторе развернут хотя бы один шлюз (Azure ExpressRoute или VPN).
   - Обеспечьте безопасность виртуальных концентраторов, развернув брандмауэр Azure в каждом виртуальном концентраторе.
   - Создайте необходимые политики брандмауэра Azure и назначьте их безопасным виртуальным концентраторам.
   - Убедитесь, что все виртуальные сети, подключенные к защищенному виртуальному концентратору, защищены брандмауэром Azure.

3. Развертывание и настройка зоны Частная зона DNS Azure.

4. Подготавливайте каналы ExpressRoute с помощью частного пиринга Azure. Следуйте инструкциям в разделе [Создание и изменение пиринга для канала ExpressRoute](/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private).

5. Подключите локальные ХКС/DC к виртуальным концентраторам виртуальных глобальных сетей Azure через каналы ExpressRoute.

6. Защита трафика виртуальной сети между виртуальными концентраторами с помощью групп безопасности сети (группы безопасности сети).

7. Используемых Настройка шифрования через частный пиринг ExpressRoute. Следуйте инструкциям в разделе [Шифрование expressroute: IPSec через ExpressRoute для виртуальной глобальной сети](/azure/virtual-wan/vpn-over-expressroute).

8. Используемых Подключите ветви к виртуальному концентратору через VPN. Следуйте инструкциям в статье [Создание подключения типа "сеть — сеть" с помощью виртуальной глобальной сети Azure](/azure/virtual-wan/virtual-wan-site-to-site-portal).

9. Используемых Настройте Global Reach ExpressRoute для подключения к локальным контроллерам домена (ХКС), если в Azure с помощью ExpressRoute подключено несколько локальных расположений. Следуйте инструкциям в разделе [Настройка ExpressRoute Global REACH](/azure/expressroute/expressroute-howto-set-global-reach).

В следующем списке приведены назначения политик Azure, используемые при реализации сетевых ресурсов для развертывания корпоративного уровня.

| Имя                     | Описание                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-FirewallPolicy`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-FirewallPolicy.parameters.json) | Создает политику брандмауэра. |
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Эта политика развертывает виртуальный концентратор, брандмауэр Azure и шлюзы VPN/ExpressRoute. Он также настраивает маршрут по умолчанию для подключенных виртуальных сетей к брандмауэру Azure. |
| [`Deploy-VWAN`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vWAN.parameters.json)| Развертывает виртуальную глобальную сеть. |

### <a name="security-governance-and-compliance"></a>Безопасность, система управления и соответствие требованиям

1. Определите и примените [платформу включения службы](./security-governance-and-compliance.md#service-enablement-framework) , чтобы обеспечить соответствие службам Azure требованиям к безопасности и управлению предприятием.

2. Создание пользовательских определений управления доступом на основе ролей.

3. Включение PIM Azure AD и обнаружение ресурсов Azure для упрощения PIM.

4. Создайте группы только Azure AD для управления ресурсами на плоскости управления Azure с помощью Azure AD PIM.

5. Примените политики, перечисленные в следующей таблице, чтобы обеспечить соответствие служб Azure требованиям предприятия.

6. Определите соглашение об именовании и примените его с помощью политики Azure.

7. Создание матрицы политик для всех областей (например, включение мониторинга для всех служб Azure с помощью политики Azure).

Следующие политики следует использовать для принудительного применения состояния соответствия для всей Организации.

| Имя                       | Описание                                                        |
|----------------------------|--------------------------------------------------------------------|
| [`Allowed-ResourceLocation`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Allowed-ResourceLocation.parameters.json)   | Указывает разрешенный регион, в котором можно развертывать ресурсы. |
| [`Allowed-RGLocation`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Allowed-RGLocation.parameters.json)         | Указывает разрешенный регион, в котором можно развертывать группы ресурсов. |
| [`Denied-Resources`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Denied-Resources.parameters.json)           | Ресурсы, запрещенные для компании. |
| [`Deny-AppGW-Without-WAF`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deny-AppGW-Without-WAF.parameters.json)     | Позволяет разворачивать шлюзы приложений с включенным брандмауэром веб-приложения Azure. |
| [`Deny-IP-Forwarding`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Deny-IP-Forwarding.parameters.json)         | Запрещает IP-пересылку. |
| [`Deny-RDP-From-Internet`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Deny-RDP-From-Internet.parameters.json)     | Запрещает RDP-подключения из Интернета. |
| [`Deny-Subnet-Without-Nsg`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deny-Subnet-Without-Nsg.parameters.json)    | Запрещает создание подсети без NSG. |
| [`Deploy-ASC-CE`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-CE.parameters.json)              | Настройка непрерывного экспорта центра безопасности Azure в рабочую область Log Analytics. |
| [`Deploy-ASC-Monitoring`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Deploy-ASC-Monitoring.parameters.json)      | Включает наблюдение в центре безопасности. |
| [`Deploy-ASC-Standard`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Standard.parameters.json)        | Гарантирует, что для подписок включен стандартный центр безопасности. |
| [`Deploy-Diag-ActivityLog`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diagnostics-ActivityLog.parameters.json) | Включает журнал действий диагностики и пересылает Log Analytics. |
| [`Deploy-Diag-LogAnalytics`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | |
| [`Deploy-VM-Monitoring`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diagnostics-VM.parameters.json) | Обеспечивает включение наблюдения за виртуальными машинами. |

### <a name="platform-identity"></a>Удостоверение платформы

1. При создании ресурсов удостоверений с помощью политики Azure назначьте политики, перечисленные в следующей таблице, с удостоверением подписки. При этом политика Azure гарантирует, что ресурсы в следующем списке будут созданы на основе указанных параметров.

2. Разверните Active Directory контроллеры домена.

В следующем списке перечислены политики, которые можно использовать при реализации ресурсов удостоверений для развертывания корпоративного уровня.

| Имя                         | Описание                                                               |
|------------------------------|---------------------------------------------------------------------------|
| [`DataProtectionSecurityCenter`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/) | Защита данных автоматически создается центром безопасности. |
| [`Deploy-VNet-Identity`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Развертывает виртуальную сеть в подписке по удостоверениям для размещения (например, контроллера домена). |

### <a name="platform-management-and-monitoring"></a>Управление платформой и мониторинг

1. Создание панелей мониторинга соответствия политике и безопасности для организационных и ресурсных представлений.

2. Создайте рабочий процесс для секретов платформы (субъектов-служб и учетная запись службы автоматизации) и смену ключей.

3. Настройте долгосрочное архивирование и хранение журналов в Log Analytics.

4. Настройте Azure Key Vault для хранения секретов платформы.

5. При создании ресурсов управления платформой с помощью политики Azure назначьте политики, перечисленные в следующей таблице, в подписку управления. При этом политика Azure гарантирует, что ресурсы в следующем списке будут созданы на основе указанных параметров.

| Имя                   | Описание                                                                            |
|------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-LA-Config`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-LA-Config.parameters.json) | Настройка рабочей области Log Analytics. |
| [`Deploy-Log-Analytics`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | Развертывает рабочую область Log Analytics. |

## <a name="file--new--region"></a>Файл > новый регион >

1. Если вы создаете сетевые ресурсы с помощью политики Azure, назначьте в подписке подключения политики, перечисленные в следующей таблице. При этом политика Azure гарантирует, что ресурсы в следующем списке будут созданы на основе указанных параметров.

    - В подписке подключения создайте новый виртуальный концентратор в существующей виртуальной глобальной сети.
    - Обеспечьте безопасность виртуального концентратора, развернув брандмауэр Azure в виртуальном концентраторе и свяжите существующие или новые политики брандмауэра с брандмауэром Azure.
    - Убедитесь, что все виртуальные сети, подключенные к защищенному виртуальному концентратору, защищены брандмауэром Azure.

2. Подключите виртуальный концентратор к локальной сети с помощью ExpressRoute или VPN.

3. Защитите трафик виртуальной сети между виртуальными концентраторами через группы безопасности сети.

4. Используемых Настройка шифрования через частный пиринг ExpressRoute.

| Имя                     | Описание                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Эта политика развертывает виртуальный концентратор, брандмауэр Azure и шлюзы (VPN/ExpressRoute). Он также настраивает маршрут по умолчанию для подключенных виртуальных сетей к брандмауэру Azure. |

<!-- docutune:disable -->

## <a name="file--new--landing-zone-for-applications-and-workloads"></a>Файл > новая > Главная зона для приложений и рабочих нагрузок

<!-- docutune:enable -->

1. Создайте подписку и переместите ее в `Landing Zones` область группы управления.

2. Создайте группы Azure AD для подписки, такие как `Owner` , `Reader` и `Contributor` .

3. Создание прав PIM Azure AD для установленных групп Azure AD.
