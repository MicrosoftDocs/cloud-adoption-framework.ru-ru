---
title: Руководство по принятию решений о миграции
description: Используйте это дерево принятия решений в качестве руководства по обобщенному выбору оптимальных средств в зависимости от решений по миграции.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: internal
ms.openlocfilehash: c3dfeaaa097f6bd87dd3b02c6026d414d1f65750
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102113271"
---
# <a name="migration-tools-decision-guide"></a>Руководство по принятию решений о миграции

Выбор стратегий и средств для переноса приложений в Azure во многом зависит от бизнес-факторов этого переноса, технологических стратегий и временных ограничений. Он потребует глубокого понимания рабочих нагрузок и ресурсов (инфраструктуры, приложений и данных), к которым будет применяться миграция. Представленное ниже дерево принятия решений выполняет роль руководства по обобщенному выбору оптимальных средств на основе решений по миграции. Используйте это дерево принятия решений в качестве отправной точки.

Выбор между миграцией с использованием технологий PaaS (платформа как услуга) или IaaS (инфраструктура как услуга) зависит от баланса между стоимостью, временем, техническими зависимостями и долгосрочными ожиданиями. Чаще всего IaaS обеспечит самый быстрый переход к облаку с минимальными изменениями рабочей нагрузки. Для PaaS обычно требуются изменения в исходном коде или структурах данных, но такая модель дает значительное долгосрочное преимущество в виде снижения эксплуатационных расходов и повышения технической гибкости. На следующей схеме термин *модернизация* обозначает решение о модернизации ресурса в процессе миграции с размещением обновленного ресурса на платформе PaaS.

![Пример дерева принятия решений по миграции.](../../_images/migrate/migration-tools-decision-tree.png)

## <a name="key-questions"></a>Основные вопросы

Ответив на следующие вопросы, вы сможете принять решение с помощью представленного выше дерева.

