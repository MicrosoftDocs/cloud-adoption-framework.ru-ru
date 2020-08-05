---
title: Реализация КАФных зон корпоративного масштаба в Azure
description: Проверьте параметры для реализации архитектуры корпоративного масштаба каф.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 164a52dc11673e454ff7ad63fc7c4ddc4617395d
ms.sourcegitcommit: 9662234674e663bc7d4bc134d303520cb146bd95
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/04/2020
ms.locfileid: "87560446"
---
# <a name="implement-caf-enterprise-scale-landing-zones-in-azure"></a>Реализация КАФных зон корпоративного масштаба в Azure

Если для бизнес-требований необходимо иметь обширную начальную реализацию зон с полностью интегрированным управлением, безопасностью и операциями в начале, используйте приведенные здесь примеры корпоративного масштаба. При таком подходе можно использовать портал Microsoft Azure или инфраструктуру в качестве кода для установки и настройки среды. Можно также переходить между порталом и инфраструктурой как кодом (рекомендуется), когда ваша организация готова.

## <a name="example-implementation"></a>Пример реализации

В таблице ниже приведены примеры модульных реализаций.

| Пример развертывания  | Описание  | Репозиторий GitHub | Развернуть в Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Корпоративный масштаб | Это рекомендуемая основа для внедрения корпоративного масштаба. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Развертывание примера в Azure](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fes-foundation.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fportal-es-foundation.json) |
| Виртуальная глобальная сеть корпоративного уровня | Добавьте модуль виртуальной глобальной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Развертывание примера в Azure](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fes-vwan.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fportal-es-vwan.json) |
| Центр и периферийное масштабирование предприятия | Добавление модуля концентратора и периферийной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) | <!-- [Deploy example to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkrnese%2FAzureDeploy%2Fmaint%2FARM%2Fdeployments%2Fe2e.json) --> Скоро выйдет |

## <a name="next-steps"></a>Дальнейшие действия

Эти примеры предоставляют простой вариант развертывания для поддержки непрерывного обучения подхода корпоративного масштабирования. Прежде чем использовать эти примеры в рабочей версии корпоративного уровня, сначала ознакомьтесь с [архитектурой корпоративного уровня](./architecture.md).
