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
ms.openlocfilehash: 32c05e04c224f88008ded6e9fe2c69bb6095d346
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828101"
---
# <a name="cost-management-tools-in-azure"></a>Средства управления затратами в Azure

[Управление затратами](./index.md) — это одна из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина сосредоточена на способах составления планов облачных расходов, распределения облачных бюджетов, мониторинга и реализации облачных бюджетов, выявления дорогостоящих аномалий и корректировки плана управления облаком, когда фактические расходы не совпадают.

Ниже приведен список собственных инструментов Azure, которые могут помочь в совершенствовании политик и процессов, поддерживающих эту дисциплину управления.

| Tool | [портал Azure](https://azure.microsoft.com/features/azure-portal)  | [Управление затратами Azure](/azure/cost-management/overview-cost-mgt)  | [Пакет содержимого Azure EA](/power-bi/service-connect-to-azure-enterprise)  | [Политика Azure](/azure/governance/policy/overview) |
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
