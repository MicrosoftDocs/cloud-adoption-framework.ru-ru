---
title: 'Облачные инновации: служба переноса данных'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Облачные инновации — служба переноса данных
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c75efe3576bb61ecb116ab22e4946b8d87da3d4a
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683417"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Получение данных с помощью миграции и модернизации существующих источников данных

Компании часто имеют множество существующих данных, которые можно [демократичными](../considerations/data.md). Когда гипотеза клиента требует использования существующих данных для создания современных решений, первым шагом может быть миграция и модернизации данных для подготовки к инвентионс и нововведениям. Для согласования с существующими усилиями по миграции в рамках плана внедрения в облако миграция и модернизации могут быть более легко выполнены в [методологии миграции](../../migrate/index.md).

## <a name="use-of-this-article"></a>Использование этой статьи

В этой статье описаны серии подходов, которые согласованы с процессом миграции, но их можно лучше согласовать со стандартным цепочки инструментов миграции. Во время процесса оценки в методологии миграции группа внедрения в облако будет оценивать текущее состояние и потребовала перехода к будущему состоянию ресурса. Если этот процесс является частью усилий по инновациям, то обе группы по внедрению в облако могут использовать эту статью для принятия этих решений.

## <a name="primary-toolset"></a>Основной набор инструментов

При миграции и модернизации данных, которые в настоящее время находятся в локальной системе, наиболее распространенным средством Azure является [Служба миграции данных (DMS)](https://docs.microsoft.com/azure/dms) , которая является частью более широкой цепочки инструментов службы " [Миграция Azure](https://docs.microsoft.com/azure/migrate/migrate-services-overview) ". Для существующих SQL Server источников данных [Помощник по миграции данных (DMA)](/sql/dma/dma-overview) также может помочь в оценке и переносе меньшего количества структур данных.

Для поддержки миграций Oracle и NoSQL [Служба миграции данных (DMS)](https://docs.microsoft.com/azure/dms) также может использоваться для определенных типов источника с целевыми базами данных, таких как Oracle в PostgreSQL или MongoDB для Cosmos DB. Чаще всего команды перехода используют сторонние средства или настраиваемые сценарии миграции для перехода на виртуальные машины на основе Cosmos DB, HDInsight или IaaS.

## <a name="considerations-and-guidance"></a>Рекомендации и рекомендации

При использовании DMS для переноса и модернизации данных важно понимать текущую платформу для размещения данных (источника), версии и будущей платформы и версии, которые наилучшим образом поддерживают гипотезу клиента (цель). Ниже приведен список исходных и целевых пар, которые можно проанализировать с помощью команды миграции. Каждый из них содержит выбор инструмента и ссылку на него на основе этих рекомендаций.

**Тип переноса:** При автономной миграции время простоя приложения начинается при запуске миграции. При использовании подключения к сети простой приложения ограничен только временем переключения в конце переноса. Мы рекомендуем понять, что такое приемлемое время простоя бизнеса и тестировать автономную миграцию, чтобы определить, соответствует ли это время восстановления. Если нет, выполните оперативную миграцию.

|Источник  |Выбор пути миграции  |Средство  |Тип миграции  |Руководство  |
|---------|---------|---------|---------|---------|
|SQL Server|Базы данных SQL Azure|DMS|Автономно|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Базы данных SQL Azure|DMS|В сети|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Управляемый экземпляр базы данных SQL Azure|DMS|Автономно|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Управляемый экземпляр базы данных SQL Azure|DMS|В сети|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server RDS|База данных SQL Azure (или Управляемый экземпляр)|DMS|В сети|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|База данных Azure для MySQL|DMS|В сети|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|База данных Azure для PostgreSQL|DMS|В сети|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|мондодб|Azure Cosmos DB API Mongo|DMS|Автономно|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Azure Cosmos DB API Mongo|DMS|В сети|[Руководство](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|Диапазон параметров PaaS & IaaS|Третья сторона или миграция Azure|Различные|[Дерево принятия решений](../../migrate/expanded-scope/data-oracle-migration.md)|
|Различные NoSQL баз данных|Параметры Космо DB или IaaS|Процедурная миграция или миграция Azure|Различные|[Дерево принятия решений](../../migrate/expanded-scope/data-no-sql-migration.md)|
