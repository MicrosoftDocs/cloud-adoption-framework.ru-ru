---
title: Управление доступом к ресурсам в Azure
description: Основные сведения об управлении доступом к ресурсам Azure, такие как Azure Resource Manager, подписки, группы ресурсов и ресурсы.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: 2924bbf984a8ed570f4d139f4a0a3b0ccf28a1e6
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102115464"
---
# <a name="resource-access-management-in-azure"></a>Управление доступом к ресурсам в Azure

В этой [методологии](../index.md) описываются пять дисциплин управления облаком, в том числе управление ресурсами. Статья [CAF. Общие сведения о дисциплине "Согласованность ресурсов"](./index.md) объясняет, как управление доступом к ресурсам вписывается в дисциплину управления ресурсами. Прежде чем переходить к изучению принципов проектирования модели системы управления, важно разобраться с элементами управления доступом к ресурсам в Azure. Конфигурация этих элементов управления доступом к ресурсами — это основа модели системы управления.

Давайте рассмотрим принцип развертывания ресурсов в Azure.

## <a name="what-is-an-azure-resource"></a>Что собой представляет ресурс Azure

В Azure *ресурс* — это сущность под управлением Azure. Например, к ресурсам относятся виртуальные машины, виртуальные сети и учетные записи хранения.

![Схема ресурса ](../../_images/govern/design/governance-1-9.png)
 *рис. 1. ресурс.*

## <a name="what-is-an-azure-resource-group"></a>Что такое группа ресурсов Azure?

