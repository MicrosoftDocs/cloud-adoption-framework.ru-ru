---
title: Средства основных способов защиты в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Описание средств, которые могут способствовать повышению уровня безопасности в Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3bf3eea5486fbd349094663dc5f37527f5042bb5
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221688"
---
# <a name="security-baseline-tools-in-azure"></a>Средства основных способов защиты в Azure

[Основные способы защиты](./index.md) — это одна из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина сосредоточена на способах установки политик, защищающих сеть, ресурсы и, что важнее, данных, которые будут находиться в решении поставщика облачных служб. В рамках пяти дисциплин управления облаком Базовая оценка безопасности подразумевает классификацию цифровых площадей и данных. Он также включает документацию по рискам, отклонения в бизнесе и стратегии устранения рисков, связанные с безопасностью данных, ресурсов и сетей. С технической точки зрения эта дисциплина также включает участие в принятии решений [о шифровании](../../decision-guides/encryption/index.md), [требованиях к сети](../../decision-guides/software-defined-network/index.md), [стратегиях гибридной идентификации](../../decision-guides/identity/index.md) и средствах для [автоматизации принудительного применения](../../decision-guides/policy-enforcement/index.md) политик безопасности. между [группами ресурсов](../../decision-guides/resource-consistency/index.md).

Следующий список средств Azure может помочь в обработке политик и процессов, поддерживающих базовые показатели безопасности.

| Tool | [Портал Azure](https://azure.microsoft.com/features/azure-portal) / [Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Хранилище ключей Azure](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Политика Azure](https://docs.microsoft.com/azure/governance/policy/overview) | [Центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
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

Полный список средств безопасности и служб Azure см. в [этой статье](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Кроме того, клиенты часто используют сторонние средства для упрощения базовых действий безопасности. Дополнительные сведения см. в статье [Интеграция решений по обеспечению безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

В дополнение к средствам безопасности [Центр управления безопасностью Microsoft](https://www.microsoft.com/trustcenter/guidance/risk-assessment) содержит подробные инструкции, отчеты и связанную документацию, которые помогут вам выполнить оценку рисков как часть процесса планирования миграции.
