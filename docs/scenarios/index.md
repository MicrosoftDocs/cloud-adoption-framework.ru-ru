---
title: Универсальная миграция для внедрения технологий Azure
description: Используйте единый подход службы "Миграция Azure" для переноса и модернизации всех ИТ-портфелей.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1fcc9914a2ba517598972c52dc9e286933d122d2
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572635"
---
<!-- docsTest:ignore "One Migration" -->
<!-- cSpell:ignore HANA -->

# <a name="the-one-migration-approach-to-migrating-the-it-portfolio"></a>Универсальная миграция для переноса ИТ-портфеля

Как Azure, так и служба "Миграция Azure" хорошо известны как платформы для размещения технологий Майкрософт. Но вы, возможно, не знаете о том, что Azure поддерживает миграцию, связанную не только с Windows и SQL Server. Сценарии *универсальной миграции*, описываемые в методологии миграции, предусматривают использование одного и того же набора согласованных правил и процессов для переноса технологий Майкрософт и сторонних производителей.

## <a name="migration-scenarios"></a>Сценарии миграции

На схеме и в таблице ниже представлено несколько сценариев в рамках единой методологии итеративной миграции для переноса и модернизации решений.

![Модель миграции Cloud Adoption Framework](../_images/migrate/one-migrate.png)

| | | | |
|---------|---------|---------|---------|
| **Виртуальные машины** | [Виртуальные машины](../migrate/azure-best-practices/contoso-migration-rehost-vm.md) | [Серверы Linux](../migrate/azure-best-practices/contoso-migration-rehost-linux-vm.md) | [Виртуальные рабочие столы](./wvd/index.md) |
| **Приложения** | [ASP.NET](../migrate/azure-best-practices/contoso-migration-refactor-web-app-sql.md) | [Java](/azure/java/migration-overview?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) | [PHP](../migrate/azure-best-practices/contoso-migration-refactor-linux-app-service-mysql.md) |
| **Data** | [SQL Server](../migrate/azure-best-practices/contoso-migration-rehost-vm-sql-managed-instance.md) | [Базы данных с открытым исходным кодом](../migrate/azure-best-practices/sql-migration.md) | Analytics |
| **Гибридный** | [Azure Stack](./azure-stack/index.md) | [VMware](../migrate/azure-best-practices/vmware-host.md) | |
| **Дополнительные сценарии** | [Безопасные рабочие нагрузки](../migrate/azure-best-practices/migrate-best-practices-security-management.md) | [Мейнфреймы](../infrastructure/mainframe-migration/index.md) | NetApp и SAP HANA |

## <a name="migration-methodology"></a>Методология миграции

В каждом из представленных выше сценариев миграции при перемещении в облако существующих рабочих нагрузок применяется один и тот же основной процесс.

![Модель миграции Cloud Adoption Framework](../_images/migrate/methodology.png)

В каждом сценарии вы будете структурировать циклы миграции для определения выпусков нескольких рабочих нагрузок. Установив план внедрения облачных технологий и целевые зоны Azure с помощью этого плана и готовых методологий, вы сможете сформировать структуру циклов миграции.

В ходе каждой итерации следуйте методологии миграции для оценки, развертывания и выпуска рабочих нагрузок. Чтобы изменить эти процессы в соответствии со сценариями своей организации, выберите любой из перечисленных выше сценариев миграции.

## <a name="next-steps"></a>Дальнейшие действия

Если у вас нет конкретного сценария, начните с [четырехэтапного процесса миграции Cloud Adoption Framework](../migrate/index.md).
