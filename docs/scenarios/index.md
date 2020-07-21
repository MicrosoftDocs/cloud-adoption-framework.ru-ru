---
title: Единый подход к внедрению технологий Azure
description: Используйте единый подход службы "Миграция Azure" для переноса и модернизации всех ИТ-портфелей.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: f8135b59ed583a2c790b1f78a6b1f940fe4a0acd
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451551"
---
<!-- docsTest:ignore "One Migration" -->
<!-- cSpell:ignore HANA -->

# <a name="one-migration-approach-to-migrating-the-it-portfolio"></a>Единый подход к миграции для переноса ИТ-портфеля

Как Azure, так и служба "Миграция Azure" хорошо известны как платформы для размещения технологий Майкрософт. Но вы, возможно, не знаете о возможности Azure поддерживать миграцию вне Windows и SQL Server. Сценарии миграции, охватываемые методикой, включают один и тот же набор согласованных правил и процессов для переноса технологий Майкрософт и сторонних производителей.

## <a name="migration-scenarios"></a>Сценарии миграции

Ниже описаны несколько сценариев, которые следуют той же итеративной методике миграции и модернизации.

![Модель миграции Cloud Adoption Framework](../_images/migrate/one-migrate.png)

### <a name="links-to-migration-scenarios"></a>Ссылки на сценарии миграции

| | | | |
|---------|---------|---------|---------|
| **Виртуальные машины** | [Виртуальные машины](../migrate/azure-best-practices/contoso-migration-rehost-vm.md) | [Серверы Linux](../migrate/azure-best-practices/contoso-migration-rehost-linux-vm.md) | [Виртуальные рабочие столы](./wvd/index.md) |
| **Приложения** | [ASP.NET](../migrate/azure-best-practices/contoso-migration-refactor-web-app-sql.md) | [Java](https://docs.microsoft.com/azure/java/migration-overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) | [PHP](../migrate/azure-best-practices/contoso-migration-refactor-linux-app-service-mysql.md) |
| **Data** | [SQL Server](../migrate/azure-best-practices/contoso-migration-rehost-vm-sql-managed-instance.md) | [Базы данных с открытым исходным кодом](../migrate/azure-best-practices/sql-migration.md) | Analytics |
| **Гибридный** | [Azure Stack](./azure-stack/index.md) | [VMware](../migrate/azure-best-practices/vmware-host.md) | |
| **Дополнительные сценарии** | [Безопасные рабочие нагрузки](../migrate/azure-best-practices/migrate-best-practices-security-management.md) | [Мейнфреймы](../infrastructure/mainframe-migration/index.md) | NetApp и SAP HANA |

## <a name="migrate-methodology"></a>Методика миграции

В каждом сценарии миграции при переносе существующих рабочих нагрузок в облако используются одни и те же последовательные процессы.

![Модель миграции Cloud Adoption Framework](../_images/migrate/methodology.png)

Структурируйте волны миграции, чтобы управлять выпусками нескольких рабочих нагрузок. Установив план внедрения облачных технологий и целевые зоны Azure с помощью этого плана и готовых методологий, вы сможете сформировать структуру своих волн миграции.

При каждой итерации следуйте методике миграции для оценки, развертывания и выпуска рабочих нагрузок. Чтобы изменить эти процессы в соответствии с конкретными сценариями, щелкните любой из перечисленных выше сценариев миграции.

## <a name="next-steps"></a>Дальнейшие действия

Если у вас нет конкретного сценария, начните с выполнения [четырехэтапного процесса миграции CAF](../migrate/index.md).
