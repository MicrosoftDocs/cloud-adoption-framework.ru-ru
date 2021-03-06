---
title: Управление удостоверениями и доступом (IAM)
description: Ознакомьтесь со сведениями о проектировании и рекомендациями по управлению удостоверениями и доступом в корпоративной среде.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 8fbce73e4cd0ae47beeb348be151093dda932c27
ms.sourcegitcommit: 3dd5cb5e84df8049ecbd484061e6df16a1914bb5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/09/2021
ms.locfileid: "102515385"
---
# <a name="identity-and-access-management"></a>Управление удостоверениями и доступом

Удостоверение предоставляет базу данных большого объема в процентах от гарантии безопасности. Оно обеспечивает доступ на основе проверки подлинности и управления авторизацией в облачных службах для защиты данных и ресурсов и принятия решения о том, какие запросы должны быть разрешены.

Система управления идентификацией и доступом (IAM) — это пограничная безопасность в общедоступном облаке. Она должна рассматриваться как основа любой безопасной и полностью соответствующей архитектуры общедоступного облака. Azure предлагает комплексный набор служб, средств и эталонных архитектур, позволяющий организациям создавать Высокобезопасные и ресурсоемкие среды, как описано здесь.

В этом разделе рассматриваются вопросы проектирования и рекомендации, связанные с IAM в среде предприятия.

## <a name="why-we-need-identity-and-access-management"></a>Зачем требуется управление удостоверениями и доступом

Технологические ландшафты на предприятии становятся сложными и разнородных. Чтобы управлять соответствием и безопасностью в этой среде, IAM позволяет подходящего лицам получать доступ к нужным ресурсам в нужное время по правильным причинам.

### <a name="plan-for-identity-and-access-management"></a>Планирование управления удостоверениями и доступом

Корпоративные организации обычно придерживаются подхода с минимальными привилегиями при оперативном доступе. Эта модель должна быть расширена, чтобы использовать Azure с помощью Azure Active Directory (Azure AD), управления доступом на основе ролей Azure (Azure RBAC) и пользовательских определений ролей. Очень важно спланировать управление доступом к ресурсам в Azure на уровне управления и плоскости данных. Любой проект для IAM и Azure RBAC должен соответствовать нормативным требованиям, безопасности и эксплуатации, прежде чем его можно будет принять.

Управление удостоверениями и доступом — это многоэтапный процесс, который требует тщательного планирования интеграции удостоверений и других соображений в области безопасности, таких как блокирование устаревших механизмов проверки подлинности и планирование современных паролей. Поэтапное планирование также включает в себя выбор управления удостоверениями и доступом "бизнес-бизнес" и "бизнес-потребитель". Хотя эти требования различаются, существуют общие рекомендации и соображения по проектированию и определения корпоративной целевой зоны.

![Схема: управление удостоверениями и доступ](./media/iam.png)

_Рис. 1. Управление удостоверениями и доступом._

**Рекомендации по проектированию:**

- Существуют ограничения на количество пользовательских ролей и назначений ролей, которые следует учитывать при создании структуры для IAM и системы управления. Дополнительные сведения см. в статье [ограничения службы RBAC Azure](/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-role-based-access-control-limits).
- Существует ограничение в 2 000 назначений ролей на подписку.
- Существует ограничение в 500 назначений ролей для каждой группы управления.
- Централизованное и федеративное владение ресурсами:
  - Управление общими ресурсами и любыми аспектами среды, которые реализуют или применяют граничную безопасность, такими как сеть, должно осуществляться централизованно. Это требование является частью многих платформ соответствия нормативным требованиям. Это стандартная практика любой организации, которая предоставляет или запрещает доступ к конфиденциальным или важным бизнес-ресурсам.
  - Управление ресурсами приложений, которые не нарушают границы безопасности, и другие аспекты, необходимые для обеспечения безопасности и соответствия требованиям, могут быть делегированы группам приложений. Предоставление пользователям возможности подготавливать ресурсы в безопасно управляемой среде позволяет организациям воспользоваться преимуществами гибкой природы облака, не нарушая ни одной критической границы безопасности или управления.