Каждый ресурс в Azure должен принадлежать [группе ресурсов](/azure/azure-resource-manager/management/overview#resource-groups). Группа ресурсов — это просто логическая конструкция, которая группирует несколько ресурсов вместе, чтобы ими можно было управлять как единой сущностью **на основе жизненного цикла и безопасности**. Например, ресурсы с аналогичным жизненным циклом, например ресурсы [n-уровневых приложений](/azure/architecture/guide/architecture-styles/n-tier), можно создавать или удалять как группу. Другими словами, все, что порождено вместе, управляется вместе и является более устаревшим, объединяется в группе ресурсов.

![Схема группы ресурсов, содержащей ресурс ](../../_images/govern/design/governance-1-10.png)
 *рис. 2. Группа ресурсов содержит ресурс.*

Группы и ресурсы в них связаны с подпиской Azure.

## <a name="what-is-an-azure-subscription"></a>Подписка Azure

*Подписка* Azure аналогична группе ресурсов в том, что это логическая конструкция, объединяющая группы ресурсов и их ресурсы. Подписка Azure также связывается с элементами управления, используемыми Azure Resource Manager. Рассмотрим более подробно Azure Resource Manager, чтобы больше узнать о связи между ним и подпиской Azure.

![Схема подписки Azure ](../../_images/govern/design/governance-1-11.png)
 *рис. 3. Подписка Azure.*

## <a name="what-is-azure-resource-manager"></a>Azure Resource Manager

[Как работает Azure?](../../get-started/what-is-azure.md) вы узнали, что Azure включает внешний интерфейс со многими службами, координирующими все функции Azure. К этим службам относится [Azure Resource Manager](/azure/azure-resource-manager/). В этой службе размещен интерфейс REST API, с помощью которого клиенты управляют ресурсами.

![Схема Azure Resource Manager ](../../_images/govern/design/governance-1-12.png)
 *рис. 4. Azure Resource Manager.*

На следующем рисунке показаны три клиента: [PowerShell](/powershell/azure/), [портал Azure](https://portal.azure.com)и [Azure CLI](/cli/azure/).

![Схема клиентов Azure, подключающихся к диспетчер ресурсов REST API ](../../_images/govern/design/governance-1-13.png)
 *рис. 5. клиенты Azure подключаются к REST API диспетчер ресурсов.*

Хотя эти клиенты подключаются к диспетчер ресурсов с помощью REST API, диспетчер ресурсов не включает функции для непосредственного управления ресурсами. Вместо этого большинство типов ресурсов в Azure имеют собственный [поставщик ресурсов](/azure/azure-resource-manager/management/overview#terminology).

![Поставщики ресурсов Azure ](../../_images/govern/design/governance-1-14.png)
 *рис. 6. поставщики ресурсов Azure.*

Когда клиент отправляет запрос на управление определенным ресурсом, Azure Resource Manager подключается к поставщику ресурсов этого типа ресурса, чтобы выполнить запрос. Например, если клиент выполняет запрос на управление ресурсом виртуальной машины, Azure Resource Manager подключается к `Microsoft.Compute` поставщику ресурсов.

![Azure Resource Manager подключении к поставщику ресурсов Microsoft. COMPUTE ](../../_images/govern/design/governance-1-15.png)
 *рис. 7. Azure Resource Manager подключается к `Microsoft.Compute` поставщику ресурсов для управления ресурсом, указанным в запросе клиента.*

Azure Resource Manager требует, чтобы клиент указал идентификатор подписки и группы ресурсов и тем самым разрешил управлять ресурсами виртуальной машины.

Теперь, когда вы имеете представление о принципе работы Azure Resource Manager, рассмотрим, как используемые этой службой элементы управления связаны с подпиской Azure. Перед выполнением Azure Resource Manager любого запроса на управление ресурсом проверяется набор элементов управления.

Сначала проверяется, выполняется ли запрос проверенным пользователем. Azure Resource Manager имеет отношения доверия с [Azure Active Directory (Azure AD)](/azure/active-directory/), что позволяет обеспечить механизм удостоверения пользователя.

![Azure Active Directory ](../../_images/govern/design/governance-1-16.png)
 *рис. 8. Azure Active Directory.*

В Azure AD данные пользователей сегментируются по клиентам. *Клиент* — это логическая конструкция, которая представляет защищенный выделенный экземпляр Azure AD, обычно связанный с Организацией. Каждая подписка связана с клиентом Azure AD.

![Клиент Azure AD, связанный с подпиской ](../../_images/govern/design/governance-1-17.png)
 *рис. 9. Клиент Azure AD, связанный с подпиской.*

Каждый запрос клиента на управление ресурсом в определенной подписке требует наличия у пользователя учетной записи в связанном клиенте Azure AD.

Следующим проверяется, имеет ли пользователь необходимые права на выполнение запроса. Разрешения назначаются пользователям с помощью [управления доступом на основе ролей Azure (Azure RBAC)](/azure/role-based-access-control/).

![Пользователи, назначенные ролям Azure ](../../_images/govern/design/governance-1-18.png)
 *рис. 10. каждому пользователю в клиенте назначается одна или несколько ролей Azure.*

Роль Azure указывает набор разрешений, которые может выполнять пользователь на определенном ресурсе. Эти разрешения применяются после назначения роли пользователю. Например, [Встроенная `owner` роль](/azure/role-based-access-control/built-in-roles#owner) позволяет пользователю выполнять любые действия с ресурсом.

На следующем этапе проверяется, разрешен ли запрос согласно параметрам, заданным в [политике ресурсов Azure](/azure/governance/policy/). Политики ресурсов Azure указывают операции, разрешенные в конкретном ресурсе. Например, в соответствии с политикой ресурсов Azure пользователи смогут развертывать только определенные типы виртуальной машины.

![Политика ресурсов Azure ](../../_images/govern/design/governance-1-19.png)
 *рис. 11. Политика ресурсов Azure.*

На следующем этапе проверяется, не превышает ли запрос [ограничения подписки Azure](/azure/azure-resource-manager/management/azure-subscription-service-limits). Например, каждая подписка может максимально содержать 980 групп ресурсов. Если получен запрос на развертывание дополнительной группы ресурсов по достижении предела, он отклоняется.

![Ограничения ресурсов Azure ](../../_images/govern/design/governance-1-20.png)
 *рис. 12. ограничения ресурсов Azure.*

В последнюю очередь проверяется, связан ли запрос в рамках финансовых обязательств с подпиской. Например, если отправляется запрос на развертывание виртуальной машины, Azure Resource Manager проверяет платежную информацию в подписке.

![Финансовые обязательства, связанные с подпиской на ](../../_images/govern/design/governance-1-21.png)
 *рис. 13. финансовое обязательство связано с подпиской.*

## <a name="summary"></a>Итоги

Из этой статьи вы узнали об управлении доступом к ресурсам в Azure с помощью Azure Resource Manager.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали об управлении доступом к ресурсам в Azure, узнайте о том, как разработать модель управления [для простой рабочей нагрузки](./governance-simple-workload.md) или [для нескольких команд](./governance-multiple-teams.md).

> [!div class="nextstepaction"]
> [Общие сведения о системе управления](../index.md)
