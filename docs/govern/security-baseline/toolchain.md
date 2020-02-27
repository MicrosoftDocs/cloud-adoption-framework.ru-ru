---
title: Средства основных способов защиты в Azure
description: Узнайте, как собственные средства Azure могут помочь развитым политикам и процессам, которые поддерживают дисциплину управления базовыми показателями безопасности.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 85b0d88d4a275c7215a498b95e0af6717bfac169
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707073"
---
# <a name="security-baseline-tools-in-azure"></a>Средства основных способов защиты в Azure

[Основные способы защиты](./index.md) — это одна из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина сосредоточена на способах установки политик, защищающих сеть, ресурсы и, что важнее, данных, которые будут находиться в решении поставщика облачных служб. В рамках пяти дисциплин управления облаком Базовая оценка безопасности подразумевает классификацию цифровых площадей и данных. Он также включает документацию по рискам, отклонения в бизнесе и стратегии устранения рисков, связанные с безопасностью данных, ресурсов и сетей. С технической точки зрения эта дисциплина также включает участие в принятии решений о [шифровании](../../decision-guides/encryption/index.md), [требованиях к сети](../../decision-guides/software-defined-network/index.md), [стратегиях гибридной идентификации](../../decision-guides/identity/index.md)и средствах для [автоматизации принудительного применения](../../decision-guides/policy-enforcement/index.md) политик безопасности в [группах ресурсов](../../decision-guides/resource-consistency/index.md).

Следующий список средств Azure может помочь в обработке политик и процессов, поддерживающих базовые показатели безопасности.

| Инструмент | [Портал Azure](https://azure.microsoft.com/features/azure-portal) и [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Хранилище ключей Azure](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Политика Azure](https://docs.microsoft.com/azure/governance/policy/overview) | [Центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Применение элементов управления доступом к ресурсам и процессам создания ресурсов   | Да                             | нет              | Да      | нет           | нет                    | нет            |
| Защита виртуальных сетей Azure                                    | Да                             | нет              | нет       | Да          | нет                    | нет            |
| Шифрование виртуальных дисков                                     | нет                              | Да             | нет       | нет           | нет                    | нет            |
| Шифрование хранилища и баз данных PaaS                         | нет                              | Да             | нет       | нет           | нет                    | нет            |
| Управление службами гибридной идентификации                            | нет                              | нет              | Да      | нет           | нет                    | нет            |
| Ограничение разрешенных типов ресурсов                         | нет                              | нет              | нет       | Да          | нет                    | нет            |
| Принудительные ограничения географических регионов                          | нет                              | нет              | нет       | Да          | нет                    | нет            |
| Мониторинг работоспособности системы безопасности сети и ресурсов          | нет                              | нет              | нет       | нет           | Да                   | Да           |
| Обнаружение вредоносных действий                                  | нет                              | нет              | нет       | нет           | Да                   | Да           |
| Заблаговременное обнаружение уязвимостей                        | нет                              | нет              | нет       | нет           | Да                   | нет            |
| Настройка резервного копирования и аварийного восстановления данных                     | Да                             | нет              | нет       | нет           | нет                    | нет            |

Полный список средств безопасности и служб Azure см. в [этой статье](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Кроме того, клиенты часто используют сторонние средства для упрощения базовых действий безопасности. Дополнительные сведения см. в статье [Интеграция решений по обеспечению безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

В дополнение к средствам безопасности [Центр управления безопасностью Microsoft](https://www.microsoft.com/trustcenter/guidance/risk-assessment) содержит подробные инструкции, отчеты и связанную документацию, которые помогут вам выполнить оценку рисков как часть процесса планирования миграции.
