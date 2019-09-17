---
title: Управление доступом к ресурсам в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Основные сведения о средствах управления доступом к ресурсам в Azure Диспетчер ресурсов Azure, подписки, группы ресурсов и ресурсы
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 46c6de1ecaba5b8278138114b6aa27a2608bfb74
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031091"
---
# <a name="resource-access-management-in-azure"></a>Управление доступом к ресурсам в Azure

[Cloud](../index.md) Management описывает пять дисциплин управления облаком, включая управление ресурсами. Статья [CAF. Общие сведения о дисциплине "Согласованность ресурсов"](./index.md) объясняет, как управление доступом к ресурсам вписывается в дисциплину управления ресурсами. Прежде чем переходить к изучению принципов проектирования модели системы управления, важно разобраться с элементами управления доступом к ресурсам в Azure. Конфигурация этих элементов управления доступом к ресурсами — это основа модели системы управления.

Давайте рассмотрим принцип развертывания ресурсов в Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Ресурсы Azure

В Azure _ресурс_ — это сущность под управлением Azure. Например, к ресурсам относятся виртуальные машины, виртуальные сети и учетные записи хранения.

![Схема ресурса](../../_images/govern/design/governance-1-9.png)
,*рис. 1. ресурс.*

## <a name="what-is-an-azure-resource-group"></a>Что такое группа ресурсов Azure?

