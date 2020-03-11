---
title: Рекомендации по обеспечению готовности к работе в Azure
description: Обзор рекомендаций по обеспечению готовности к работе в Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: d7889b4020d906bb452ded413f6ff5e603bb9881
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892622"
---
# <a name="best-practices-for-azure-readiness"></a>Рекомендации по обеспечению готовности к работе в Azure

При обеспечении готовности к работе с облаком очень важно обучить персонал техническим навыкам, требуемым для внедрения облачных решений и подготовки целевой среды к размещению перемещаемых в облако ресурсов и рабочих нагрузок. Ознакомьтесь с этими и другими рекомендациями, которые помогут вашей команде подготовить среду Azure.

## <a name="azure-fundamentals"></a>Основные понятия Azure

Организация и развертывание ресурсов в среде Azure.

- [Основные понятия Azure.](../considerations/fundamental-concepts.md) Изучите основные понятия и термины и узнайте, как они связаны друг с другом.
- [Рекомендации по именованию и добавлению тегов.](../azure-best-practices/naming-and-tagging.md) Ознакомьтесь с подробными рекомендациями по именованию и ресурсов и расстановке в них тегов. Эти рекомендации касаются внедрения облачных решений в организации.
- [Масштабирование с использованием нескольких подписок Azure.](../azure-best-practices/scaling-subscriptions.md) Узнайте о стратегиях масштабирования с использованием нескольких подписок Azure.
- [Организация ресурсов с помощью групп управления Azure.](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Узнайте, как группы управления Azure помогают управлять ресурсами, роли, политиками и развертываниями в нескольких подписках.
- [Обеспечение согласованности гибридного облака.](../considerations/hybrid-consistency.md) Создайте гибридные облачные решения, которые предоставляют преимущества облачных технологий наряду со многими функциями локального управления.

## <a name="networking"></a>Сеть

Подготовьте сетевую инфраструктуру облака для использования рабочих нагрузок.

- [Решения по выбору сетей.](../considerations/networking-options.md) Выберите сетевые службы, средства и архитектуру с учетом требований к корпоративной рабочей нагрузке, системе управления и подключению.
- [Планирование виртуальной сети.](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Спланируйте виртуальные сети с учетом требований к изоляции, подключению и расположению.
- [Рекомендации по защите сети.](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Ознакомьтесь с рекомендациями по устранению общих проблем с защитой сети с помощью встроенных возможностей Azure.
- [Сети периметра.](./perimeter-networks.md) Включите безопасное подключение между облачными сетями и локальными или физическими сетями центра обработки данных, а также двухсторонний обмен данными с Интернетом.
- [Звездообразная топология сети](./hub-spoke-network-topology.md). Эффективно управляйте общими требованиями к обмену данными или безопасности для сложных рабочих нагрузок и устраняйте возможные ограничения, связанные с использованием подписок.

## <a name="identity-and-access-control"></a>Идентификаторы и управление доступом

Проектируйте инфраструктуру управления удостоверениями и доступом, чтобы оптимизировать работу систем управления и безопасности для рабочих нагрузок.

- [Рекомендации по защите управления удостоверениями и доступом в Azure.](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Ознакомьтесь с рекомендациями по управлению удостоверениями и доступом с помощью встроенных возможностей Azure.
- [Рекомендации по управлению доступом на основе ролей.](../considerations/roles.md) Включите избирательное управление доступом на основе групп для ресурсов, связанных с ролями пользователей.
- [Защита привилегированного доступа для гибридных и облачных развертываний в Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Убедитесь, что корпоративные учетные записи административного доступа и привилегированные учетные записи защищены в пределах облачной и локальной сред.

## <a name="storage"></a>Память

- [Рекомендации по выбору службы хранилища Azure.](../considerations/storage-options.md) Выберите оптимальное решение службы хранилища Azure в соответствии с вашими сценариями использования.
- [Руководство по защите службы хранилища Azure.](https://docs.microsoft.com/azure/storage/blobs/security-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Узнайте о функциях системы безопасности службы хранилища Azure.

## <a name="databases"></a>Базы данных

- [Выбор оптимального варианта SQL Server в Azure.](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Выберите решение PaaS или IaaS, которое наилучшим образом подходит для ваших рабочих нагрузок SQL Server.
- [Рекомендации по защите базы данных.](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Ознакомьтесь с рекомендациями по защите базы данных в Azure.
- [Выбор подходящего хранилища данных](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Выберите хранилище данных в соответствии со своими требованиями. В базах данных SQL и NoSQL доступны сотни вариантов реализации. Хранилища данных обычно различают по методам структурирования данных и типам поддерживаемых операций. В этой статье описаны некоторые распространенные модели хранилища.

## <a name="cost-management"></a>управления затратами;

- [Отслеживание затрат в бизнес-подразделениях, средах и проектах.](./track-costs.md) Ознакомьтесь с рекомендациями по созданию оптимальных механизмов отслеживания затрат.
- [Оптимизация инвестиций в облако с помощью службы "Управление затратами Azure".](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Реализуйте стратегию по управлению затратами и узнайте об инструментах для решения сопутствующих задач.
- [Создание бюджетов и управление ими.](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Узнайте, как создавать бюджеты и управлять ими в Управлении затратами Azure.
- [Экспорт данных о затратах.](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Узнайте, как экспортировать данные о затратах с помощью Управления затратами Azure.
- [Оптимизация затрат на основе рекомендаций.](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Узнайте, как определять малоиспользуемые ресурсы и сокращать затраты с помощью Управления затратами Azure и Помощника по Azure.
- [Использование оповещений о затратах для мониторинга потребления и расходов.](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Узнайте, как использовать оповещения Управления затратами для отслеживания потребления и расходов в Azure.
