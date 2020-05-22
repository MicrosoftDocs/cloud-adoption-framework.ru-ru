---
title: Средства и шаблоны
description: Найдите средства и шаблоны, доступные в облачной инфраструктуре внедрения, чтобы ускорить внедрение облачных технологий.
author: JanetCThomas
ms.author: janet
ms.date: 04/14/2020
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.topic: article
ms.openlocfilehash: 3968e453eb89a0f00d7fd23eeec90fb6a947cd05
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756062"
---
<!-- cSpell:ignore Terraform's -->

# <a name="tools-and-templates"></a>Средства и шаблоны

Инфраструктура внедрения в облако включает средства, помогающие быстро реализовать технические изменения. Используйте эти средства, шаблоны и оценки для ускорения внедрения в облако. Следующие ресурсы могут помочь при каждом этапе внедрения. Некоторые средства и шаблоны можно использовать на нескольких этапах.

## <a name="strategy"></a>Стратегия

| Ресурс | Описание |
|----------|-------------|
| [Средство отслеживания перехода в облако](https://docs.microsoft.com/assessments/?mode=pre-assessment&id=cloud-journey-tracker) | Определите путь перехода к облаку с учетом потребностей своего бизнеса. |
| [&nbsp;Шаблон стратегии и &nbsp; плана &nbsp;](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) | Документирование решений при выполнении стратегии и плана внедрения в облако. |

## <a name="plan"></a>Планирование

| Ресурс | Описание |
|----------|-------------|
| [Средство отслеживания перехода в облако](https://docs.microsoft.com/assessments/?mode=pre-assessment&id=cloud-journey-tracker) | Определите путь перехода к облаку с учетом потребностей своего бизнеса. |
| [&nbsp;Шаблон стратегии и &nbsp; плана &nbsp;](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) | Документирование решений при выполнении стратегии и плана внедрения в облако. |
| [Генератор планов внедрения в облако](../plan/template.md) | Стандартизация процессов путем развертывания невыполненной работы для [Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/what-is-azure-boards) с помощью шаблона плана внедрения в облако. |

## <a name="ready"></a>Ready

| Ресурс | Описание |
|----------|-------------|
| [Контрольный список готовности](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/ready/readiness-checklist.docx) | Этот контрольный список используется для подготовки среды к внедрению, включая подготовку первой целевой зоны миграции, персонализацию схемы и ее расширение. |
| [Шаблон отслеживания именования и маркировки](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) | Документирование решений о стандартах именования и маркировки для обеспечения согласованности и сокращения времени адаптации. |
| [&nbsp;Проект КАФ Foundation &nbsp;](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Используйте упрощенную реализацию первоначальной системы управления, чтобы обеспечить практический опыт работы с инструментами управления в Azure. |
| [Схема КАФ миграции на главную зону](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone) | Подготавливайте и подготавливайте рабочие нагрузки узла, перенесенные из локальной среды в Azure. Дополнительные сведения об этом проекте см. [в статье развертывание целевой зоны миграции](../ready/landing-zone/migrate-landing-zone.md). |
| [Схема Terraformной зоны](../ready/landing-zone/terraform-landing-zone.md) | База кода с открытым исходным кодом для terraform версии схем целевой зоны каф. |
| [Реестр terraform](https://registry.terraform.io/search?q=aztfmod) | Веб-сайт реестра terraform с фильтрацией для перечисления всех модулей инфраструктуры внедрения в облаке, необходимых для создания целевой зоны terraform. |

## <a name="govern"></a>Управление

| Ресурс | Описание |
|----------|-------------|
| [Оценка производительности управления](https://cafbaseline.com) | Определите расхождения между текущим состоянием и бизнес-приоритетами, а также получите доступ к ресурсам, которые позволят устранить эти расхождения. |
| [&nbsp;Проект КАФ Foundation &nbsp;](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Упрощенная реализация начального руководства для предоставления практических опыта работы с инструментами управления в Azure. |
| [Шаблон процесса управления](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Governance%20Discipline%20Template.docx) | Определите базовый набор процессов управления, используемый для реализации каждой дисциплины управления. |
| [Шаблон процесса управления затратами](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Cost%20Management%20Discipline%20Template.docx) | Определите инструкции политики и руководство по проектированию, которые позволят вам развить облачное управление в Организации с целью сосредоточиться на управлении затратами. |
| [Шаблон процесса ускорения развертывания](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Deployment%20Acceleration%20Discipline%20Template.docx) | Определите инструкции политики и руководство по проектированию, которые позволят вам развить облачное управление в Организации с помощью ускорения развертывания. |
| [Шаблон процесса идентификации](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Identity%20Baseline%20Discipline%20Template.docx) | Определите инструкции политики и руководство по проектированию, которые позволят вам развить облачное управление в Организации, чтобы сосредоточиться на требованиях к идентификации. |
| [Шаблон процесса согласованности ресурсов](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Resource%20Consistency%20Discipline%20Template.docx) | Определите инструкции политики и руководство по проектированию, которые позволят вам развить управление облаком в Организации, чтобы сосредоточиться на согласованности ресурсов. |
| [Шаблон базового процесса безопасности](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Security%20Baseline%20Discipline%20Template.docx) | Определите инструкции политики и руководство по проектированию, которые позволят вам развить управление облаком в Организации, чтобы сосредоточиться на базовых показателях безопасности. |

## <a name="manage"></a>Управление

| Ресурс | Описание |
|----------|-------------|
| [Microsoft Azure хорошо спроектированная проверка](https://docs.microsoft.com/assessments/?id=azure-architecture-review) | Эта оперативная оценка поможет определить архитектуру рабочей нагрузки и параметры операций. |
| [&nbsp; &nbsp; Исходный &nbsp; код рекомендаций](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/manage/Automation-Best-Practices) | Этот развертываемый исходный код дополняет и ускоряет внедрение рекомендаций для служб управления сервером Azure. Используйте этот исходный код, чтобы быстро включить управление операциями и установить базовый план операций. |
| [Книга Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) | Документирование решений об управлении операциями в облаке и обеспечение взаимодействия с бизнесом для обеспечения соответствия требованиям соглашения об уровне обслуживания, инвестиций в устойчивость и распределении бюджета, связанных с операциями. |

## <a name="organize"></a>Организация

| Ресурс | Описание |
|----------|-------------|
| [Схема RACI в разных командах](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) | Скачайте и измените шаблон электронной таблицы RACI, чтобы принимать решения организационной структуры с течением времени. |
