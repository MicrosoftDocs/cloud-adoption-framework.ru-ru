---
title: Реализация корпоративных зон корпоративного масштаба в Azure для облачной инфраструктуры
description: Проверьте параметры, чтобы реализовать облачную платформу внедрения для архитектуры Azure корпоративного уровня.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 238dd2621349cf396eda9ff3ff2c075f3475ced4
ms.sourcegitcommit: d31a9043d1ae9283ed126bf118ca26d1d18d6948
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/10/2020
ms.locfileid: "88040870"
---
# <a name="implement-cloud-adoption-framework-enterprise-scale-landing-zones-in-azure"></a>Реализация корпоративных зон корпоративного масштаба в Azure для облачной инфраструктуры

Если для бизнес-требований необходимо иметь обширную начальную реализацию зон с полностью интегрированным управлением, безопасностью и операциями в начале, используйте приведенные здесь примеры корпоративного масштаба. При таком подходе можно использовать портал Azure или инфраструктуру в качестве кода для установки и настройки среды. Можно также переходить между порталом и инфраструктурой как кодом (рекомендуется), когда ваша организация готова.

## <a name="example-implementation"></a>Пример реализации

В следующей таблице перечислены примеры модульных реализаций.

| Пример развертывания  | Description  | Репозиторий GitHub | Развертывание в Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Корпоративный масштаб | Это рекомендуемая основа для внедрения корпоративного масштаба. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Развертывание примера в Azure](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fes-foundation.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fportal-es-foundation.json) |
| Виртуальная глобальная сеть корпоративного уровня | Добавьте модуль виртуальной глобальной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Развертывание примера в Azure](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fes-vwan.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fportal-es-vwan.json) |
| Центр и периферийное масштабирование предприятия | Добавьте сетевой модуль Hub-лучевой в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) | <!-- [Deploy example to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkrnese%2FAzureDeploy%2Fmaint%2FARM%2Fdeployments%2Fe2e.json) --> Скоро выйдет |

## <a name="next-steps"></a>Дальнейшие действия

Эти примеры предоставляют простой вариант развертывания для поддержки непрерывного обучения подхода корпоративного масштабирования. Прежде чем использовать эти примеры в рабочей версии корпоративного уровня, ознакомьтесь с [архитектурой корпоративного масштаба](./architecture.md).
