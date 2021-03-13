---
title: Управление и мониторинг корпоративного уровня для SAP в Azure
description: Узнайте о вопросах проектирования и рекомендациях по управлению и мониторингу SAP в Azure.
author: JefferyMitchell
ms.author: brblanch
ms.date: 03/01/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: e7a70b51d2d66723fbcfb95ca0616bddacdce5ba
ms.sourcegitcommit: 36e85ac734b184de3f29884b744ea74c81ccc72b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2021
ms.locfileid: "103442987"
---
# <a name="enterprise-scale-management-and-monitoring-for-sap-on-azure"></a>Управление и мониторинг корпоративного уровня для SAP в Azure

В этой статье рассматривается, как с помощью централизованного управления и мониторинга на уровне платформы работать с SAP в корпоративной области Azure. В статье представлены основные рекомендации для групп деятельности SAP по обслуживанию систем SAP на платформе Azure.

**Рекомендации по проектированию:**

Ниже приведены некоторые рекомендации по проектированию для мониторинга и управления SAP в Azure.

- Рассмотрим централизованную рабочую область Azure Log Analytics с Azure Monitor и Application Insights для установки мониторинга уровня платформы и приложений.

- Рассмотрим отслеживание задержки между виртуальными машинами (VM) для приложений, зависящих от задержки.

- Рассмотрите возможность планирования [азакснап](/azure/azure-netapp-files/azacsnap-introduction) из Центральной виртуальной машины, а не на отдельных виртуальных машинах.

**Рекомендации по проектированию:**

Ниже приведены некоторые рекомендации по проектированию для мониторинга и управления SAP в Azure.

- Мониторинг систем и решений SAP.

- Используйте диспетчер решений SAP и [Azure Monitor для решений SAP](/azure/virtual-machines/workloads/sap/azure-monitor-overview) , чтобы отслеживать SAP Hana, КЛАСТЕРы SUSE с высоким уровнем доступности и системы SQL.

- Запустите расширение виртуальной машины для проверки SAP. Расширение виртуальной машины для SAP использует назначенную виртуальной машиной управляемую идентификацию для доступа к данным мониторинга и конфигурации ВИРТУАЛЬНОЙ машины. Проверка гарантирует, что все метрики производительности, отображаемые в приложении SAP, берутся из базового [расширения Azure для SAP](/azure/virtual-machines/workloads/sap/deployment-guide).

- Защитите свою базу данных HANA с помощью службы [Azure Backup](/azure/virtual-machines/workloads/sap/sap-hana-backup-guide) . При развертывании Azure NetApp Files (использовании) для базы данных HANA используйте [средство создания моментальных снимков с единообразием приложений Azure (азакснап)](/azure/azure-netapp-files/azacsnap-introduction) для создания моментальных снимков, соответствующих приложению.

- Создание платформы мониторинга с помощью средств [телеметрии SAP](https://github.com/microsoft/saptelemetry) для предоставления сведений о бизнес-процессах.

- [Монитор подключения](/azure/network-watcher/connection-monitor) наблюдателя за сетями используется для наблюдения за метриками задержки базы данных SAP и сервера приложений, а также для сбора и отображения измерений задержки сети с помощью [Azure Monitor](https://techcommunity.microsoft.com/t5/running-sap-applications-on-the/collecting-and-displaying-niping-network-latency-measurements/ba-p/1833979).

- Используйте [Azure Site Recovery](/azure/site-recovery/monitoring-common-questions) наблюдение для поддержания работоспособности службы аварийного восстановления для серверов приложений SAP.

- Оптимизируйте операции SAP и управляйте ими с помощью [ландшафтного управления SAP (лама)](https://www.sap.com/products/landscape-management.html). Используйте [соединитель SAP лама для Azure](/azure/virtual-machines/workloads/sap/lama-installation) для перемещения, копирования, клонирования и обновления систем SAP.

- Выполните [проверку качества SAP HANA](https://github.com/Azure/SAP-on-Azure-Scripts-and-Utilities/tree/main/QualityCheck) в подготовленной инфраструктуре Azure, чтобы убедиться, что подготовленные виртуальные машины соответствуют SAP HANA в рекомендациях Azure.

- Для каждой подписки Azure выполните [проверку задержки для зоны доступности Azure](https://github.com/Azure/SAP-on-Azure-Scripts-and-Utilities/tree/main/AvZone-Latency-Test) перед развертыванием зональные, чтобы выбрать зоны с низкой задержкой для развертывания SAP в Azure.

- Внедрение защиты от угроз для SAP с помощью [Sentinel Azure](/azure/sentinel/overview).
