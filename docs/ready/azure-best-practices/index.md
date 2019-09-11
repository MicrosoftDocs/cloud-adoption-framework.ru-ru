---
title: Рекомендации по обеспечению готовности к работе в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Обзор рекомендаций по обеспечению готовности к работе в Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: f1d4423e230d2eeff524a864f163e0cb13dc065b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818273"
---
# <a name="best-practices-for-azure-readiness"></a>Рекомендации по обеспечению готовности к работе в Azure

При обеспечении готовности к работе с облаком очень важно обучить персонал техническим навыкам, требуемым для внедрения облачных решений и подготовки целевой среды к размещению перемещаемых в облако ресурсов и рабочих нагрузок. В следующих разделах приводятся рекомендации и дополнительные указания, которые помогут вашей группе настроить и подготовить среду Azure.

## <a name="azure-fundamentals"></a>Основные понятия Azure

Используйте перечисленные ниже руководства по упорядочению и развертыванию ресурсов в среде Azure.

- [Основные понятия Azure.](../considerations/fundamental-concepts.md) Изучите основные понятия и термины, используемые в Azure, а также то, как эти понятия связаны друг с другом.
- [Рекомендации по именованию и добавлению тегов.](../considerations/name-and-tag.md) Ознакомьтесь с подробными рекомендациями по именованию и ресурсов и расстановке в них тегов. Эти рекомендации касаются внедрения облачных решений в организации.
- [Масштабирование с использованием нескольких подписок Azure.](../considerations/scaling-subscriptions.md) Узнайте о стратегиях масштабирования с использованием нескольких подписок Azure.
- [Организация ресурсов с помощью групп управления Azure.](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте, как группы управления Azure помогают управлять ресурсами, роли, политиками и развертываниями в нескольких подписках.
- [Обеспечение согласованности гибридного облака.](../../infrastructure/misc/hybrid-consistency.md) Создайте гибридные облачные решения, которые предоставляют преимущества облачных технологий наряду со многими функциями локального управления.

## <a name="networking"></a>Сеть

Используйте следующие руководства, чтобы подготовить сетевую инфраструктуру облака для использования ваших рабочих нагрузок.

- [Решения по выбору сетей.](../considerations/network-decisions.md) Выберите сетевые службы, средства и архитектуру с учетом требований к корпоративной рабочей нагрузке, системе управления и подключению.
- [Планирование виртуальной сети.](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте, как спланировать виртуальные сети с учетом требований к изоляции, подключению и расположению.
- [Рекомендации по защите сети.](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Ознакомьтесь с рекомендациями по устранению общих проблем с защитой сети с помощью встроенных возможностей Azure.
- [Сети периметра.](./perimeter-networks.md) Сети периметра (также известны как промежуточные зоны, DMZ) обеспечивают безопасное подключение между облачными сетями и локальными или физическими сетями центра обработки данных, а также двухстороннюю связь с Интернетом.
- [Звездообразная топология сети.](./hub-spoke-network-topology.md) Звездообразная топология — это сетевая модель, которая учитывает общие требования к обмену данными и обеспечению безопасности для сложных рабочих нагрузок, а также позволяет устранять потенциальные ограничения, связанные с подписками Azure.

## <a name="identity-and-access-control"></a>Идентификаторы и управление доступом

Используйте следующие руководства при проектировании инфраструктуры управления удостоверениями и доступом, чтобы оптимизировать работу систем управления и безопасности для рабочих нагрузок.

- [Рекомендации по защите управления удостоверениями и доступом в Azure.](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Ознакомьтесь с рекомендациями по управлению удостоверениями и доступом с помощью встроенных возможностей Azure.
- [Рекомендации по управлению доступом на основе ролей.](./roles.md) Управление доступом на основе ролей Azure помогает избирательно контролировать доступ на основе групп к ресурсам c назначением определенных ролей пользователей.
- [Защита привилегированного доступа для гибридных и облачных развертываний в Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Используйте Azure Active Directory для защиты учетных записей администраторов и административного доступа в пределах организации в облаке и локальной среде.

## <a name="storage"></a>Хранилище

- [Рекомендации по выбору службы хранилища Azure.](../considerations/storage-guidance.md) Выберите оптимальное решение службы хранилища Azure в соответствии с вашими сценариями использования.
- [Руководство по защите службы хранилища Azure.](https://docs.microsoft.com/azure/storage/common/storage-security-guide?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте о функциях системы безопасности службы хранилища Azure.

## <a name="databases"></a>Базы данных

- [Выбор оптимального варианта SQL Server в Azure.](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Выберите решение PaaS или IaaS, которое наилучшим образом подходит для ваших рабочих нагрузок SQL Server.
- [Рекомендации по защите базы данных.](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Ознакомьтесь с рекомендациями по защите базы данных в Azure.
- [Выбор подходящего хранилища данных](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Выбор правильного хранилища данных, соответствующего всем требованиям, является для проекта ключевым решением. Выбирать приходится буквально из сотен реализаций баз данных SQL и NoSQL. Хранилища данных обычно различают по методам структурирования данных и типам поддерживаемых операций. В этой статье описаны несколько самых распространенных моделей хранилища.

## <a name="cost-management"></a>управления затратами;

- [Отслеживание затрат в бизнес-подразделениях, средах и проектах.](./track-costs.md) Ознакомьтесь с рекомендациями по созданию оптимальных механизмов отслеживания затрат.
- [Оптимизация инвестиций в облако с помощью службы "Управление затратами Azure".](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Реализуйте стратегию по управлению затратами и узнайте об инструментах для решения сопутствующих задач.
- [Создание бюджетов и управление ими.](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте, как создавать бюджеты и управлять ими в службе "Управление затратами Azure".
- [Экспорт данных о затратах.](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте, как создавать экспортированные данные и управлять ими в Управлении затратами Azure.
- [Оптимизация затрат на основе рекомендаций.](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте, как определять малоиспользуемые ресурсы и снижать затраты с помощью службы "Управление затратами Azure" и Помощника по Azure.
- [Использование оповещений о затратах для мониторинга потребления и расходов.](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Узнайте, как использовать оповещения Управления затратами для отслеживания потребления и расходов в Azure.