<!-- docutune:ignore Azure-AD-only Azure-AD-managed -->

**Рекомендации по проектированию:**

- Используйте [Azure RBAC](/azure/role-based-access-control/overview) для управления доступом к ресурсам по плоскости данных, где это возможно. Примерами могут быть Azure Key Vault, учетная запись хранения или база данных SQL.
- Развертывайте политики условного доступа Azure AD для любого пользователя с правами в средах Azure. Это предоставляет еще один механизм защиты от несанкционированного доступа к управляемой среде Azure.
- Применяйте многофакторную проверку подлинности для любого пользователя с правами в средах Azure. Применение многофакторной проверки подлинности является обязательным во многих платформах соответствия. Это значительно снижает риск кражи учетных данных и несанкционированного доступа.
- Используйте [Azure AD privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-configure) , чтобы установить нулевой доступ и наименьшую привилегию. Сопоставьте организационные роли с минимальным требуемым уровнем доступа. Служба PIM Azure AD может быть расширением существующих средств и процессов, использовать собственные средства Azure, как описано выше, или использовать их при необходимости.
- Используйте группы, предназначенные только для Azure AD, для ресурсов уровня управления Azure в Azure AD PIM при предоставлении доступа к ресурсам.
  - Добавьте локальные группы в группу, предназначенную только для Azure AD, если система управления группами уже существует.
- Используйте проверки доступа в PIM Azure AD для периодической проверки прав на ресурсы. Проверки доступа являются частью многих платформ соответствия. В результате для решения этой потребности во многих организациях уже будет существовать процесс.
- Интеграция журналов Azure AD с платформой [Azure Monitor](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor). Azure Monitor позволяет иметь единый доверенный источник данных на основе данных журналов и мониторинга в Azure, что дает организациям встроенные возможности облака для соответствия требованиям по сбору и хранению журналов.
- Если существуют требования к независимости данных, для их применения можно развернуть пользовательские политики.
- Используйте пользовательские определения ролей в клиенте Azure AD, пока вы учитываете следующие ключевые роли:

| Роль | Использование | Actions | Нет действий |
|---|---|---|---|
| Владелец платформы Azure (например, роль "встроенный владелец");               | Управление жизненным циклом группы управления и подписки                                                           | `*`                                                                                                                                                                                                                  |                                                                                                                                                                                         |
| Управление сетью (Нетопс)        | Глобальное управление подключением на уровне платформы: виртуальные сети, определяемые пользователем маршруты, группы безопасности сети, NVA, VPN, Azure ExpressRoute и др.            | `*/read`, `Microsoft.Network/vpnGateways/*`, `Microsoft.Network/expressRouteCircuits/*`, `Microsoft.Network/routeTables/write`, `Microsoft.Network/vpnSites/*`                              |                                                                                                                                                                               |
| Операции безопасности (SecOps)       | Роль администратора безопасности с горизонтальным представлением всей области Azure и политики очистки Azure Key Vault | `*/read`, `*/register/action`, `Microsoft.KeyVault/locations/deletedVaults/purge/action`, `Microsoft.Insights/alertRules/*`, `Microsoft.Authorization/policyDefinitions/*`, `Microsoft.Authorization/policyAssignments/*`, `Microsoft.Authorization/policySetDefinitions/*`, `Microsoft.PolicyInsights/*`, `Microsoft.Security/*` |                                                                            |
| Владелец подписки                 | Делегированная роль владельца подписки, полученная от роли владельца подписки                                       | `*`                                                                                                                                                                                                                  | `Microsoft.Authorization/*/write`, `Microsoft.Network/vpnGateways/*`, `Microsoft.Network/expressRouteCircuits/*`, `Microsoft.Network/routeTables/write`, `Microsoft.Network/vpnSites/*` |
| Владельцы приложений (DevOps/Аппопс) | Роль участника, предоставленная группе приложений или операций на уровне группы ресурсов                                 | `*`                                                                                                                                                                                                                   | `Microsoft.Authorization/*/write`, `Microsoft.Network/publicIPAddresses/write`, `Microsoft.Network/virtualNetworks/write`, `Microsoft.KeyVault/locations/deletedVaults/purge/action`                                         |

