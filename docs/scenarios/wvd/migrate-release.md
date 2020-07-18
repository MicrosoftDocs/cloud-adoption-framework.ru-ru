---
title: Задачи, выполняемые после развертывания и выпуска виртуальных рабочих столов Windows
description: Используйте платформу внедрения облаков для Azure, чтобы изучить рекомендации по переносу виртуальных рабочих столов Windows, чтобы сократить сложность и стандартизировать процесс миграции.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4c5c4140bb5735706f8cefbb4f37cdc391601c75
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452357"
---
# <a name="windows-virtual-desktop-post-deployment"></a>Виртуальные рабочие столы Windows после развертывания

Процесс выпуска экземпляров виртуальных рабочих столов Windows для миграции или развертывания относительно прост. Этот процесс отражает тот, который использовался при проверке [концепции виртуальных рабочих столов Windows](./proof-of-concept.md):

- Протестируйте производительность и задержку групп приложений и развернутые настольные компьютеры для выборки пользователей.
- Подключите конечных пользователей, чтобы обучить их, как подключиться через:
  - [Настольный клиент Windows](https://docs.microsoft.com/azure/virtual-desktop/connect-windows-7-and-10)
  - [Веб-клиент](https://docs.microsoft.com/azure/virtual-desktop/connect-web)
  - [Клиент Android](https://docs.microsoft.com/azure/virtual-desktop/connect-android)
  - [Клиент macOS](https://docs.microsoft.com/azure/virtual-desktop/connect-macos)
  - [Клиент iOS](https://docs.microsoft.com/azure/virtual-desktop/connect-ios)

## <a name="post-deployment"></a>После развертывания

После завершения выпуска часто добавляйте [ведение журналов и диагностику для лучшей эксплуатации виртуальных рабочих столов Windows](https://docs.microsoft.com/azure/virtual-desktop/diagnostics-log-analytics#push-diagnostics-data-to-your-workspace). Кроме того, для рабочих групп можно подключить узлы в составе poold и настольных компьютеров к [рекомендациям управления сервером Azure](../../manage/azure-server-management/index.md) для управления отчетами, исправлениями и BCDR конфигурациями.

Хотя в этом сценарии миграции не хватает области, процесс выпуска может привести к необходимости переноса дополнительных рабочих нагрузок в Azure во время последующих итераций миграции. Если вы еще не настроили Office 365 или Azure AD, группа может выбрать подключение к этим службам при выпуске сценариев рабочего стола. Для гибридной операционной модели группы эксплуатации могут также выбрать интеграцию Intune, System Center или других средств управления конфигурацией, улучшающих операции, соответствие требованиям и безопасность.

## <a name="next-step-your-next-migration-iteration"></a>Следующий шаг: Следующая итерация миграции

После завершения миграции виртуальных рабочих столов Windows группа по внедрению в облако может начать следующую миграцию для конкретного сценария. Кроме того, если есть дополнительные рабочие столы для переноса, эту серию статей можно использовать снова, чтобы попытаться перейти к следующей миграции или развертыванию виртуальных рабочих столов Windows.

- [Планирование миграции или развертывания виртуальных рабочих столов Windows](./plan.md)
- [Проверка среды или начальных зон Azure](./ready.md)
- [Завершение концепции эксперимента с виртуальными рабочими столами Windows](./proof-of-concept.md)
- [Оценка миграции или развертывания виртуальных рабочих столов Windows](./migrate-assess.md)
- [Развертывание или миграция экземпляров виртуальных рабочих столов Windows](./migrate-deploy.md)
- [Выпуск развертывания виртуальных рабочих столов Windows в рабочей среде](./migrate-release.md)
