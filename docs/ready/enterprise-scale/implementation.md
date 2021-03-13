---
title: Реализация корпоративных зон корпоративного масштаба в Azure для облачной инфраструктуры
description: Проверьте параметры, чтобы реализовать облачную платформу внедрения для архитектуры Azure корпоративного уровня.
author: JefferyMitchell
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 2d33b50eb9eaa46202091660f67762a946eb9db5
ms.sourcegitcommit: 36e85ac734b184de3f29884b744ea74c81ccc72b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2021
ms.locfileid: "103439718"
---
# <a name="implement-cloud-adoption-framework-enterprise-scale-landing-zones-in-azure"></a>Реализация корпоративных зон корпоративного масштаба в Azure для облачной инфраструктуры

Если бизнес-требования посвящены богатой первоначальной реализации зон с полностью интегрированной плоскостью управления, безопасности и эксплуатации с самого начала, используйте параметры примера корпоративного масштаба, перечисленные здесь. При таком подходе вы можете использовать портал Azure или инфраструктуру в качестве кода для установки и настройки среды Azure. Можно также переходить между порталом и инфраструктурой как кодом (рекомендуется), когда ваша организация готова.

## <a name="reference-implementation"></a>Эталонная реализация

В следующей таблице приведен пример реализации эталонных реализаций на основе рекомендованной архитектуры корпоративного масштаба.

| Пример развертывания | Описание | Репозиторий GitHub | Развернуть в Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Корпоративный масштаб | Это рекомендуемая основа для внедрения корпоративного масштаба. | [Пример в GitHub][GitHub-WingTip] | [![Кнопка DTA-Button-WingTip]][DTA-WingTip] |
| Центр и периферийное масштабирование предприятия | Добавление модуля концентратора и периферийной сети в фундамент предприятия. | [Пример в GitHub][GitHub-AdventureWorks] | [![DTA-кнопка-AdventureWorks]][DTA-AdventureWorks] |
| Виртуальная глобальная сеть корпоративного уровня | Добавьте модуль виртуальной глобальной сети в фундамент предприятия. | [Пример в GitHub][GitHub-Contoso] | [![Кнопка DTA — contoso]][DTA-Contoso] |

## <a name="next-steps"></a>Дальнейшие действия

Эти примеры предоставляют простой вариант развертывания для поддержки непрерывного обучения подхода корпоративного масштабирования. Прежде чем использовать эти примеры в рабочей версии корпоративного уровня, ознакомьтесь с архитектурой корпоративного масштаба.

> [!div class="nextstepaction"]
> [Обзор архитектуры корпоративного масштаба](./architecture.md)

<!-- The following section is used to store references to external images and links to reduce maintenance overhead and enable tooltips -->

[//]: # (*******************************)
[//]: # (ССЫЛКИ НА ВНЕШНИЕ ИЗОБРАЖЕНИЯ НИЖЕ)
[//]: # (*******************************)

Программа [dta-Button-WingTip]: https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true "развертывает эталонную реализацию Wingtip (Foundation) в Azure."
Программа [dta-Button-AdventureWorks]: https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true "развертывает эталонную реализацию AdventureWorks (гибридное подключение с помощью концентратора и периферийных серверов) в Azure."
[Кнопка dta-Button — Contoso]: https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true "deploy Contoso (гибридное подключение к виртуальной глобальной сети) в Azure."

[//]: # (**************************)
[//]: # (МЕТКИ ВНЕШНИХ ССЫЛОК НИЖЕ)
[//]: # (**************************)

[GitHub-WingTip]: https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md
[GitHub-AdventureWorks]: https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md
[GitHub-Contoso]: https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md

[DTA-WingTip]: https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fes-foundation.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fportal-es-foundation.json
[DTA-AdventureWorks]: https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fadventureworks%2FarmTemplates%2Fes-hubspoke.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fadventureworks%2FarmTemplates%2Fportal-es-hubspoke.json

[DTA-Contoso]: https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fes-vwan.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fportal-es-vwan.json