Каждый ресурс в Azure должен принадлежать [группе ресурсов](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Группа ресурсов — это логическая конструкция, в которой сгруппированы несколько ресурсов, что позволяет управлять ими как единой сущностью. Например, ресурсы с аналогичным жизненным циклом, например ресурсы [n-уровневых приложений](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), можно создавать или удалять как группу.

![Схема группы ресурсов, содержащей ресурс](../../_images/govern/design/governance-1-10.png)
*рис. 2. Группа ресурсов содержит ресурс.*

Группы и ресурсы в них связаны с **подпиской** Azure.

## <a name="what-is-an-azure-subscription"></a>Подписка Azure

Подписка Azure, как и группа ресурсов, — это логическая конструкция, в которой сгруппированы группы и ресурсы в них. Тем не менее подписка Azure также связана с элементами управления, используемыми Azure Resource Manager. Что это означает? Рассмотрим более подробно Azure Resource Manager, чтобы больше узнать о связи между ним и подпиской Azure.

![Схема подписки](../../_images/govern/design/governance-1-11.png)
Azure*рис. 3. Подписка Azure.*

## <a name="what-is-azure-resource-manager"></a>Azure Resource Manager

Из статьи [Пояснения. Принцип работы Azure](../../getting-started/what-is-azure.md) вы узнали, что Azure включает внешний интерфейс со многими службами, которые оркестрируют работу всех функции Azure. К этим службам относится [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager). В этой службе размещен интерфейс REST API, с помощью которого клиенты управляют ресурсами.

![Схема Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
*рис. 4. Azure Resource Manager.*

На следующем рисунке показано три клиента: [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [портал Azure](https://portal.azure.com)и [Azure CLI](https://docs.microsoft.com/cli/azure):

![Схема клиентов Azure, подключающихся к API](../../_images/govern/design/governance-1-13.png)
Azure Resource Manager*рис. 5. клиенты Azure подключаются к API-интерфейсу RESTful Azure Resource Manager.*

Эти клиенты подключаются к Azure Resource Manager через RESTful API. Однако Azure Resource Manager не содержит функциональность, чтобы управлять ресурсами напрямую. Вместо этого большинство типов ресурсов в Azure имеют собственный [**поставщик ресурсов**](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#terminology).

![Поставщики](../../_images/govern/design/governance-1-14.png)
ресурсов Azure*рис. 6. поставщики ресурсов Azure.*

Когда клиент отправляет запрос на управление определенным ресурсом, Azure Resource Manager подключается к поставщику ресурсов этого типа ресурса, чтобы выполнить запрос. Например, если клиент отправляет запрос на управление ресурсами виртуальной машины, Azure Resource Manager подключается к поставщику ресурсов **Microsoft.compute**.

![Azure Resource Manager подключении к поставщику](../../_images/govern/design/governance-1-15.png)
ресурсов Microsoft. COMPUTE рис. 7.*Azure Resource Manager подключается к поставщику ресурсов **Microsoft. COMPUTE** для управления ресурсом, указанным в запросе клиента.*

Azure Resource Manager требует, чтобы клиент указал идентификатор подписки и группы ресурсов и тем самым разрешил управлять ресурсами виртуальной машины.

Теперь, когда вы имеете представление о принципе работы Azure Resource Manager, рассмотрим, как используемые этой службой элементы управления связаны с подпиской Azure. Перед выполнением Azure Resource Manager любого запроса на управление ресурсом проверяется набор элементов управления.

Сначала проверяется, выполняется ли запрос проверенным пользователем. Azure Resource Manager имеет отношения доверия с [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory), что позволяет обеспечить механизм удостоверения пользователя.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
*рис. 8. Azure Active Directory.*

В Azure AD данные пользователей сегментируются по **клиентам**. Клиент — это логическая структура, представляющая собой защищенный выделенный экземпляр Azure AD, который, как правило, связан с организацией. Каждая подписка связана с клиентом Azure AD.

![Клиент Azure AD, связанный с подпиской](../../_images/govern/design/governance-1-17.png)
на*рис. 9 — клиент Azure AD, связанный с подпиской.*

Каждый запрос клиента на управление ресурсом в определенной подписке требует наличия у пользователя учетной записи в связанном клиенте Azure AD.

Следующим проверяется, имеет ли пользователь необходимые права на выполнение запроса. Разрешения присваиваются пользователям с использованием механизма [управления доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![Пользователи, назначенные ролям RBAC](../../_images/govern/design/governance-1-18.png)
*Рис. 10. Каждому пользователю в клиенте назначается одна или несколько ролей RBAC.*

Роль RBAC указывает набор разрешений, которые пользователь имеет в определенном ресурсе. Эти разрешения применяются после назначения роли пользователю. Например, пользователь со [встроенной ролью **владельца**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) может выполнять любые действия в ресурсе.

На следующем этапе проверяется, разрешен ли запрос согласно параметрам, заданным в [политике ресурсов Azure](https://docs.microsoft.com/azure/governance/policy). Политики ресурсов Azure указывают операции, разрешенные в конкретном ресурсе. Например, в соответствии с политикой ресурсов Azure пользователи смогут развертывать только определенные типы виртуальной машины.

![Политика ресурсов Azure](../../_images/govern/design/governance-1-19.png)
*Рис. 11. Политика ресурсов Azure.*

На следующем этапе проверяется, не превышает ли запрос [ограничения подписки Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits). Например, каждая подписка может максимально содержать 980 групп ресурсов. Если получен запрос на развертывание дополнительной группы ресурсов после превышения этого ограничения, такой запрос будет отклонен.

![Ограничения ресурсов Azure](../../_images/govern/design/governance-1-20.png)
*Рис. 12. Ограничения ресурсов Azure.*

В последнюю очередь проверяется, связан ли запрос в рамках финансовых обязательств с подпиской. Например, если отправляется запрос на развертывание виртуальной машины, Azure Resource Manager проверяет платежную информацию в подписке.

![Финансовое обязательство, связанное с подпиской](../../_images/govern/design/governance-1-21.png)
*Рис. 13. Финансовое обязательство, связанное с подпиской.*

## <a name="summary"></a>Сводка

Из этой статьи вы узнали об управлении доступом к ресурсам в Azure с помощью Azure Resource Manager.

## <a name="next-steps"></a>Следующие шаги

Теперь, когда вы узнали об управлении доступом к ресурсам в Azure, узнайте о том, как разработать модель управления [для простой рабочей нагрузки](./governance-simple-workload.md) или [для нескольких команд](./governance-multiple-teams.md).

> [!div class="nextstepaction"]
> [Общие сведения о системе управления](../index.md)
