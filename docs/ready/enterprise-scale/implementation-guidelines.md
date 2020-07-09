---
title: Рекомендации по реализации КАФ корпоративного масштаба
description: Узнайте о рекомендациях по реализации КАФ корпоративного масштаба в инфраструктуре внедрения Microsoft Cloud для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c06aae816d25ddf15f96292398bbdf0a82d17fd0
ms.sourcegitcommit: 4bbd5f6444d033ef1f38dc6f3bad7b914a82f68f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128162"
---
<!-- cSpell:ignore interdomain VMSS VWAN -->

# <a name="caf-enterprise-scale-implementation-guidelines"></a>Рекомендации по реализации КАФ корпоративного масштаба

В этом разделе описывается, как приступить к работе со встроенной реализацией платформы корпоративного масштаба и целями проектирования структуры.

Существует три категории действий, которые необходимо выполнить для реализации архитектуры корпоративного масштаба:

<!-- docsTest:disable -->

1. **Что должно быть верно для архитектуры корпоративного масштабирования:** Охватывает действия, которые должны выполняться администраторами Azure и Azure AD для установки начальной конфигурации. Эти действия помещаются последовательно и обычно являются одноразовыми действиями.

2. **Включить новый регион (файл-> новый > регион):** Набор действий, которые требуются при необходимости расширить корпоративную платформу в новом регионе Azure.

3. **Разверните новую зону размещения (File-> New-> Главная зона):** Это повторяющиеся действия, необходимые для создания новой целевой зоны.

<!-- docsTest:enable -->

Чтобы эксплуатацию в масштабе, эти действия должны следовать принципам "инфраструктура как код" (IaC) и должны быть автоматизированы с помощью конвейеров развертывания.

## <a name="what-must-be-true-for-a-caf-enterprise-scale-landing-zone"></a>Что должно быть верно для целевой зоны КАФ корпоративного масштаба

### <a name="enterprise-agreement-ea-enrollment-and-azure-ad-tenants"></a>Регистрация Соглашение Enterprise (EA) и клиенты Azure AD

1. Настройте администратора EA и учетную запись уведомления.

2. Создание подразделений: Бизнес-домены, географические или организационные.

3. Создайте учетную запись EA в отделе.

4. Программа установки Azure AD Connect для каждого клиента Azure AD, если удостоверение должно быть синхронизировано из локальной среды.

5. Устанавливайте нулевой доступ к ресурсам Azure и своевременный доступ через Azure AD PIM.

### <a name="management-group-and-subscription"></a>Группа управления и подписка

