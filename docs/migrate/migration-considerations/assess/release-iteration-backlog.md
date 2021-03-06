---
title: Невыполненная работа итерации и выпуска
description: Используйте платформу внедрения облачных технологий для Azure, чтобы научиться создавать итерации и невыполненные работы в выпусках для организации задач.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: internal
ms.openlocfilehash: aa0c464d187446d5c9d7baf249499cec278d042a
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101785450"
---
# <a name="manage-change-in-an-incremental-migration-effort"></a>Управление изменениями в процессе поэтапной миграции

В этой статье предполагается, что процессы миграции являются поэтапными и выполняются параллельно с [процессом управления](../../../govern/index.md). Тем не менее те же рекомендации можно использовать, чтобы определить начальные задачи в структурной декомпозиции работы для традиционных подходов каскадного управления изменениями.

## <a name="release-backlog"></a>Список невыполненных работ по выпуску

Список *невыполненных работ по выпуску* состоит из ряда ресурсов (виртуальных машин, баз данных, файлов и приложений), которые необходимо перенести, прежде чем можно будет выпустить рабочую нагрузку для использования в облаке. Во время каждой итерации команда по внедрению в облако документирует и оценивает усилия, необходимые для переноса каждого ресурса в облако. См. раздел "Невыполненная работа по итерации" ниже.

## <a name="iteration-backlog"></a>Список невыполненных работ по итерации

*Список невыполненных работ по итерации* — это подробный список работ, необходимых для переноса определенного числа ресурсов из существующих цифровых активов в облако. Записи в этом списке часто хранятся в качестве рабочих элементов в таком средстве гибкого управления, как Azure DevOps.

Перед началом первой итерации команда по внедрению в облако указывает длительность итерации (обычно от двух до четырех недель). Этот период времени важен для определения времени начала и окончания каждого набора утвержденных действий. Поддержание согласованных окон выполнения позволяет легко оценивать скорость (темпы миграции) и выполнять изменения в соответствии с изменяющимися бизнес-потребностями.

До каждой итерации команда рассматривает список невыполненных работ по выпуску, оценивая усилия и приоритеты ресурсов, которые необходимо перенести. Затем они утверждают определенное число согласованных миграций. После того как она будет согласована командой внедрения в облако, список действий становится *текущим невыполненной работой итерации*.

Во время каждой итерации члены команды работают вместе для выполнения обязательств в рамках текущего списка невыполненных работ по итерации.

## <a name="next-steps"></a>Дальнейшие действия

После того как невыполненная работа по итерации определена и принята командой по внедрению в облако, [утверждения на управление изменениями](./approve.md) могут быть завершены.

> [!div class="nextstepaction"]
> [Утверждение изменений архитектуры перед миграцией](./approve.md)
