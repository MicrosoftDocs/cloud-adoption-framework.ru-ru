---
title: Основные понятия Azure
description: Используйте платформу внедрения облачных решений Azure для изучения фундаментальных концепций и терминов, используемых в Azure, а также принципов связи друг с другом.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: internal
ms.openlocfilehash: 378836786bf0d35f26dccbbf25b59fb4f02332f6
ms.sourcegitcommit: a0ddde4afcc7d8c21559e79d406dc439ee4f38d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2020
ms.locfileid: "97713409"
---
# <a name="azure-fundamental-concepts"></a>Основные понятия Azure

Изучите основные понятия и термины, используемые в Azure, и узнайте, как эти понятия связаны друг с другом.

## <a name="azure-terminology"></a>Терминология Azure

Начиная работу по внедрению облачных технологий Azure, полезно знать следующие определения:

- **Ресурс:** Сущность, управляемая Azure. Примеры включают виртуальные машины Azure, виртуальные сети и учетные записи хранения.
- **Подписка:** Логический контейнер для ресурсов. Каждый ресурс Azure связан только с одной подпиской. Создание подписки является первым шагом при внедрении Azure.
- **Учетная запись Azure:** Адрес электронной почты, который вы задаете при создании подписки Azure, — это учетная запись Azure для подписки. Сторона, связанная с учетной записью электронной почты, отвечает за ежемесячные расходы, связанные с ресурсами в подписке. При создании учетной записи Azure вы предоставляете контактные данные и сведения о выставлении счетов, например кредитную карту. Для нескольких подписок можно использовать одну и ту же учетную запись Azure (адрес электронной почты). Каждая подписка связана только с одной учетной записью Azure.
- **Администратор учетной записи:** Сторона, связанная с адресом электронной почты, который используется для создания подписки Azure. Администратор учетной записи несет ответственность за оплату за все расходы, которые связаны с ресурсами подписки.
- **Azure Active Directory (Azure AD):** Облачная служба управления удостоверениями и доступом Майкрософт. Azure AD помогает сотрудникам входить в систему и получать доступ к ресурсам:
- **Клиент Azure AD:** Выделенный и доверенный экземпляр Azure AD. Клиент Azure AD создается автоматически, когда ваша организация сначала регистрирует подписку на облачную службу Майкрософт, например Microsoft Azure, Intune или Microsoft 365. Клиент Azure представляет одну организацию.
- **Каталог Azure AD:** Каждый клиент Azure AD имеет один выделенный и доверенный каталог. Каталог включает пользователей, группы и приложения клиента. Каталог используется для выполнения функций идентификации и управления доступом к ресурсам клиента. Каталог может быть связан с несколькими подписками, но каждая подписка связана только с одним каталогом.
- **Группы ресурсов:** Логические контейнеры, используемые для группировки связанных ресурсов в подписке. Каждый ресурс может существовать только в одной группе ресурсов. Группы ресурсов обеспечивают более детализированное группирование в рамках подписки и обычно используются для представления коллекции ресурсов, необходимых для поддержки рабочей нагрузки, приложения или конкретной функции в рамках подписки.
- **Группы управления:** Логические контейнеры, используемые для одной или нескольких подписок. Можно определить иерархию групп управления, подписок, групп ресурсов и ресурсов для эффективного управления доступом, политиками и соответствием с помощью наследования.
- **Регион:** Набор центров обработки данных Azure, развернутых в пределах периметра, определяемого заданной задержкой. Центры обработки данных подключены через выделенную, региональную сеть с низкой задержкой. Большинство ресурсов Azure выполняются в определенном регионе Azure.

## <a name="azure-subscription-purposes"></a>Цели подписки Azure

Подписка Azure служит для нескольких целей. Подписка Azure — это:

