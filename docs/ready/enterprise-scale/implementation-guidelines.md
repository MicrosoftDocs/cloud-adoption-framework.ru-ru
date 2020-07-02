---
title: Рекомендации по реализации
description: Рекомендации по реализации.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 392e1e9625f631a76cd7584d4cc31485bcea8f0a
ms.sourcegitcommit: 7c16b2857b00520bec3c4f6e9844ceac33970846
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766784"
---
<!-- cSpell:ignore interdomain VMSS -->

# <a name="implementation-guidelines"></a>Рекомендации по реализации

В этом разделе описывается, как приступить к работе со встроенной реализацией платформы корпоративного масштаба и целями проектирования структуры.

Существует три категории действий, которые необходимо выполнить для реализации архитектуры корпоративного масштаба:

1. **Что должно быть верно для архитектуры корпоративного масштабирования:** Охватывает действия, которые должны выполняться администраторами Azure и Azure AD для установки начальной конфигурации. Эти действия помещаются последовательно и обычно являются одноразовыми действиями.

2. **Включить новый регион (_файл-> новый > регион_):** Набор действий, которые требуются при необходимости расширить корпоративную платформу в новом регионе Azure.

3. **Разверните новую зону размещения (_File-> new-> Главная зона_):** Это повторяющиеся действия, необходимые для создания новой целевой зоны.

Чтобы эксплуатацию в масштабе, эти действия должны следовать принципам "инфраструктура как код" (IaC) и должны быть автоматизированы с помощью конвейеров развертывания.

## <a name="what-must-be-true-for-an-enterprise-scale-landing-zone"></a>Что должно быть верно для целевой зоны корпоративного уровня

### <a name="enterprise-agreement-ea-enrollment-and-azure-ad-tenants"></a>Регистрация Соглашение Enterprise (EA) и клиенты Azure AD

1. Настройте администратора EA и учетную запись уведомления.

2. Создание отделов — бизнес-домены или географические Организации.

3. Создайте учетную запись EA в отделе.

4. Программа установки Azure AD Connect для каждого клиента Azure AD, если удостоверение должно быть синхронизировано из локальной среды.

5. Устанавливайте нулевой доступ к ресурсам Azure и своевременный доступ через Azure AD PIM.

### <a name="management-group-and-subscription"></a>Группа управления и подписка

