---
title: Реализация корпоративных зон корпоративного уровня в Azure
description: Обзор параметров для реализации архитектуры корпоративного масштаба
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 83c95275b124e6a2fe5787ae3f33d6566c0303e9
ms.sourcegitcommit: 568037e0d2996e4644c11eb61f96362a402759ec
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/16/2020
ms.locfileid: "84800067"
---
# <a name="implement-enterprise-scale-landing-zones-in-azure"></a>Реализация корпоративных зон корпоративного уровня в Azure

Если для бизнес-требований необходимо иметь обширную первоначальную реализацию начальных зон с полностью интегрированным управлением, безопасностью и операциями в начале, корпорация Майкрософт предлагает использовать пример корпоративного масштаба на этой странице. Этот подход может использовать портал Microsoft Azure или инфраструктуру в качестве кода для установки и настройки среды. Можно также переходить между порталом и инфраструктурой как кодом (рекомендуется), когда ваша организация готова. Как и в случае с любым другим Microsoft Azure подходом "инфраструктура как код", вам потребуется Azure Resource Manager шаблоны и навыки GitHub.

## <a name="example-implementation"></a>Пример реализации

В таблице ниже приведены примеры модульных реализаций.

| Пример развертывания  | Описание  | Репозиторий GitHub | Развернуть в Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Корпоративный масштаб | Это рекомендуемая основа для внедрения корпоративного масштаба. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Развертывание примера в Azure](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzOps%2Fmain%2Ftemplate%2Fux-foundation.json) |
| Виртуальная глобальная сеть корпоративного уровня | Добавьте модуль виртуальной глобальной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Развертывание примера в Azure](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzOps%2Fmain%2Ftemplate%2Fux-vwan.json) |
| Центр и периферийное масштабирование предприятия | Добавление модуля концентратора и периферийной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) | <!-- [Deploy example to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkrnese%2FAzureDeploy%2Fmaint%2FARM%2Fdeployments%2Fe2e.json) --> Ожидается в ближайшее время |

## <a name="next-steps"></a>Дальнейшие действия

Приведенные выше примеры предоставляют простой вариант развертывания для поддержки непрерывного обучения подхода корпоративного масштабирования. Прежде чем использовать эти примеры в рабочей версии корпоративного уровня, сначала ознакомьтесь с [архитектурой корпоративного уровня](./architecture.md).
