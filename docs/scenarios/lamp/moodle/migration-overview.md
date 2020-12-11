---
title: Обзор миграции Moodle вручную
description: Ознакомьтесь с предварительными требованиями и общими действиями для ручного переноса Moodle из локальной среды в Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 659c1a151bd1f6d908737c6be5ab0177f361b2f1
ms.sourcegitcommit: d19b0fc9ef37bf1060fe7595cd2be1612a43ea4a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2020
ms.locfileid: "96605427"
---
# <a name="overview-of-moodle-manual-migration"></a>Обзор миграции Moodle вручную

[Moodle](https://moodle.org/) — это бесплатная система управления обучением с открытым исходным кодом, написанная на PHP. В этом руководство объясняется, как перенести развертывание Moodle из локальной среды в Azure. В этом руководстве описаны два разных подхода, которые используют портал Azure или интерфейс командной строки Azure (Azure CLI).

## <a name="prerequisites"></a>Предварительные требования

Перед началом миграции вам понадобятся следующие компоненты:

- Локальное программное обеспечение обновлено и исправлено до следующих версий:
  - Ubuntu 18.04 LTS
  - Nginx 1.14.
  - Сервер базы данных MySQL 5.6, 5.7 или 8.0. В этом руководством используется база данных Azure для MySQL.
  - PHP 7.2, 7.3 или 7.4.
  - Moodle 3,8 или 3
- Веб-сайт Moodle настроен в **режим обслуживания**.
- Доступ к локальной инфраструктуре для [резервного копирования развертывания и конфигураций Moodle](migration-pre.md#back-up-on-premises-data), включая конфигурации баз данных.
- [Azure CLI](migration-pre.md#install-the-azure-cli) и [AzCopy](migration-pre.md#download-and-install-azcopy) , установленные локально.
- Создана [Подписка Azure](migration-pre.md#create-a-subscription) и [учетная запись хранилища BLOB-объектов Azure](migration-pre.md#create-a-storage-account) .

## <a name="moodle-migration-process"></a>Процесс миграции Moodle

Миграция Moodle с помощью шаблона Azure Resource Manager (ARM) создает инфраструктуру в Azure, а затем переносит стек программного обеспечения Moodle и связанные с ним зависимости.

Шаги миграции Moodle в Azure делятся на следующие три этапа:

1. [Подготовка к миграции](migration-pre.md)
1. [Перенос приложений](migration-start.md)
1. [Действия после миграции](migration-post.md)

## <a name="next-steps"></a>Дальнейшие действия

Перейдите к [процедуре подготовки к Moodle миграции](./migration-pre.md).