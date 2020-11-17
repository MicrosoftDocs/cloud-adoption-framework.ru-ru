---
title: Moodle задачи миграции, архитектура и шаблон
description: Сведения о задаче и архитектуре, а также о шаблонах, участвующих в Moodle миграции.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: f3e5d88e894289e615ac0573d6c640832b8ed028
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714756"
---
# <a name="moodle-migration-tasks-architecture-and-template"></a>Moodle задачи миграции, архитектура и шаблон

## <a name="moodle-migration-task-outline"></a>Структура задачи миграции Moodle

Moodle миграция включает следующие задачи:

- Разверните инфраструктуру Azure с помощью шаблонов Azure Resource Manager.
- Скачайте и установите AzCopy.
- Скопируйте резервный архив в экземпляр виртуальной машины контроллера из Azure Resource Manager развертывания.
- Миграция приложения и конфигурации Moodle.
- Настройте экземпляр контроллера Moodle и рабочие узлы.
- Настройка PHP и веб-сервера.

## <a name="deploy-azure-infrastructure-with-azure-resource-manager-templates"></a>Развертывание инфраструктуры Azure с помощью шаблонов Azure Resource Manager

- При использовании шаблона Azure Resource Manager для развертывания инфраструктуры в Azure доступны несколько вариантов. На следующей схеме представлен обзор ресурсов инфраструктуры.

![Ресурсы инфраструктуры Azure.](images/architecture.png)

Полностью настраиваемое развертывание обеспечивает большую гибкость и возможности для развертывания. Стандартный размер развертывания использует один из четырех предопределенных размеров Moodle. Четыре стандартных шаблона — минимальный, короткий, крупный и максимальный, и они доступны в [репозитории Moodle GitHub](https://github.com/Azure/Moodle).

- [Минимальное](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-minimal.json): в этом развертывании будет использоваться служба NFS, MySQL и меньшего размера автомасштабирования виртуальных машин веб-интерфейса (один Виртуальное ядро), что обеспечит более быстрое время развертывания (менее 30 минут). в настоящее время для подписки Azure на бесплатную пробную версию потребуется только две виртуальные машины.

- [Small-to-MID](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-small2mid-noha.json): поддерживает до 1 000 одновременных пользователей. Это развертывание будет использовать NFS (без высокой доступности) и MySQL (восемь виртуальных ядер) без других параметров, таких как эластичный Поиск или кэш Redis.

- [Крупный (высокий уровень доступности)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-large-ha.json): поддерживает более 2 000 одновременных пользователей. В этом развертывании будут использоваться службы файлов Azure, MySQL (16 виртуальных ядер) и кэш Redis, а не другие параметры, такие как эластичный Поиск.

- Максимум. в этом [максимальном](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-maximal.json)развертывании будут использоваться службы файлов Azure, MySQL с наивысшим номером SKU, кэш Redis, эластичный Поиск (три виртуальные машины) и крупные размеры хранилища (как для дисков данных, так и для баз данных).

Выберите **запустить** , чтобы развернуть любой из предопределенных шаблонов. Это позволит вам направить вас на портал Azure, где потребуется выполнить обязательные поля, такие как **Подписка**, **Группа ресурсов**, [**ключ SSH**](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)и **регион**.

![Пользовательское развертывание: развертывание из пользовательского шаблона.](images/custom-deployment.png)

Предыдущие предопределенные шаблоны будут развертывать версии по умолчанию.

```bash
Ubuntu: 18.04-LTS
PHP: 7.4
Moodle: 3.8
```

Если версии PHP и Moodle задержкой с локальной средой, обновите версии, выполнив следующие действия.

- На странице **Настраиваемое развертывание** выберите **изменить шаблон** .

![Изменение шаблона: изменение шаблона Azure Resource Manager.](images/edit-template.png)

- В разделе **Resources** добавьте версии Moodle и филиппинскому в блок **Parameters** .

    ```json
    "phpVersion":       { "value": "7.2" },
    "moodleVersion":    { "value": "MOODLE_38_STABLE"}
    ```

- Для Moodle 3,9 значение должно быть `MOODLE_39_STABLE` .

- Выберите **Сохранить**, чтобы сохранить изменения.

## <a name="next-steps"></a>Следующие шаги

Перейдите к [Moodle Resources](./migration-resources.md) , чтобы получить дополнительные сведения о процессе миграции Moodle.
