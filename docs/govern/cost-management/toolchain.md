---
title: Средства управления затратами в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Средства управления затратами в Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 230e36d1ca59c208109eedbbdf7466f6373f4b00
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029294"
---
# <a name="cost-management-tools-in-azure"></a>Средства управления затратами в Azure

[Управление затратами](./index.md) — это одна из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина сосредоточена на способах составления планов облачных расходов, распределения облачных бюджетов, мониторинга и реализации облачных бюджетов, выявления дорогостоящих аномалий и корректировки плана управления облаком, когда фактические расходы не совпадают.

Ниже приведен список собственных инструментов Azure, которые могут помочь в совершенствовании политик и процессов, поддерживающих эту дисциплину управления.

| Tool | [портал Azure](https://azure.microsoft.com/features/azure-portal)  | [Управление затратами Azure](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Пакет содержимого Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Политика Azure](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Соглашение Enterprise требуется?     | Нет         | Нет         | Да         | Нет         |
|Управление бюджетом     | Нет         | Да         | Нет         | Да         |
|Отслеживание затрат на отдельном ресурсе    | Да         | Да         | Да         | Нет         |
|Отслеживание затрат на нескольких ресурсах    | Нет         | Да        | Да         | Нет         |
|Контроль затрат на отдельном ресурсе     | Да (изменение размера вручную)         | Да         | Нет         | Да         |
|Применение затрат для нескольких ресурсов    | Нет         | Да         | Нет         | Да         |
|Принудительное применение метаданных учета для ресурсов    | Нет         | Нет         | Нет         | Да         |
|Отслеживание и выявление тенденций     | Да (ограничено)         | Да        | Да         | Нет         |
|Обнаружение аномалий в затратах     | Нет         | Да        | Да         | Нет        |
|Социализация отклонений     | Нет        | Да        | Да        | Нет        |