- Используйте JIT-доступ центра безопасности Azure ко всем ресурсам "инфраструктура как услуга" (IaaS), чтобы обеспечить защиту на уровне сети для временного доступа пользователей к виртуальным машинам IaaS.
- Используйте управляемые удостоверения Azure AD для ресурсов Azure, чтобы предотвратить использование аутентификации на основе имен пользователей и паролей. Так как многие нарушения безопасности в общедоступных облачных ресурсах исходят из-за кражи учетных данных, внедренных в код, или других текстовых источников, применение управляемых удостоверений для программного доступа значительно сокращает риск кражи учетных данных.
- Используйте привилегированные удостоверения для модулей автоматизации Runbook, для которых требуются повышенные права доступа. Автоматизированные рабочие процессы, которые нарушают критические границы безопасности, должны управляться теми же инструментами и политиками, что и пользователи эквивалентных привилегий.
- Не добавляйте пользователей непосредственно в области ресурсов Azure. Вместо этого добавьте пользователей в определенные роли, которые затем назначаются областям ресурсов. Прямые назначения пользователей обходит централизованное управление, значительно повышая уровень управления, необходимый для предотвращения несанкционированного доступа к ограниченным данным.

### <a name="plan-for-authentication-inside-a-landing-zone"></a>Планирование проверки подлинности в целевой зоне

Важное решение по проектированию, которое корпоративная организация должна принять при внедрении Azure, — это необходимость расширения существующего локального домена удостоверений в Azure или создания абсолютно нового домена. Требования к проверке подлинности в целевой зоне должны быть тщательно оценены и включены в планы развертывания доменных служб Active Directory (AD DS) в Windows Server, доменных службах Azure AD (Azure AD DS) или обеих служб. Большинство сред Azure используют, по крайней мере, Azure AD для аутентификации в структуре Azure и проверку подлинности на локальном узле и управление групповыми политиками AD DS.

**Рекомендации по проектированию:**

- Для управления ресурсами, развернутыми в целевой зоне, рекомендуется использовать централизованные и делегированные обязанности.
- Приложения, использующие доменные службы и использующие старые протоколы, могут использовать [AD DS Azure](/azure/active-directory-domain-services).

**Рекомендации по проектированию:**

- Используйте централизованные и делегированные обязанности для управления ресурсами, развернутыми в целевой зоне, на основе требований к ролям и безопасности.
- Для привилегированных операций, таких как создание объектов субъекта-службы, регистрация приложений в Azure AD, приобретение и обработка сертификатов или групповых сертификатов, требуются специальные разрешения. Определите, какие пользователи будут обрабатывать такие запросы, а также как защитить и отслеживать их учетные записи с необходимой степенью контроля.
- Если в Организации есть сценарий, в котором приложение, использующее встроенную проверку подлинности Windows, должно быть доступно удаленно через Azure AD, попробуйте использовать [azure AD application proxy](/azure/active-directory/manage-apps/application-proxy).
- Существует разница между Azure AD, Azure AD DS и AD DS, работающими в Windows Server. Оцените потребности приложений, а также выясните и задокументируйте поставщика проверки подлинности, который будет использоваться каждым из них. Выполняйте соответствующее планирование для всех приложений.
- Оцените совместимость рабочих нагрузок для AD DS в Windows Server и Azure AD DS.
- Убедитесь, что структура сети позволяет ресурсам, требующим AD DS на Windows Server, выполнять локальную аутентификацию и управление для доступа к соответствующим контроллерам домена.
  - Для AD DS в Windows Server рассмотрите среды общих служб, которые обеспечивают локальную проверку подлинности и управление узлом в более крупном контексте сети корпоративного уровня.
- Разверните Azure AD DS в основном регионе, так как эту службу можно проецировать только в одну подписку.
- Используйте управляемые удостоверения вместо субъектов-служб для проверки подлинности в службах Azure. Такой подход снижает вероятность кражи учетных данных.
