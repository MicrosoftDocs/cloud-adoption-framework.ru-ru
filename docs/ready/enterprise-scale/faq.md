---
title: ВОПРОСЫ И ОТВЕТЫ
description: Вопросы и ответы.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: befa3a167d38dc49120255b7ba7f5a992be8d888
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076913"
---
# <a name="faq"></a>ВОПРОСЫ И ОТВЕТЫ

На этой странице приведены часто задаваемые вопросы по проектированию корпоративного уровня и реализации contoso.

## <a name="enterprise-scale-design"></a>Проектирование корпоративного масштаба

### <a name="where-a-landing-zone-maps-in-azure-in-the-context-of-enterprise-scale"></a>Когда целевая зона сопоставляется в Azure в контексте корпоративного масштаба

С точки зрения корпоративного масштаба Подписка — это Целевая зона в Azure.

## <a name="contoso-implementation"></a>Реализация contoso

### <a name="why-enterprise-scale-azure-resource-manager-templates-require-permissions-at-the-tenant-root--scope"></a>Почему для шаблонов Azure Resource Manager предприятия требуются разрешения в корневой области клиента

Создание группы управления — это `put` интерфейс программирования приложений на уровне клиента. Необходимым условием для использования примеров шаблонов является предоставление разрешения в корневой области.

### <a name="why-sync-a-fork-with-the-upstream-repo"></a>Зачем синхронизировать вилку с вышестоящим репозиторием

Это позволяет управлять частотой и исправлениями. Это промежуточное решение, в то время как мы упаковываем базу кода конвейера как действия GitHub, поэтому этот шаг не потребуется в будущем.