1. Создайте иерархию группы управления, следуя рекомендациям в этой [статье](./management-group-and-subscription-organization.md#define-a-management-group-hierarchy).

2. Определите критерии подготовки подписки и обязанности владельца подписки.

3. Создание подписок, подключений и удостоверений для управления платформой, глобальных сетей и ресурсов подключения и удостоверений, таких как контроллеры доменов AD.

4. Настройка репозитория Git для размещения IaC и субъектов-служб для использования с конвейером CI/CD.

5. Создание пользовательских определений ролей и управление назначениями с помощью Azure AD PIM для областей подписки и групп управления.

6. Создайте назначения политик Azure в следующей таблице для целевых зон.

| name                  | Описание                                                                                   |
|-----------------------|-----------------------------------------------------------------------------------------------|
| [Deny-Публицендпоинтс](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policySetDefinitions-Deny-PublicEndpoints.parameters.json)  | Запрещает создание служб с общедоступными конечными точками во всех целевых зонах.                    |
| [Развертывание виртуальной машины и резервное копирование](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-VM-Backup.parameters.json)      | Обеспечивает настройку и развертывание резервной копии на всех виртуальных машинах в целевых зонах.                |
| [Deploy-VNet](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json)           | Гарантирует, что виртуальная сеть развернута и подключена к виртуальному концентратору регонал. |

### <a name="global-networking-and-connectivity"></a>Глобальные сетевые подключения и подключение

1. Выделите соответствующий диапазон CIDR для виртуальной сети для каждого региона Azure, в котором будут развернуты виртуальные концентраторы и виртуальных сетей

2. Если вы решили создать сетевые ресурсы с помощью политики Azure, назначьте в подписке подключения политики, перечисленные в таблице ниже. При этом политика Azure обеспечивает создание ресурсов в списке на основе указанных параметров.
   - Создайте виртуальную глобальную сеть Azure Standard.
   - Создайте виртуальный концентратор виртуальной сети Azure для каждого региона. Убедитесь, что на виртуальном концентраторе развернут хотя бы один шлюз (ExpressRoute или VPN).
   - Обеспечьте безопасность виртуальных концентраторов, развернув брандмауэр Azure в каждом виртуальном концентраторе.
   - Создайте необходимые политики брандмауэра Azure и назначьте их безопасным виртуальным концентраторам.
   - Убедитесь, что все виртуальных сетей, подключенные к защищенному виртуальному концентратору, защищены брандмауэром Azure.

3. Развертывание и настройка зоны Частная зона DNS Azure.

4. Подготавливайте каналы ExpressRoute с помощью частного пиринга Azure. Следуйте инструкциям в статье [Создание и изменение пиринга для канала ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private) .

5. Подключите локальные ХКС/DC к виртуальным концентраторам виртуальных глобальных сетей Azure через каналы ExpressRoute.

6. Защитите трафик виртуальной сети между виртуальными концентраторами с помощью группы безопасности сети.

7. Используемых Настройка шифрования через частный пиринг ExpressRoute. Следуйте инструкциям в разделе [Шифрование expressroute: IPSec через ExpressRoute для виртуальной глобальной сети](https://docs.microsoft.com/en-us/azure/virtual-wan/vpn-over-expressroute).

8. Используемых Подключите ветви к виртуальному концентратору через VPN. Следуйте инструкциям в статье [Создание подключения типа "сеть — сеть" с помощью виртуальной глобальной сети Azure](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-site-to-site-portal).

9. Используемых Настройте Global Reach ExpressRoute для подключения к локальным контроллерам домена (ХКС), если в Azure с помощью ExpressRoute подключено несколько локальных расположений. Следуйте инструкциям в разделе [Настройка ExpressRoute Global REACH](https://docs.microsoft.com/azure/expressroute/expressroute-howto-set-global-reach).

В следующем списке приведены назначения политик Azure, используемые при реализации сетевых ресурсов для развертывания корпоративного уровня.

| name                     | Описание                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [Deploy-Фиреваллполици](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-FirewallPolicy.parameters.json)  | Создает политику брандмауэра. |
| [Deploy-Вхуб](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json)        | Эта политика развертывает виртуальный концентратор, брандмауэр Azure, шлюзы (VPN/ExpressRoute) и настраивает маршрут по умолчанию для подключенных виртуальных сетей к брандмауэру Azure. |
| [Deploy-ВВАН](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vWAN.parameters.json)            | Развертывает виртуальную глобальную сеть                             |

### <a name="security-governance-and-compliance"></a>Безопасность, система управления и соответствие требованиям

1. Определите и примените [платформу включения службы](./security-governance-and-compliance.md#service-enablement-framework) , чтобы обеспечить соответствие службам Azure требованиям к безопасности и управлению предприятием.

2. Создание настраиваемых определений ролей RBAC Azure.

3. Включите Azure AD PIM и найдите ресурсы Azure, чтобы упростить управление привилегированными пользователями.

4. Создание групп с поддержкой Azure AD для управления ресурсами на плоскости управления Azure с помощью Azure AD PIM.

5. Примените политики, перечисленные в первой таблице ниже, чтобы обеспечить соответствие служб Azure требованиям предприятия.

6. Определите соглашение об именовании и примените его с помощью политики Azure.

7. Создание матрицы политик для всех областей (например, включение мониторинга для всех служб Azure с помощью политики Azure).

Следующие политики следует использовать для принудительного применения состояния соответствия для всей Организации.

| name                       | Описание                                                        |
|----------------------------|--------------------------------------------------------------------|
| [Allowed-Ресаурцелокатион](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Allowed-ResourceLocation.parameters.json)   | Указывает разрешенный регион, в котором можно развернуть ресаурцен       |
| [Allowed-RGLocation](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Allowed-RGLocation.parameters.json)         | Указывает разрешенный регион, в котором можно развертывать группы ресурсов |
| [Запрещенные ресурсы](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Denied-Resources.parameters.json)           | Ресурс, запрещенный для компании                           |
| [Deny-AppGW-без-WAF](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-AppGW-Without-WAF.parameters.json)     | Разрешает использовать шлюзы приложений, развернутые с включенной WAF              |
| [Deny-IP-пересылка](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-IP-Forwarding.parameters.json)         | Запретить IP-пересылку                                                 |
| [Deny-RDP-From-Internet](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-RDP-From-Internet.parameters.json)     | Запретить подключения по протоколу RDP из Интернета                                 |
| [Deny-Subnet-без-NSG](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-Subnet-Without-Nsg.parameters.json)    | Запретить создание подсети без NSG                                |
| [Deploy-ASC-CE](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-CE.parameters.json)              | Развертывание по УБЫВАНИЮ непрерывного экспорта в рабочую область                          |
| [Deploy-ASC-Monitoring](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Monitoring.parameters.json)      | Включение мониторинга в Центре безопасности Azure                         |
| [Deploy-ASC-Standard](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Standard.parameters.json)        | Гарантирует, что в подписках включен стандартный центр безопасности.  |
| [Deploy-DIAG-ActivityLog](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diag-ActivityLog.parameters.json)    | Включает журнал диагностики Активитли и пересылает его в LA             |
| [Deploy-DIAG-LogAnalytics](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diag-LogAnalytics.parameters.json)   |                                                                    |
| [Развертывание-VM-Monitoring](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-VM-Monitoring.parameters.json)       | Обеспечивает включение наблюдения за виртуальными машинами  

### <a name="platform-indentity"></a>Отступ платформы

1. Если вы решили создать ресурсы идентификации с помощью политики Azure, назначьте политики, перечисленные в таблице ниже, в качестве подписки Identity. При этом политика Azure обеспечивает создание ресурсов в списке на основе указанных параметров.

2. Разверните контроллеры домена AD.

В следующем списке перечислены политики, которые можно использовать при реализации ресурсов удостоверений для развертывания корпоративного уровня.

| name                         | Описание                                                               |
|------------------------------|---------------------------------------------------------------------------|
| [датапротектионсекуритицентер](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-DataProtectionSecurityCenter.parameters.json) | ASC Protection, автоматически создаваемая центром безопасности Azure         |
| [Развертывание-виртуальная сеть — удостоверение](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json)         | Развертывает виртуальную сеть в подписке Identity для размещения, например DC.     |

### <a name="platform-management-and-monitoring"></a>Управление платформой и мониторинг

1. Создание панелей мониторинга соответствия политике и безопасности для организационных и ресурсных представлений.

2. Создайте рабочий процесс для секретов платформы (субъектов-служб и учетная запись службы автоматизации) и смену ключей.

3. Настройка долгосрочного архивирования и хранения журналов в Log Analytics.

4. Программа установки Azure Key Vault для хранения секретов платформы.

5. Если вы решили создать ресурсы управления платформой с помощью политики Azure, назначьте политики, перечисленные в таблице ниже, в подписку управления. При этом политика Azure гарантирует, что ресурс в приведенном ниже списке будет создан на основе предоставленных параметров.

| name                   | Описание                                                                            |
|------------------------|----------------------------------------------------------------------------------------|
| [Deploy-LA-config](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-LA-Config.parameters.json)       | Настройка рабочей области Log Analytics                                           |
| [Развертывание-log-Analytics](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json)   | Развертывает рабочую область Log Analytics |

## <a name="file--new--region"></a>**Файл-> новый > регион**

1. Если вы решили создать сетевые ресурсы с помощью политики Azure, назначьте в подписке подключения политики, перечисленные в таблице ниже. При этом политика Azure обеспечит создание ресурса в приведенном ниже списке на основе указанных параметров.
   - В рамках подписки на подключение создайте новый виртуальный концентратор в существующей виртуальной глобальной сети.
   - Обеспечьте безопасность виртуального концентратора, развернув брандмауэр Azure в виртуальном концентраторе и свяжите существующие или новые политики брандмауэра с брандмауэром Azure.
   - Убедитесь, что все виртуальных сетей, подключенные к защищенному виртуальному концентратору, защищены брандмауэром Azure.

2. Подключите виртуальный концентратор к локальной сети с помощью ExpressRoute или VPN.

3. Защитите трафик виртуальной сети между виртуальными концентраторами через группы безопасности сети.

4. Используемых Настройка шифрования через частный пиринг ExpressRoute.

| name                     | Описание                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [Deploy-Вхуб](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json)        | Эта политика развертывает виртуальный концентратор, брандмауэр Azure, шлюзы (VPN и ExpressRoute) и настраивает маршрут по умолчанию для подключенных виртуальных сетей к брандмауэру Azure. |

## <a name="file---new---landing-zone-for-applications-and-workloads"></a>Файловая > новая > зона для приложений и рабочих нагрузок

1. Создайте подписку и переместите ее в `Landing Zones` область группы управления.

2. Создание групп Azure AD для подписки — владельца, читателя, участника и т. д.

3. Создание прав PIM Azure AD для установленных групп Azure AD.
