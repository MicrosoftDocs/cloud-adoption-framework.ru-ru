---
title: Архитектура и шаблоны миграции Moodle
description: Узнайте о шаблонах Azure Resource Manager (ARM) для развертывания инфраструктуры Moodle Azure, а также о том, как развертывать или редактировать их.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: e36261c7021f970d4ca94903fe5260a7f787803f
ms.sourcegitcommit: 18f3ee8fcd8838f649cb25de1387b516aa23a5a0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2020
ms.locfileid: "96327859"
---
# <a name="moodle-migration-architecture-and-templates"></a>Архитектура и шаблоны миграции Moodle

Moodle миграция включает следующие задачи:

1. Разверните инфраструктуру Azure с помощью шаблонов Azure Resource Manager (ARM).
1. [Скачайте и установите AzCopy](migration-start.md#download-and-install-azcopy-on-the-controller-vm).
1. [Скопируйте архив резервной копии Moodle в экземпляр виртуальной машины контроллера](migration-start.md#copy-the-archive-to-the-controller-vm) в развертывании Azure Resource Manager.
1. [Перенесите приложение Moodle и конфигурацию](migration-start.md#import-the-moodle-database-to-azure).
1. [Настройте экземпляр контроллера Moodle и рабочие узлы](azure-infra-config.md).
1. [Настройте PHP и веб-сервер](azure-infra-config.md).

В этой статье описываются варианты инфраструктуры Azure Moodle и способы развертывания ресурсов Azure с помощью выбора шаблонов ARM.

## <a name="azure-infrastructure"></a>Инфраструктура Azure

На следующей схеме показан обзор ресурсов инфраструктуры Azure Moodle.

![Диаграмма, на которой показаны ресурсы инфраструктуры Azure.](images/architecture.png)

## <a name="arm-template-options"></a>Параметры шаблона ARM

Для развертывания ресурсов Moodle в Azure можно использовать полностью настраиваемый шаблон ARM или один из нескольких предварительно определенных шаблонов ARM. Полностью настраиваемое развертывание обеспечивает наибольшую гибкость и возможности развертывания. Полностью настраиваемый шаблон и готовые шаблоны можно найти в [репозитории Moodle GitHub](https://github.com/Azure/Moodle).

В стандартном шаблоне развертывания используется один из четырех предопределенных размеров Moodle: минимальный, короткий-средний, крупный или максимальный.

- Для *минимального развертывания* требуются только две виртуальные машины (ВМ), поэтому она работает с подпиской на бесплатную пробную версию Azure. В этом развертывании используется сетевая файловая система (NFS), MySQL и небольшой номер SKU веб-интерфейса виртуальной машины автомасштабирования с одним Виртуальное ядро. Этот шаблон имеет время быстрого развертывания в течение 30 минут.
  
  [![, Запускающего шаблон ARM для развертывания минимального Moodle.](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-minimal.json)

- *Развертывание Small-to-MID* поддерживает до 1 000 параллельных пользователей. В этом развертывании используется NFS, без высокой доступности и MySQL в восьми виртуальных ядер. Это развертывание не включает такие параметры, как кэш Elasticsearch или Redis.
  
  [![, Которая запускает шаблон ARM развертывания Small-to-MID Moodle.](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-small2mid-noha.json)

- *Большое развертывание с высоким уровнем доступности* поддерживает более 2 000 параллельных пользователей. В этом развертывании используются службы файлов Azure, MySQL с 16 виртуальных ядер и кэш Redis без других параметров, таких как Elasticsearch.
  
  [![, Которая запускает шаблон многоуровневого развертывания с высоким уровнем доступности Moodle.](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-large-ha.json)

- *Максимальное* развертывание использует службы файлов Azure, MySQL с наивысшим номером SKU, кэш Redis, Elasticsearch на трех виртуальных машинах и крупные размеры хранилища для дисков данных и баз данных.
  
  [![, Которая запускает максимальный шаблон Moodle развертывания.](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-maximal.json)

## <a name="deploy-the-template"></a>Развертывание шаблона

Развертывание одного из стандартных шаблонов ARM:

1. В предыдущем разделе нажмите кнопку **развернуть в Azure** для нужного развертывания. Это действие переведет вас на портал Azure.
   
1. На странице **пользовательское развертывание** в портал Azure заполните поля обязательная **Подписка**, **Группа ресурсов**, **регион** и **открытый ключ SSH** . Сведения о том, как добавить ключ SSH, см. в разделе [Создание нового ключа SSH и добавление его в ssh-agent](https://docs.github.com/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
   
   :::image type="content" source="images/custom-deployment.png" alt-text="Снимок экрана с экраном настраиваемого развертывания Azure для шаблона ARM для развертывания Moodle." border="false":::
   
1. Выберите **Проверить и создать**.

### <a name="edit-the-template"></a>Изменение шаблона

Стандартные шаблоны ARM развертывают следующие версии программного обеспечения по умолчанию:

- Ubuntu: 18,04 LTS
- PHP: 7,4
- Moodle: 3,8

Если локальные версии PHP и Moodle отличаются от предыдущих значений, обновите версии шаблонов, чтобы они совпадали, выполнив следующие действия.

1. В портал Azure на странице **Настраиваемое развертывание** шаблона ARM выберите **изменить шаблон**.
   
1. В разделе " **ресурсы** " шаблона в разделе " **Параметры**" добавьте параметры для версий Moodle и PHP.

   ```json
   "phpVersion":       { "value": "7.2" },
   "moodleVersion":    { "value": "MOODLE_38_STABLE"}
   ```
   
   Например, для Moodle 3,9 `moodleVersion` значение должно быть `MOODLE_39_STABLE` .
   
   :::image type="content" source="images/edit-template.png" alt-text="Снимок экрана, показывающий страницу изменения шаблона для шаблона ARM для развертывания Moodle." border="false":::
   
1. Щелкните **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия

Продолжайте [Moodle материалы по миграции](migration-resources.md) , чтобы получить сведения о ресурсах, которые шаблон ARM развертывает в Azure.