1. Создайте иерархию группы управления, следуя рекомендациям в этой [статье](./management-group-and-subscription-organization.md#define-a-management-group-hierarchy).

2. Определите критерии подготовки подписки и обязанности владельца подписки.

3. Создание подписок на управление, подключение и идентификацию для управления платформой, глобальных сетей, а так же ресурсов подключения и удостоверений, как Active Directory контроллеров домена.

4. Настройка репозитория Git для размещения IaC и субъектов-служб для использования с конвейером CI/CD.

5. Создание пользовательских определений ролей и управление назначениями с помощью Azure AD PIM для областей подписки и групп управления.

6. Создайте назначения политик Azure в следующей таблице для целевых зон.

| Имя                  | Описание                                                                                   |
|-----------------------|-----------------------------------------------------------------------------------------------|
| [`Deny-PublicEndpoints`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policySetDefinitions-Deny-PublicEndpoints.parameters.json) | Запрещает создание служб с общедоступными конечными точками во всех целевых зонах. |
| [`Deploy-VM-Backup`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-VM-Backup.parameters.json) | Обеспечивает настройку и развертывание резервной копии на всех виртуальных машинах в целевых зонах. |
| [`Deploy-VNet`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Гарантирует, что в каждой из целевых зон развернута виртуальная сеть и что они являются равноправными по отношению к региональному виртуальному концентратору. |

### <a name="global-networking-and-connectivity"></a>Глобальные сетевые подключения и подключение

1. Выделите соответствующий диапазон CIDR для виртуальной сети для каждого региона Azure, в котором будут развернуты виртуальные концентраторы и виртуальных сетей

2. Если вы решили создать сетевые ресурсы с помощью политики Azure, назначьте в подписке подключения политики, перечисленные в таблице ниже. При этом политика Azure обеспечивает создание ресурсов в списке на основе указанных параметров.
   - Создайте экземпляр виртуальной глобальной сети Azure Standard.
   - Создайте виртуальный концентратор виртуальной сети Azure для каждого региона. Убедитесь, что на виртуальном концентраторе развернут хотя бы один шлюз (ExpressRoute или VPN).
   - Обеспечьте безопасность виртуальных концентраторов, развернув брандмауэр Azure в каждом виртуальном концентраторе.
   - Создайте необходимые политики брандмауэра Azure и назначьте их безопасным виртуальным концентраторам.
   - Убедитесь, что все виртуальных сетей, подключенные к защищенному виртуальному концентратору, защищены брандмауэром Azure.

3. Развертывание и настройка зоны Частная зона DNS Azure.

4. Подготавливайте каналы ExpressRoute с помощью частного пиринга Azure. Следуйте инструкциям в статье [Создание и изменение пиринга для канала ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private) .

5. Подключите локальные ХКС/DC к виртуальным концентраторам виртуальных глобальных сетей Azure через каналы ExpressRoute.

6. Защитите трафик виртуальной сети между виртуальными концентраторами с помощью группы безопасности сети.

7. Используемых Настройка шифрования через частный пиринг ExpressRoute. Следуйте инструкциям в разделе [Шифрование expressroute: IPSec через ExpressRoute для виртуальной глобальной сети](https://docs.microsoft.com/azure/virtual-wan/vpn-over-expressroute).

8. Используемых Подключите ветви к виртуальному концентратору через VPN. Следуйте инструкциям в статье [Создание подключения типа "сеть — сеть" с помощью виртуальной глобальной сети Azure](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-site-to-site-portal).

9. Используемых Настройте Global Reach ExpressRoute для подключения к локальным контроллерам домена (ХКС), если в Azure с помощью ExpressRoute подключено несколько локальных расположений. Следуйте инструкциям в разделе [Настройка ExpressRoute Global REACH](https://docs.microsoft.com/azure/expressroute/expressroute-howto-set-global-reach).

В следующем списке приведены назначения политик Azure, используемые при реализации сетевых ресурсов для развертывания корпоративного уровня.

| Имя                     | Описание                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-FirewallPolicy`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-FirewallPolicy.parameters.json) | Создает политику брандмауэра. |
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Эта политика развертывает виртуальный концентратор, брандмауэр Azure и шлюзы VPN/ExpressRoute и настраивает маршрут по умолчанию для подключенной виртуальных сетей к брандмауэру Azure. |
| [`Deploy-VWAN`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vWAN.parameters.json)| Развертывает виртуальную глобальную сеть. |

### <a name="security-governance-and-compliance"></a>Безопасность, система управления и соответствие требованиям

1. Определите и примените [платформу включения службы](./security-governance-and-compliance.md#service-enablement-framework) , чтобы обеспечить соответствие службам Azure требованиям к безопасности и управлению предприятием.

2. Создание настраиваемых определений ролей RBAC Azure.

3. Включите Azure AD PIM и найдите ресурсы Azure, чтобы упростить управление привилегированными пользователями.

4. Создание групп с поддержкой Azure AD для управления ресурсами на плоскости управления Azure с помощью Azure AD PIM.

5. Примените политики, перечисленные в первой таблице ниже, чтобы обеспечить соответствие служб Azure требованиям предприятия.

6. Определите соглашение об именовании и примените его с помощью политики Azure.

7. Создание матрицы политик для всех областей (например, включение мониторинга для всех служб Azure с помощью политики Azure).

Следующие политики следует использовать для принудительного применения состояния соответствия для всей Организации.

| Имя                       | Описание                                                        |
|----------------------------|--------------------------------------------------------------------|
| [`Allowed-ResourceLocation`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Allowed-ResourceLocation.parameters.json)   | Указывает разрешенный регион, в котором можно развертывать ресурсы. |
| [`Allowed-RGLocation`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Allowed-RGLocation.parameters.json)         | Указывает разрешенный регион, в котором можно развертывать группы ресурсов. |
| [`Denied-Resources`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Denied-Resources.parameters.json)           | Ресурс, запрещенный для компании. |
| [`Deny-AppGW-Without-WAF`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-AppGW-Without-WAF.parameters.json)     | Позволяет разворачивать шлюзы приложений с включенным WAF. |
| [`Deny-IP-Forwarding`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-IP-Forwarding.parameters.json)         | Запрет IP-пересылки. |
| [`Deny-RDP-From-Internet`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-RDP-From-Internet.parameters.json)     | Запретить подключения по протоколу RDP из Интернета. |
| [`Deny-Subnet-Without-Nsg`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-Subnet-Without-Nsg.parameters.json)    | Запретить создание подсети без NSG. |
| [`Deploy-ASC-CE`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-CE.parameters.json)              | Настройка непрерывного экспорта центра безопасности в рабочую область Log Analytics. |
| [`Deploy-ASC-Monitoring`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Monitoring.parameters.json)      | Включите наблюдение в центре безопасности Azure. |
| [`Deploy-ASC-Standard`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Standard.parameters.json)        | Гарантирует, что для подписок включен стандартный центр безопасности. |
| [`Deploy-Diag-ActivityLog`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diag-ActivityLog.parameters.json) | Включает журнал действий диагностики и пересылает Log Analytics. |
| [`Deploy-Diag-LogAnalytics`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diag-LogAnalytics.parameters.json) | |
| [`Deploy-VM-Monitoring`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-VM-Monitoring.parameters.json) | Обеспечивает включение наблюдения за виртуальными машинами. |

### <a name="platform-identity"></a>Удостоверение платформы

1. Если вы решили создать ресурсы идентификации с помощью политики Azure, назначьте политики, перечисленные в таблице ниже, в качестве подписки Identity. При этом политика Azure обеспечивает создание ресурсов в списке на основе указанных параметров.

2. Разверните Active Directory контроллеры домена.

В следующем списке перечислены политики, которые можно использовать при реализации ресурсов удостоверений для развертывания корпоративного уровня.

| Имя                         | Описание                                                               |
|------------------------------|---------------------------------------------------------------------------|
| [`DataProtectionSecurityCenter`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-DataProtectionSecurityCenter.parameters.json) | Защита данных автоматически создается центром безопасности Azure. |
| [`Deploy-VNet-Identity`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Развертывает виртуальную сеть в подписке по удостоверениям для размещения (например, DC). |

### <a name="platform-management-and-monitoring"></a>Управление платформой и мониторинг

1. Создание панелей мониторинга соответствия политике и безопасности для организационных и ресурсных представлений.

2. Создайте рабочий процесс для секретов платформы (субъектов-служб и учетная запись службы автоматизации) и смену ключей.

3. Настройка долгосрочного архивирования и хранения журналов в Log Analytics.

4. Программа установки Azure Key Vault для хранения секретов платформы.

5. Если вы решили создать ресурсы управления платформой с помощью политики Azure, назначьте политики, перечисленные в таблице ниже, в подписку управления. При этом политика Azure гарантирует, что ресурс в приведенном ниже списке будет создан на основе предоставленных параметров.

| Имя                   | Описание                                                                            |
|------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-LA-Config`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-LA-Config.parameters.json) | Настройка рабочей области Log Analytics. |
| [`Deploy-Log-Analytics`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | Развертывает рабочую область Log Analytics. |

## <a name="file--new--region"></a>**Файл-> новый > регион**

1. Если вы решили создать сетевые ресурсы с помощью политики Azure, назначьте в подписке подключения политики, перечисленные в таблице ниже. При этом политика Azure обеспечит создание ресурса в приведенном ниже списке на основе указанных параметров.

    - В подписке подключения создайте новый виртуальный концентратор в существующей виртуальной глобальной сети.
    - Обеспечьте безопасность виртуального концентратора, развернув брандмауэр Azure в виртуальном концентраторе и свяжите существующие или новые политики брандмауэра с брандмауэром Azure.
    - Убедитесь, что все виртуальных сетей, подключенные к защищенному виртуальному концентратору, защищены брандмауэром Azure.

2. Подключите виртуальный концентратор к локальной сети с помощью ExpressRoute или VPN.

3. Защитите трафик виртуальной сети между виртуальными концентраторами через группы безопасности сети.

4. Используемых Настройка шифрования через частный пиринг ExpressRoute.

| Имя                     | Описание                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Эта политика развертывает виртуальный концентратор, брандмауэр Azure, шлюзы (VPN и ExpressRoute) и настраивает маршрут по умолчанию для подключенных виртуальных сетей к брандмауэру Azure. |

<!-- docsTest:disable -->

## <a name="file---new---landing-zone-for-applications-and-workloads"></a>Файловая > новая > зона для приложений и рабочих нагрузок

<!-- docsTest:enable -->

1. Создайте подписку и переместите ее в `Landing Zones` область группы управления.

2. Создайте группы Azure AD для подписки, такие как `Owner` , `Reader` и `Contributor` .

3. Создание прав PIM Azure AD для установленных групп Azure AD.