- **Юридическое соглашение.** Каждая подписка связана с [предложением Azure](https://azure.microsoft.com/support/legal/offer-details), например бесплатной пробной версией или оплатой по мере использования. Каждое предложение имеет определенные тарифные планы, преимущества и связанные условия. При создании подписки вы выбираете предложение Azure.
- **Соглашение об оплате.** При создании подписки вы предоставляете сведения о платеже для этой подписки, такие как номер кредитной карты. Каждый месяц затраты, понесенные ресурсами, развернутыми в этой подписке, рассчитываются и оплачиваются с помощью этого метода оплаты.
- **Граница шкалы.** Ограничения масштабирования определяются для подписки. Ресурсы подписки не могут превышать установленные ограничения шкалы. Например, существует ограничение на количество виртуальных машин, которые можно создать в одной подписке.
- **Административная граница.** Подписка может действовать в качестве границы для администрирования, безопасности и политики. Azure также предоставляет другие механизмы для удовлетворения этих потребностей, таких как группы управления, группы ресурсов и управление доступом на основе ролей в Azure.

## <a name="azure-subscription-considerations"></a>Рекомендации по подписке Azure

При создании подписки Azure делаются несколько ключевых вариантов подписки:

- **Кто отвечает за оплату подписки?** Сторона, связанная с адресом электронной почты, который вы задаете при создании подписки по умолчанию, является администратором учетной записи подписки. Сторона, связанная с этим адресом электронной почты, отвечает за оплату за все расходы, связанные с ресурсами подписки.
- **Какое предложение Azure мне интересно?** Каждая подписка связана с определенным предложением [Azure](https://azure.microsoft.com/support/legal/offer-details). Вы можете выбрать предложение Azure, которое наилучшим образом соответствует вашим потребностям. Например, если вы планируете использовать подписку для выполнения непроизводственных рабочих нагрузок, вы можете выбрать разработка и тестирование с оплатой по мере использования предложение или Enterprise — разработка и тестирование предложение.

> [!NOTE]
> При регистрации в Azure отображается фраза _создание учетной записи Azure_. Учетная запись Azure создается при создании подписки Azure и связывании подписки с учетной записью электронной почты.

## <a name="azure-administrative-roles"></a>Административные роли Azure

Azure определяет три типа ролей для администрирования подписок, удостоверений и ресурсов:

- Роли классического администратора подписки
- Роли Azure
- Роли Azure Active Directory (Azure AD)

Роль администратора учетной записи для подписки Azure назначается учетной записью электронной почты. Администратор учетной записи является полноправным владельцем подписки. Администратор учетной записи может [управлять администраторами подписки](/azure/cost-management-billing/manage/add-change-subscription-administrator) с помощью портал Azure.

По умолчанию роль администратора службы для подписки также назначается учетной записи электронной почты, используемой для создания подписки Azure. Администратор служб имеет разрешения на доступ к подписке, эквивалентной роли владельца Azure на основе RBAC. Администратор службы также имеет полный доступ к портал Azure. Администратор учетной записи может изменить администратора службы на другую учетную запись электронной почты.

При создании подписки Azure ее можно связать с существующим клиентом Azure AD. В противном случае будет создан новый клиент Azure AD со связанным каталогом. Роль глобального администратора в каталоге Azure AD назначается учетной записи электронной почты, используемой для создания подписки Azure AD.

Учетная запись Azure может быть связана с несколькими подписками. Администратор учетной записи может перенести подписку на другую учетную запись.

Подробное описание ролей, определенных в Azure, см. в разделе [роли администратора классической подписки, роли Azure и роли Azure AD](/azure/role-based-access-control/rbac-and-directory-admin-roles).

## <a name="subscriptions-and-regions"></a>Подписки и регионы

Каждый ресурс Azure логически связан только с одной подпиской. При создании ресурса необходимо выбирать, на какую подписку Azure будет развернут этот ресурс. Позже можно переместить ресурс в другую подписку.

Хотя подписка не привязана к определенному региону Azure, каждый ресурс Azure развертывается только в одном регионе. Ресурсы могут находиться в нескольких регионах, связанных с одной подпиской.

> [!NOTE]
> Большинство ресурсов Azure развертываются в только определенном регионе. Некоторые типы ресурсов считаются глобальными ресурсами, такими как политики, заданные с помощью служб политик Azure.

## <a name="related-resources"></a>Связанные ресурсы

Следующие ресурсы предоставляют подробную информацию о понятиях, обсуждаемых в этой статье:

- [Принцип работы Azure](../../get-started/what-is-azure.md)
- [Управление доступом к ресурсам в Azure](../../govern/resource-consistency/resource-access-management.md)
- [Общие сведения об Azure Resource Manager](/azure/azure-resource-manager/management/overview)
- [Управление доступом Azure на основе ролей (Azure RBAC)](/azure/role-based-access-control/overview)
- [Что такое Azure Active Directory?](/azure/active-directory/fundamentals/active-directory-whatis)
- [Associate or add an Azure subscription to your Azure Active Directory tenant](/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory) (Связывание или добавление подписки Azure в клиент Azure Active Directory)
- [Топологии для Azure AD Connect](/azure/active-directory/hybrid/plan-connect-topologies)
- [Подписки, лицензии, учетные записи и клиенты для облачных предложений Майкрософт](/office365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings)

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы принимаете фундаментальные концепции Azure, узнайте, как масштабировать с несколькими подписками Azure.

> [!div class="nextstepaction"]
> [Масштабирование с несколькими подписками Azure](../azure-best-practices/scale-subscriptions.md)
