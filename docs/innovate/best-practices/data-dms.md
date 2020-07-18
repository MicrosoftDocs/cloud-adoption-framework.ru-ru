---
title: Средства инноваций для переноса данных
description: Узнайте о Azure Database Migration Service и других средствах, которые выполняют миграцию и модернизировать данные для подготовки к облачным инвентионс и новшествам.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a21b41583789d25f00d8dfb81ac1e9b8943af004
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86449784"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Получение данных с помощью миграции и модернизации существующих источников данных

Компании часто имеют различные типы существующих данных, которые они могут [более демократичным](../considerations/data.md). Когда гипотеза клиента требует использования существующих данных для создания современных решений, первым шагом может быть миграция и модернизации данных для подготовки к инвентионс и нововведениям. Для соответствия существующим усилиям по миграции в рамках плана внедрения в облако можно легко выполнить миграцию и модернизации в рамках [методологии миграции](../../migrate/index.md).

## <a name="use-of-this-article"></a>Использование этой статьи

В этой статье описывается ряд подходов, которые выводятся в соответствии с методологией миграции. Эти подходы можно наилучшим образом согласовать со стандартным цепочки инструментов миграции.

На этапе оценки методологии миграции группа внедрения в облако оценивает текущее состояние и желаемое будущее состояние для перенесенного ресурса. Если этот процесс является частью усилий по инновациям, то обе группы по внедрению в облако могут использовать эту статью для выполнения этих оценок.

## <a name="primary-toolset"></a>Основной набор инструментов

При миграции и модернизировать локальных данных наиболее распространенным средством Azure является [Azure Database Migration Service](https://docs.microsoft.com/azure/dms). Эта служба является частью более широкой цепочки инструментов [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) . Для существующих SQL Server источников данных [Помощник по миграции данных](https://docs.microsoft.com/sql/dma/dma-overview) может помочь в оценке и миграции небольшого количества структур данных.

Для поддержки миграций Oracle и NoSQL можно также использовать [Database Migration Service](https://docs.microsoft.com/azure/dms) для определенных типов баз данных источника и назначения. Примеры включают перенос баз данных Oracle в базы данных PostgreSQL или MongoDB для Azure Cosmos DB. Как правило, группы внедрения используют средства партнеров или пользовательские сценарии для перехода на Azure Cosmos DB, Azure HDInsight или виртуальные машины в зависимости от инфраструктуры как услуги (IaaS).

## <a name="considerations-and-guidance"></a>Рекомендации и рекомендации

При использовании Azure Database Migration Service для переноса и модернизировать данных важно понимать следующее:

- Текущая платформа для размещения источника данных.
- Текущая версия.
- Будущая платформа и версия, которые наилучшим образом поддерживают гипотезу или цель клиента.

В следующей таблице приведены исходная и Целевая пары, которые можно проверить с помощью команды миграции. Каждая пара включает в себя возможность выбора средства и ссылку на соответствующее руководством.

### <a name="migration-type"></a>Тип перемещения

При автономной миграции простой приложения начинается с момента начала переноса. При использовании подключения к сети простой приложения ограничен только временем переключения в конце переноса.

Мы рекомендуем выбрать приемлемое время простоя предприятия и протестировать автономную миграцию. Это необходимо для проверки соответствия времени восстановления допустимому простою. Если время восстановления неприемлемо, выполните оперативную миграцию.

| Источник  | Назначение  | Инструмент  | Тип перемещения | Руководство |
|---|---|---|---|---|
| SQL Server | База данных SQL Azure | Database Migration Service | Автономная миграция | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql) |
| SQL Server | База данных SQL Azure | Database Migration Service | Миграция по сети | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online) |
| SQL Server | Управляемый экземпляр SQL Azure | Database Migration Service | Автономная миграция | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) |
| SQL Server | Управляемый экземпляр SQL Azure | Database Migration Service | Миграция по сети | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) |
| SQL Server RDS | База данных SQL Azure или Azure SQL Управляемый экземпляр | Database Migration Service | Миграция по сети | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online) |
| MySQL | База данных Azure для MySQL | Database Migration Service | Миграция по сети | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online) |
| PostgreSQL | База данных Azure для PostgreSQL | Database Migration Service | Миграция по сети | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online) |
| MongoDB | API Azure Cosmos DB для MongoDB | Database Migration Service | Автономная миграция | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db) |
| MongoDB | API Azure Cosmos DB для MongoDB | Database Migration Service | Миграция по сети | [Руководство](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online) |
