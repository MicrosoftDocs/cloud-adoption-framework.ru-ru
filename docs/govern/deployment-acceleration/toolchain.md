---
title: Средства ускорения развертывания в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Средства ускорения развертывания в Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d47162b3e1a6a303e8b346146948667bc42c2326
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222672"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Средства ускорения развертывания в Azure

[Ускорение развертывания](./index.md) является одной из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина сосредоточена на способах создания политики для контроля конфигурации или развертывания ресурсов. В рамках пяти дисциплин управления облаком ускорение развертывания включает в себя развертывание и выравнивание конфигурации. Эти действия можно выполнять вручную или автоматически с помощью DevOps. В любом случае задействованные политики будут сохраняться практически одинаково.

Хранители облака, защитники облака и архитекторы облачных решений, интересующиеся системой управления, могут уделить большое количество времени дисциплине "Ускорение развертывания", которая фиксирует принципы политики и требования в нескольких различных процедурах по внедрению облачных технологий. Средства в этом цепочки инструментов важны для группы управления облаком и должны иметь высокий приоритет для руководства по обучению группы.

Ниже приведен список инструментов Azure, которые могут помочь в совершенствовании политик и процессов, поддерживающих эту дисциплину системы управления.

|  | [Политика Azure](https://docs.microsoft.com/azure/governance/policy/overview) | [Группы управления Azure](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) | [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Граф ресурсов Azure](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Управление затратами Azure](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
|Реализация корпоративных политик     |Да |Нет  |Нет  |Нет | Нет |Нет |
|Применение политик в подписках     |Обязательное значение |Да  |Нет  |Нет | Нет |Нет |
|Развертывание определенных ресурсов     |Нет |Нет  |Да  |Нет | Нет |Нет |
|Создание полностью соответствующих сред      |Обязательное значение |Обязательное значение  |Обязательное значение  |Да | Нет |Нет |
|Политики аудита      |Да |Нет  |Нет  |Нет | Нет |Нет |
|Запрос к ресурсам Azure      |Нет |Нет  |Нет  |Нет |Да |Нет |
|Отчет о стоимости ресурсов      |Нет |Нет  |Нет  |Нет |Нет |Да |

Ниже приведены дополнительные средства, которые могут потребоваться для выполнения определенных задач ускорения развертывания. Часто эти средства используются за пределами команды системы управления, но по-прежнему считаются важным аспектом дисциплины "Ускорение развертывания".

|  | [портал Azure](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Политика Azure](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure DevOps](https://docs.microsoft.com/azure/devops/index) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
|Развертывание вручную (один ресурс)     | Да | Да  | Нет  | Не эффективное | Нет | Да |
|Развертывание вручную (полная среда)     | Не эффективное | Да | Нет  | Не эффективное | Нет | Да |
|Автоматическое развертывание (полная среда)     | Нет  | Да  | Нет  | Да  | Нет | Да |
|Обновление конфигурации одного ресурса     | Да | Да | Не эффективное | Не эффективное | Нет | Да — во время репликации |
|Обновление конфигурации полной среды     | Не эффективное | Да | Да | Да  | Нет | Да — во время репликации |
|Управление схемой конфигурации     | Не эффективное | Не эффективное | Да  | Да  | Нет | Да — во время репликации |
|Создание автоматического конвейера для развертывания кода и настройки ресурсов (DevOps)     | Нет | Нет | Нет | Да | Нет | Нет |

Помимо собственных средств Azure, упомянутых выше, довольно часто клиенты используют сторонние средства для упрощения развертываний в рамках дисциплины "Ускорение развертывания" и развертываний DevOps.