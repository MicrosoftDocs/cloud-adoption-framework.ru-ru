---
title: Управление работой Azure в вашем центре обработки данных
description: Узнайте, как управлять работой Azure в центре обработки данных Azure Stack.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: c9f8a2f161571ced20f3a9317469cee14cc35fb1
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452111"
---
# <a name="govern-azure-running-in-your-datacenter"></a>Управление работой Azure в вашем центре обработки данных

Управление гибридными решениями на платформах общедоступных и частных облаков повышает сложность. Так как центр Azure Stack является собственным частным экземпляром Azure, работающим в вашем центре обработки данных, его сложность по сути уменьшается.

Бизнес-процессы, дисциплины и многие рекомендации, описанные в статье Управление [методологией](../../govern/index.md) облачной инфраструктуры внедрения, по-прежнему можно применять к гибридным системам управления с помощью центра Azure Stack. Многие собственные средства облака, используемые в общедоступной облачной версии Azure, также можно использовать в центре Azure Stack.

## <a name="azure-stack-hub-governance-considerations"></a>Рекомендации по управлению центром Azure Stack

В следующей серии блогов показано, как можно реализовать концепции управления облаком для центра Azure Stack:

- [Службы Организации](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven/) , такие как группы ресурсов, управление доступом на основе РОЛЕЙ (RBAC), аудит изменений, блокировки и теги.
- [Службы безопасности](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/), включая брандмауэры по умолчанию, ограничения, обновления ВМ и управление исправлениями, а также состояние вредоносных программ.
- [DevOps параметры](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven-2/), включая инфраструктуру как код (IaC), портал с PowerShell и интерфейсом командной строки (CLI), Azure Application Insights и интеграцию с Azure DevOps и Jenkins.

## <a name="governance-toolchain-for-azure-stack-hub"></a>Управление цепочки инструментов для центра Azure Stack

Рекомендации по применению собственных средств управления в облаке для Azure Stack центральных средах см. по следующим ссылкам:

- [Azure Resource Manager шаблоны и настройка требуемого состояния](https://docs.microsoft.com/azure-stack/user/azure-stack-arm-templates?view=azs-2002)
- [PowerShell](https://docs.microsoft.com/azure-stack/user/azure-stack-powershell-overview?view=azs-2002)
- [Политика Azure](https://docs.microsoft.com/azure-stack/user/azure-stack-policy-module?view=azs-2002)
- [Управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure-stack/user/azure-stack-manage-permissions?view=azs-2002)

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Следующий шаг. Интеграция этой стратегии в свое путешествие для внедрения в облако

В следующих статьях приведены рекомендации по развертыванию облачных технологий в конкретных точках.

- [Управление Azure Stack Hub](./manage.md)
