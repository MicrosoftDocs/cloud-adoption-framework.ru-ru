---
title: Управление экземпляром Azure в центре обработки данных
description: Узнайте, как управлять экземпляром Azure, работающим на Azure Stack концентраторе данных.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: 885278cb4ebf0faaf5686a16687bef7ccd7fe684
ms.sourcegitcommit: a0ddde4afcc7d8c21559e79d406dc439ee4f38d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2020
ms.locfileid: "97713816"
---
# <a name="govern-an-azure-instance-in-your-datacenter"></a>Управление экземпляром Azure в центре обработки данных

Управление гибридными решениями на платформах общедоступных и частных облаков повышает сложность. Так как развертывание центра Azure Stack — это собственный частный экземпляр Azure, работающий в вашем центре обработки данных, эта сложность по своей природе снижается.

Бизнес-процессы, дисциплины и многие рекомендации, описанные в статье Управление [методологией](../../govern/index.md) облачной инфраструктуры внедрения, по-прежнему можно применять к гибридным системам управления с помощью центра Azure Stack. Многие собственные средства облака, используемые в общедоступной облачной версии Azure, также можно использовать в развертывании центра Azure Stack.

## <a name="azure-stack-hub-governance-considerations"></a>Рекомендации по управлению центром Azure Stack

В следующей серии блогов показано, как ваша организация может реализовать концепции управления облаком для центра Azure Stack:

- [Службы Организации](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven/) , такие как группы ресурсов, управление доступом на основе ролей Azure (Azure RBAC), аудит изменений, блокировки и теги.
- [Службы безопасности](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/), включая брандмауэры по умолчанию, ограничения, обновления ВМ и управление исправлениями, а также состояние вредоносных программ.
- [DevOps параметры](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven-2/), включая инфраструктуру как код, портал с PowerShell и интерфейсом командной строки, Azure Application Insights и интеграцию с Azure DevOps и Jenkins.

## <a name="governance-toolchain-for-azure-stack-hub"></a>Управление цепочки инструментов для центра Azure Stack

Рекомендации по применению собственных средств управления в облаке для Azure Stack центральных средах см. в следующих статьях:

- [Azure Resource Manager шаблоны и настройка требуемого состояния](/azure-stack/user/azure-stack-arm-templates?view=azs-2002)
- [PowerShell](/azure-stack/user/azure-stack-powershell-overview?view=azs-2002)
- [Политика Azure](/azure-stack/user/azure-stack-policy-module?view=azs-2002)
- [Управление доступом на основе ролей в Azure](/azure-stack/user/azure-stack-manage-permissions?view=azs-2002)

## <a name="next-steps"></a>Дальнейшие действия

Рекомендации по конкретным элементам процесса внедрения облачных технологий см. в следующих статьях:

- [Управление Azure Stack Hub](./manage.md)
