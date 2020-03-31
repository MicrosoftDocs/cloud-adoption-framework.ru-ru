---
title: Управление доступом к ресурсам в Azure
description: Основные сведения об управлении доступом к ресурсам Azure, такие как Azure Resource Manager, подписки, группы ресурсов и ресурсы.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fe478b76aa44da56620517ea0df4cea7357ea23b
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2020
ms.locfileid: "80435006"
---
# <a name="resource-access-management-in-azure"></a>Управление доступом к ресурсам в Azure

[Cloud](../index.md) Management описывает пять дисциплин управления облаком, включая управление ресурсами. Статья [CAF. Общие сведения о дисциплине "Согласованность ресурсов"](./index.md) объясняет, как управление доступом к ресурсам вписывается в дисциплину управления ресурсами. Прежде чем переходить к изучению принципов проектирования модели системы управления, важно разобраться с элементами управления доступом к ресурсам в Azure. Конфигурация этих элементов управления доступом к ресурсами — это основа модели системы управления.

Давайте рассмотрим принцип развертывания ресурсов в Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Ресурсы Azure

В Azure _ресурс_ — это сущность под управлением Azure. Например, к ресурсам относятся виртуальные машины, виртуальные сети и учетные записи хранения.

Схема ![ресурса](../../_images/govern/design/governance-1-9.png)
*рис. 1. ресурс.*

## <a name="what-is-an-azure-resource-group"></a>Что такое группа ресурсов Azure?

