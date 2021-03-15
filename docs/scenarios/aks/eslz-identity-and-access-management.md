---
title: Управление удостоверениями и доступом в масштабах предприятия для AKS
description: Описание того, как этот сценарий корпоративного уровня может улучшить управление удостоверениями и доступом для службы Azure Kubernetes.
author: TomGeske
ms.author: thomasge
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 12ca9ad27af872e64d4cef1a90a99c04f5c21c87
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101798958"
---
# <a name="identity-and-access-management-for-azure-kubernetes-service-aks-enterprise-scale-scenario"></a>Сценарий корпоративного уровня управления удостоверениями и доступом для Azure Kubernetes Service (AKS)

Вашей организации или компании необходимо разработать подходящие параметры безопасности для удовлетворения их требований. Управление удостоверениями и доступом охватывает несколько аспектов, таких как удостоверения кластера, удостоверения рабочей нагрузки и доступ к операторам.

## <a name="design-considerations"></a>Рекомендации по проектированию

- Решите, какое удостоверение кластера используется (управляемое удостоверение или субъект-служба).
- Выбор способа проверки подлинности доступа к кластеру (на основе сертификатов или Azure Active Directory).
- Выберите кластер с несколькими клиентами и настройте управление доступом на основе ролей (RBAC) в Kubernetes.
  - Выберите метод для изоляции (пространство имен, сетевая политика, вычисление (пул узлов) или кластер).
  - Примите решение о ролях Kubernetes RBAC и распределении вычислений на уровне группы приложений для изоляции.
  - Решите, могут ли группы приложений считывать другие рабочие нагрузки в своем кластере или в других кластерах.
- Определите пользовательские роли RBAC Azure для [целевой зоны AKS](../../ready/enterprise-scale/identity-and-access-management.md).
  - Определите, какие разрешения требуются для роли "Проектирование надежности сайта" (выполняются), чтобы администрировать или устранять неполадки в целом кластере.
  - Определите, какие разрешения требуются для SecOps.
  - Определите, какие разрешения необходимы для владельца целевой зоны.
  - Определите, какие разрешения необходимы группам приложений для развертывания в кластере.
- Решите, требуются ли удостоверения рабочей нагрузки (удостоверения Pod Azure AD). Они могут потребоваться для служб Azure, таких как интеграция Azure Key Vault, Azure Cosmos DB и др.

## <a name="design-recommendations"></a>Рекомендации по проектированию

- **Удостоверения кластера**
  - Используйте собственное [управляемое удостоверение](https://aka.ms/aks/mi) для кластера AKS.
  - Определите пользовательские роли RBAC Azure для целевой зоны AKS, чтобы упростить управление необходимыми разрешениями для удостоверения, управляемого кластером.
- **Доступ к кластеру**
  - Используйте Kubernetes RBAC с Azure AD для [ограничения привилегий](/azure/aks/azure-ad-rbac) и минимального предоставления прав администратора для защиты конфигурации и секретного доступа.
  - Используйте [интеграцию Azure AD, управляемую AKS](https://aka.ms/aks/managed-aad) , чтобы использовать Azure AD для проверки подлинности и доступа к операторам и разработчикам.
- Определите необходимые роли RBAC и привязки ролей в Kubernetes.
  - Используйте [роли и привязки ролей Kubernetes](/azure/aks/concepts-identity#kubernetes-role-based-access-control-kubernetes-rbac) для групп Azure AD для обеспечения надежности сайта (выполняются), SecOps и доступа для разработчиков.
  - ВЫПОЛНЯЮТСЯ полный доступ должен быть предоставлен по требованию. Используйте [Управление привилегированными пользователями в Azure AD](/azure/active-directory/privileged-identity-management/pim-configure) и управление удостоверениями и доступом в [масштабах предприятия](../../ready/enterprise-scale/identity-and-access-management.md).