- **Будет ли разумным тратить время, силы и деньги на модернизацию платформы приложения одновременно с миграцией?** Технологии PaaS, такие как Служба приложений Azure и Функции Azure, способны увеличить гибкость развертывания и упростить управление виртуальными машинами, на которых размещаются приложения. Для полноценной реализации таких облачных преимуществ может потребоваться рефакторинг приложений, что может повлечь немалые затраты ресурсов на выполнение процесса миграции. Хорошим кандидатом для модернизации будет приложение, которое можно перевести на технологии PaaS с минимальными изменениями. Если же требуется обширный рефакторинг, часто лучше выбрать перенос на виртуальные машины на платформе IaaS.
- **Будет ли разумным тратить время, силы и деньги на модернизацию платформы данных одновременно с миграцией?** Как и в случае с миграцией приложений, управляемые службы хранения Azure PaaS (например, База данных SQL Azure, Azure Cosmos DB и служба хранилища Azure) предлагают гибкость и возможности управления. Но для перехода на эти службы может потребоваться рефакторинг существующих данных и использующих их приложений. Для платформ данных рефакторинг обычно требуется выполнять в намного меньшем объеме, чем для платформы приложений. По этой причине распространенным сценарием является модернизация платформы данных с сохранением прежней платформы приложений. Для модернизации лучше всего подходят такие данные, которые можно перенести в управляемую службу данных с минимальными изменениями. Данные, для рефакторинга которых в формат PaaS потребуется значительное время или большие затраты, часто лучше переносить на виртуальные машины на платформе IaaS. Это позволит в полной мере воспользоваться существующими возможностями размещения.
- **Выполняется ли приложение в настоящее время на выделенных виртуальных машинах или в совместном размещении с другими приложениями?** На платформы PaaS часто проще перенести приложения, которые работают на выделенных виртуальных машинах, чем выполняемые на общих серверах.
- **Потребует ли перенос данных больше пропускной способности, чем обеспечивает ваша сеть?** Пропускная способность сети между локальными источниками данных и Azure может ограничить возможности по переносу данных. Если передача данных создаст нагрузку на сеть, превышающую эффективные возможности сети или значительно замедляющую процесс, могут потребоваться альтернативные или автономные механизмы передачи. [Статья о репликации для миграции](../../migrate/migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) в Cloud Adoption Framework описывает ограничения репликации и их влияние на процесс миграции. В процессе оценки готовности к миграции уточните у ИТ-специалистов, соответствует ли пропускная способность локальной сети и подключения к Интернету всем требованиям к миграции. Также изучите [вариант миграции, когда требования к хранилищу данных превышают возможности сети](../../migrate/azure-best-practices/network-capacity-exceeded.md#suggested-prerequisites).
- **Использует ли приложение существующий конвейер DevOps?** Во многих случаях предложение Azure Pipelines поддерживает рефакторинг для развертывания приложений в облачных средах размещения.
- **Предъявляют ли ваши данные сложные требования к хранилищу?** Для рабочих приложений обычно требуется хранилище данных с высоким уровнем доступности, поддержкой функции AlwaysOn и другими возможностями для обеспечения доступности и непрерывности работы. Варианты управляемых баз данных Azure на основе PaaS (Базы данных SQL Azure, База данных Azure для MySQL и Azure Cosmos DB) поддерживают соглашения об уровне обслуживания с гарантией непрерывной работы на уровне 99,99 %. При этом решение с технологиями IaaS (SQL Server на виртуальных машинах Azure) предлагает соглашения об уровне обслуживания для одного экземпляра на уровне 99,95 %. Если данные невозможно модернизировать для использования хранилища PaaS, обеспечение более продолжительной бесперебойной работы для хранилищ данных IaaS потребует применения сложных сценариев, например с использованием кластеров SQL Server AlwaysOn и непрерывной синхронизацией данных между экземплярами. Это может повлечь значительные затраты на размещение и обслуживание, поэтому при рассмотрении вариантов миграции уделяйте особое внимание соблюдению баланса между требованиями бесперебойной работы, усилиями по модернизации и ограничениями бюджета.

## <a name="innovation-and-migration"></a>Инновации и миграция

Так как платформа Cloud Adoption Framework в значительной мере ориентирована на процессы [добавочной миграции](../../migrate/index.md#migration-effort), любое первоначальное решение о стратегии и средствам миграции не исключает реализации последующих инноваций и обновлений приложений для использования новых возможностей платформы Azure. Даже если первоначальная миграция нацелена только на смену размещения по модели IaaS, обязательно регулярно проверяйте портфель размещенных в облаке приложений для определения возможностей по оптимизации.

## <a name="learn-more"></a>Дополнительные сведения

- **[Общие сведения об облаке. Обзор вычислительных служб в Azure](/azure/architecture/guide/technology-choices/compute-decision-tree).** Содержит сведения о возможностях вычислительных служб IaaS и PaaS в Azure.
- **[Общие сведения об облаке. Выбор подходящего хранилища данных](/azure/architecture/guide/technology-choices/data-store-overview).** Описывает варианты хранилищ данных PaaS на платформе Azure.
- **[Рекомендации по миграции. Потребности, связанные с данными, превышают пропускную способность сети в процессе миграции](../../migrate/azure-best-practices/network-capacity-exceeded.md).** Описывает альтернативные механизмы переноса данных для сценариев, в которых такой перенос затруднен ограничениями пропускной способности сети.
- **[База данных SQL. Выбор оптимального варианта SQL Server в Azure](/azure/azure-sql/azure-sql-iaas-vs-paas-what-is-overview#business-motivations-for-choosing-databases-managed-instances-or-sql-virtual-machines).** Описание вариантов и бизнес-обоснований для выбора между размещением рабочих нагрузок SQL Server в среде на основе управляемой инфраструктуры (IaaS) или управляемой службы (PaaS).
