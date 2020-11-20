---
title: Реализация корпоративных зон корпоративного масштаба в Azure для облачной инфраструктуры
description: Проверьте параметры, чтобы реализовать облачную платформу внедрения для архитектуры Azure корпоративного уровня.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ee89c383640d0beb228caf3047d40701bf82148e
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/20/2020
ms.locfileid: "94997188"
---
# <a name="implement-cloud-adoption-framework-enterprise-scale-landing-zones-in-azure"></a>Реализация корпоративных зон корпоративного масштаба в Azure для облачной инфраструктуры

Если для бизнес-требований необходимо иметь обширную начальную реализацию зон с полностью интегрированным управлением, безопасностью и операциями в начале, используйте приведенные здесь примеры корпоративного масштаба. При таком подходе можно использовать портал Azure или инфраструктуру в качестве кода для установки и настройки среды. Можно также переходить между порталом и инфраструктурой как кодом (рекомендуется), когда ваша организация готова.

## <a name="example-implementation"></a>Пример реализации

В следующей таблице перечислены примеры модульных реализаций.

| Пример развертывания  | Описание  | Репозиторий GitHub | Развернуть в Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Корпоративный масштаб | Это рекомендуемая основа для внедрения корпоративного масштаба. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Развертывание примера в Azure](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fes-foundation.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fportal-es-foundation.json) |
| Виртуальная глобальная сеть корпоративного уровня | Добавьте модуль виртуальной глобальной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Развертывание примера в Azure](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fes-vwan.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fportal-es-vwan.json) |
| Центр и периферийное масштабирование предприятия | Добавление модуля концентратора и периферийной сети в фундамент предприятия. | [Пример в GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) |[Развертывание примера в Azure](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fadventureworks%2FarmTemplates%2Fes-hubspoke.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fadventureworks%2FarmTemplates%2Fportal-es-hubspoke.json) |

## <a name="next-steps"></a>Дальнейшие действия

Эти примеры предоставляют простой вариант развертывания для поддержки непрерывного обучения подхода корпоративного масштабирования. Прежде чем использовать эти примеры в рабочей версии корпоративного уровня, ознакомьтесь с [архитектурой корпоративного масштаба](./architecture.md).
