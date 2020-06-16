---
title: ВОПРОСЫ И ОТВЕТЫ
description: ВОПРОСЫ И ОТВЕТЫ
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 7225502e8b02f2bd54dd61fe67aa2c9465621ed7
ms.sourcegitcommit: d88c1cc3597a83ab075606d040ad659ac4b33324
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2020
ms.locfileid: "84792484"
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