Каждый ресурс в Azure должен принадлежать [группе ресурсов](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Группа ресурсов — это просто логическая конструкция, которая группирует несколько ресурсов вместе, чтобы ими можно было управлять как единой сущностью _на основе жизненного цикла и безопасности_. Например, ресурсы с аналогичным жизненным циклом, например ресурсы [n-уровневых приложений](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), можно создавать или удалять как группу. Другой способ: все, что порождено вместе, управляется вместе и является устаревшим, объединяется в группе ресурсов.

![диаграмма группы ресурсов, содержащей ресурс](../../_images/govern/design/governance-1-10.png)
*рис. 2. Группа ресурсов содержит ресурс.*

Группы и ресурсы в них связаны с **подпиской** Azure.

## <a name="what-is-an-azure-subscription"></a>Подписка Azure

Подписка Azure, как и группа ресурсов, — это логическая конструкция, в которой сгруппированы группы и ресурсы в них. Тем не менее подписка Azure также связана с элементами управления, используемыми Azure Resource Manager. Рассмотрим более подробно Azure Resource Manager, чтобы больше узнать о связи между ним и подпиской Azure.

![схеме подписки Azure](../../_images/govern/design/governance-1-11.png)
*рис. 3. Подписка Azure.*

## <a name="what-is-azure-resource-manager"></a>Azure Resource Manager

Из статьи [Пояснения. Принцип работы Azure](../../getting-started/what-is-azure.md) вы узнали, что Azure включает внешний интерфейс со многими службами, которые оркестрируют работу всех функции Azure. К этим службам относится [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager). В этой службе размещен интерфейс REST API, с помощью которого клиенты управляют ресурсами.

![схема Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
*рис. 4 — Azure Resource Manager.*

На следующем рисунке показаны три клиента: [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [портал Azure](https://portal.azure.com)и [Azure CLI](https://docs.microsoft.com/cli/azure).

![схеме клиентов Azure, подключающихся к API Azure Resource Manager](../../_images/govern/design/governance-1-13.png)
*рис. 5. клиенты Azure подключаются к api Azure Resource Manager RESTful.*

Эти клиенты подключаются к Azure Resource Manager через RESTful API. Однако Azure Resource Manager не содержит функциональность, чтобы управлять ресурсами напрямую. Скорее, большинство типов ресурсов в Azure имеют собственный [поставщик ресурсов](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#terminology).

![поставщиков ресурсов Azure](../../_images/govern/design/governance-1-14.png)
*рис. 6. поставщики ресурсов Azure.*

Когда клиент отправляет запрос на управление определенным ресурсом, Azure Resource Manager подключается к поставщику ресурсов этого типа ресурса, чтобы выполнить запрос. Например, если клиент отправляет запрос на управление ресурсами виртуальной машины, Azure Resource Manager подключается к поставщику ресурсов **Microsoft.compute**.

![Azure Resource Manager подключении к поставщику ресурсов Microsoft. COMPUTE](../../_images/govern/design/governance-1-15.png)
*рис. 7 — Azure Resource Manager подключается к поставщику ресурсов **Microsoft. COMPUTE** для управления ресурсом, указанным в запросе клиента.*

Azure Resource Manager требует, чтобы клиент указал идентификатор подписки и группы ресурсов и тем самым разрешил управлять ресурсами виртуальной машины.

Теперь, когда вы имеете представление о принципе работы Azure Resource Manager, рассмотрим, как используемые этой службой элементы управления связаны с подпиской Azure. Перед выполнением Azure Resource Manager любого запроса на управление ресурсом проверяется набор элементов управления.

Сначала проверяется, выполняется ли запрос проверенным пользователем. Azure Resource Manager имеет отношения доверия с [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory), что позволяет обеспечить механизм удостоверения пользователя.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
*рис. 8 — Azure Active Directory.*

В Azure AD данные пользователей сегментируются по **клиентам**. Клиент — это логическая структура, представляющая собой защищенный выделенный экземпляр Azure AD, который, как правило, связан с организацией. Каждая подписка связана с клиентом Azure AD.

![клиент Azure AD, связанный с подпиской](../../_images/govern/design/governance-1-17.png)
*рис. 9 — клиент Azure AD, связанный с подпиской.*

Каждый запрос клиента на управление ресурсом в определенной подписке требует наличия у пользователя учетной записи в связанном клиенте Azure AD.

Следующим проверяется, имеет ли пользователь необходимые права на выполнение запроса. Разрешения присваиваются пользователям с использованием механизма [управления доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![пользователей, назначенных ролям RBAC](../../_images/govern/design/governance-1-18.png)
*рис. 10. Каждому пользователю в клиенте назначается одна или несколько ролей RBAC.*

Роль RBAC указывает набор разрешений, которые пользователь имеет в определенном ресурсе. Эти разрешения применяются после назначения роли пользователю. Например, пользователь со [встроенной ролью **владельца**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) может выполнять любые действия в ресурсе.

На следующем этапе проверяется, разрешен ли запрос согласно параметрам, заданным в [политике ресурсов Azure](https://docs.microsoft.com/azure/governance/policy). Политики ресурсов Azure указывают операции, разрешенные в конкретном ресурсе. Например, в соответствии с политикой ресурсов Azure пользователи смогут развертывать только определенные типы виртуальной машины.

![политики ресурсов Azure](../../_images/govern/design/governance-1-19.png)
*рис. 11. Политика ресурсов Azure.*

На следующем этапе проверяется, не превышает ли запрос [ограничения подписки Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits). Например, каждая подписка может максимально содержать 980 групп ресурсов. Если получен запрос на развертывание дополнительной группы ресурсов по достижении предела, он отклоняется.

ограничения ресурсов Azure ![](../../_images/govern/design/governance-1-20.png)
*рис. 12. Ограничения ресурсов Azure.*

В последнюю очередь проверяется, связан ли запрос в рамках финансовых обязательств с подпиской. Например, если отправляется запрос на развертывание виртуальной машины, Azure Resource Manager проверяет платежную информацию в подписке.

![финансовые обязательства, связанные с подпиской](../../_images/govern/design/governance-1-21.png)
*рис. 13. С подпиской связано финансовое обязательство.*

## <a name="summary"></a>Сводка

Из этой статьи вы узнали об управлении доступом к ресурсам в Azure с помощью Azure Resource Manager.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали об управлении доступом к ресурсам в Azure, узнайте о том, как разработать модель управления [для простой рабочей нагрузки](./governance-simple-workload.md) или [для нескольких команд](./governance-multiple-teams.md).

> [!div class="nextstepaction"]
> [Общие сведения о системе управления](../index.md)
