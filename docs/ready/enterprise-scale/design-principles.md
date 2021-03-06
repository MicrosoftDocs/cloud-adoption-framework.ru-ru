---
title: Принципы проектирования облачного развертывания инфраструктуры корпоративного внедрения
description: Узнайте о принципах проектирования корпоративного масштаба в инфраструктуре внедрения Microsoft Cloud для Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 0e1d7d0ef9c58836e57a6d3e325087e15676bf2d
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447189"
---
# <a name="cloud-adoption-framework-enterprise-scale-design-principles"></a>Принципы проектирования облачного развертывания инфраструктуры корпоративного внедрения

Архитектура корпоративного масштаба, указанная в этом руководстве, основана на принципах разработки, описанных здесь. Эти принципы служат в качестве компаса для последующих решений по проектированию в критических технических областях. Ознакомьтесь с этими принципами, чтобы лучше понять их влияние и компромиссы, связанные с их несоблюдением.

## <a name="subscription-democratization"></a>Демократизация подписки

Подписки следует использовать как единицу управления и масштаба с учетом потребностей и приоритетов бизнеса для поддержки бизнес-областей и владельцев портфелей, чтобы ускорить миграцию приложений и разработку новых приложений. Подписки должны предоставляться подразделениям для поддержки проектирования, разработки и тестирования новых рабочих нагрузок и миграции рабочих нагрузок.

## <a name="policy-driven-governance"></a>Система управления на основе политик

Политика Azure предоставляет границы и обеспечивает постоянное соответствие требованиям для платформы организации и развернутых на ней приложений. Политика Azure также предоставляет владельцам приложений достаточную свободу и безопасный неограниченный путь к облаку.

## <a name="single-control-and-management-plane"></a>Единая плоскость контроля и управления

Архитектура корпоративного уровня не должна учитывать все уровни абстракции, такие как разработанные клиентами порталы или инструменты. Она должна обеспечивать согласованную работу как для AppOps (централизованно управляемые группы эксплуатации), так и для DevOps (выделенные группы эксплуатации приложений). Azure предоставляет единую и согласованную плоскость управления для всех ресурсов Azure и каналов подготовки с доступом на основе ролей и элементами управления на основе политик. Azure можно использовать для создания стандартизированного набора политик и элементов управления для всех ресурсов организации.

## <a name="application-centric-and-archetype-neutral"></a>Ориентация на приложения и независимость от архетипа

Архитектура корпоративного уровня должна сосредоточиться на миграции и разработке на уровне приложений, а не на чистом переносе инфраструктуры методом lift-and-shift, например миграции виртуальных машин. Не следует проводить различия между старыми и новыми приложениями или приложениями, предоставляемыми в рамках инфраструктуры как услуги или платформы как услуги. В конечном итоге вы должны создать безопасную основу для всех типов приложений, которые будут развернуты на платформе Azure.

## <a name="align-azure-native-design-and-roadmaps"></a>Согласование собственной структуры и планов развития Azure

Подход к архитектуре корпоративного уровня по возможности направлен на использование собственных служб и возможностей платформы Azure. Этот подход должен быть согласован с планами развития платформы Azure, чтобы обеспечить доступность новых возможностей в ваших средах. Планы развития платформы Azure помогут вам выстроить эффективную стратегию миграции и траекторию движения в масштабе организации.

## <a name="recommendations"></a>Рекомендации

Будьте готовы пожертвовать определенными функциями, ведь маловероятно, что в первый же день вам понадобится все сразу. Используйте предварительные версии служб и опирайтесь на планы развития, чтобы обойти технические помехи.
