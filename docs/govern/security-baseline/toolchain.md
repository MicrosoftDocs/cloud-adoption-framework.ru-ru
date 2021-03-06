---
title: Средства основных способов защиты в Azure
description: Узнайте, как собственные средства Azure могут помочь развитым политикам и процессам, поддерживающим специализацию в плане безопасности.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: ea3fdbc23847b1e0c20c84bade64e5d0e96b439e
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101787643"
---
# <a name="security-baseline-tools-in-azure"></a>Средства основных способов защиты в Azure

По [специализации в плане безопасности](./index.md) — одна из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина сосредоточена на способах установки политик, защищающих сеть, ресурсы и, что важнее, данных, которые будут находиться в решении поставщика облачных служб. В рамках пяти дисциплин управления облаком Базовая оценка безопасности подразумевает классификацию цифровых площадей и данных. Он также включает документацию по рискам, отклонения в бизнесе и стратегии устранения рисков, связанные с безопасностью данных, ресурсов и сетей. С технической точки зрения эта дисциплина также включает участие в принятии решений о [шифровании](../../decision-guides/encryption/index.md), [требованиях к сети](../../decision-guides/software-defined-network/index.md), [стратегиях гибридной идентификации](../../decision-guides/identity/index.md)и средствах для [автоматизации принудительного применения](../../decision-guides/policy-enforcement/index.md) политик безопасности в [группах ресурсов](../../decision-guides/resource-consistency/index.md).

Следующий список средств Azure может помочь в обработке политик и процессов, поддерживающих эту дисциплину.

| Инструмент | [Портал Azure](https://azure.microsoft.com/features/azure-portal/) и [Azure Resource Manager](/azure/azure-resource-manager/management/overview) | [Хранилище ключей Azure](/azure/key-vault/)  | [Azure AD](/azure/active-directory/fundamentals/active-directory-whatis) | [Политика Azure](/azure/governance/policy/overview) | [Центр безопасности Azure](/azure/security-center/security-center-introduction) | [Azure Monitor](/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Применение элементов управления доступом к ресурсам и процессам создания ресурсов   | Да                             | Нет              | Да      | Нет           | Нет                    | Нет            |
| Защита виртуальных сетей Azure                                    | Да                             | Нет              | Нет       | Да          | Нет                    | Нет            |
| Шифрование виртуальных дисков                                     | Нет                              | Да             | Нет       | Нет           | Нет                    | Нет            |
| Шифрование хранилища и баз данных PaaS                         | Нет                              | Да             | Нет       | Нет           | Нет                    | Нет            |
| Управление службами гибридной идентификации                            | Нет                              | Нет              | Да      | Нет           | Нет                    | Нет            |
| Ограничение разрешенных типов ресурсов                         | Нет                              | Нет              | Нет       | Да          | Нет                    | Нет            |
| Принудительные ограничения географических регионов                          | Нет                              | Нет              | Нет       | Да          | Нет                    | Нет            |
| Мониторинг работоспособности системы безопасности сети и ресурсов          | Нет                              | Нет              | Нет       | Нет           | Да                   | Да           |
| Обнаружение вредоносных действий                                  | Нет                              | Нет              | Нет       | Нет           | Да                   | Да           |
| Заблаговременное обнаружение уязвимостей                        | Нет                              | Нет              | Нет       | Нет           | Да                   | Нет            |
| Настройка резервного копирования и аварийного восстановления данных                     | Да                             | Нет              | Нет       | Нет           | Нет                    | Нет            |

Полный список средств безопасности и служб Azure см. в [этой статье](/azure/security/fundamentals/services-technologies).

Клиенты обычно используют сторонние средства для реализации действий по специализации в плане безопасности. Дополнительные сведения см. в статье [Интеграция решений безопасности в центре безопасности Azure](/azure/security-center/security-center-partner-integration).

Помимо средств безопасности, [Управление соответствием в Microsoft 365](https://www.microsoft.com/microsoft-365/enterprise/compliance-management) содержит подробные рекомендации, отчеты и сопутствующую документацию, которая помогает выполнять оценку рисков в рамках процесса планирования миграции.
