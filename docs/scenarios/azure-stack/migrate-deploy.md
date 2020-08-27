---
title: Развертывание рабочих нагрузок в Azure Stack Hub
description: Узнайте, как развертывать рабочие нагрузки в центре обработки данных с помощью центра Azure Stack.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9b1cf8600bd0160f02de9bfd4532c189008b5322
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/26/2020
ms.locfileid: "88885445"
---
# <a name="deploy-workloads-to-azure-stack-hub"></a>Развертывание рабочих нагрузок в Azure Stack Hub

Используя Azure Stack, ваша организация может запустить собственный экземпляр Azure в своем центре обработки данных. Организации включают Azure Stack в свою облачную стратегию, так как они помогают им в обработке ситуаций, когда общедоступное облако не будет работать. Ниже перечислены три наиболее распространенные причины использования Azure Stack.

- Плохое сетевое подключение к общедоступному облаку.
- Нормативные или договорные требования.
- Серверные системы, которые не могут быть доступны в Интернете.

## <a name="infrastructure-as-a-service-deployment"></a>Инфраструктура как развертывание службы

Независимо от причины развертывания инфраструктуры как услуги (IaaS) развертывание в центр Azure Stack будет аналогично любому другому развертыванию IaaS. Пользователи часто считают IaaS только виртуальными машинами, но IaaS — это больше. При развертывании виртуальной машины в Azure или Azure Stack компьютер поставляется с программно-определяемой сетью, включая систему доменных имен, общедоступные IP-адреса, правила брандмауэра (также называемые группами безопасности сети) и многие другие возможности. При развертывании виртуальной машины также создаются диски для виртуальных машин в хранилище, определяемом программным обеспечением, с помощью хранилища BLOB-объектов Azure.

Более подробные инструкции по развертыванию виртуальных машин на Azure Stack см. в разделе [Общие сведения о Azure Stack COMPUTE](/azure-stack/user/azure-stack-compute-overview?view=azs-2002).

## <a name="platform-as-a-service-deployment"></a>Платформа как развертывание службы

В облаке все ресурсы "платформа как услуга" (PaaS) выполняются в какой-либо форме службы инфраструктуры, например виртуальной машине. Однако службы Azure маскируются эти серверные ресурсы так, чтобы их не было управлять ими. Маскировка и координация этих ресурсов инфраструктуры осуществляется с помощью Azure Resource Manager. Вы могли увидеть один аспект диспетчер ресурсов при развертывании в Azure с помощью шаблона Azure Resource Manager. Эти шаблоны указывают Azure, какой поставщик ресурсов требуется вызвать, и способ настройки ресурсов.

Когда облако работает в вашем центре обработки данных, администраторы концентраторов стеков должны быть в некоторой степени знакомы со слоями запутывания. Прежде чем пользователи или разработчики смогут использовать ресурс PaaS, администратору центра Azure Stack потребуется установить поставщик ресурсов из Marketplace. Эти поставщики ресурсов позволяют экземпляру центра Azure Stack реплицировать функции поставщика ресурсов Azure в экземпляре Stack. Дополнительные сведения о развертывании поставщиков ресурсов центра Azure Stack см. в статье [блогов по Azure Stack IaaS](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/).

## <a name="deploy-workloads"></a>Развертывание рабочих нагрузок

После того как администратор центра Azure Stack правильно настроил ваш экземпляр стека, миграция может продолжаться, как и в случае с большинством других усилий по миграции Azure. С помощью Azure Stack команда может выполнять любой из следующих типов миграции:

- [Ethereum блокчейн Network](/azure-stack/user/azure-stack-ethereum?view=azs-2002)
- [Обработчик AKS](/azure-stack/user/azure-stack-kubernetes-aks-engine-overview?view=azs-2002)
- [Azure Cognitive Services](/azure-stack/user/azure-stack-solution-template-cognitive-services?view=azs-2002)
- [Веб-приложение C# ASP.NET](/azure-stack/user/azure-stack-dev-start-howto-vm-dotnet?view=azs-2002)
- [Виртуальная машина Linux](/azure-stack/user/azure-stack-dev-start-howto-deploy-linux?view=azs-2002)
- [Веб-приложение Java](/azure-stack/user/azure-stack-dev-start-howto-vm-java?view=azs-2002)

## <a name="additional-considerations-during-migration"></a>Дополнительные рекомендации по миграции

Следующие статьи помогут команде во время миграции и модернизации:

- Службы [масштабируемости и доступности](https://azure.microsoft.com/blog/azure-stack-iaas-part-six/) , такие как оплата за использование, наборы доступности виртуальных машин, масштабируемые наборы ВМ, сетевые адаптеры, а также возможность добавлять виртуальные машины и диски и изменять их размер
- [Емкость хранилища](https://azure.microsoft.com/blog/azure-stack-iaas-part-3/), включая возможность загрузки и загрузки, а также записи и развертывания образов виртуальных машин.
- [Шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates) быстрого запуска Azure Stack Репозиторий GitHub
- [Шаблоны](https://github.com/Azure/Azure-QuickStart-Templates) быстрого запуска Azure Репозиторий GitHub

## <a name="next-steps"></a>Дальнейшие шаги

Рекомендации по конкретным элементам процесса внедрения облачных технологий см. в следующих статьях:

- [Система управления Azure Stack Hub](./govern.md)
- [Управление Azure Stack Hub](./manage.md)
