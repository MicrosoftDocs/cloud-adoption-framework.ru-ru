---
title: Развертывание рабочих нагрузок в центре Azure Stack
description: Узнайте, как развертывать рабочие нагрузки в центре обработки данных с помощью центра Azure Stack.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2e29dcf36d0da76d72187fb895f6108e7a9dd2b5
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452448"
---
# <a name="deploy-workloads-to-azure-stack-hub"></a>Развертывание рабочих нагрузок в центре Azure Stack

Azure Stack позволяет клиентам запускать свой собственный экземпляр Azure в своем центре обработки данных. Организации выбирают Azure Stack как часть своей облачной стратегии, так как они помогают им в обработке ситуаций, когда общедоступное облако не будет работать. Три наиболее распространенные причины использования Azure Stack обусловлены плохим сетевым подключением к общедоступному облаку, нормативными или контрактными требованиями или серверными системами, которые не могут быть доступны в Интернете.

## <a name="infrastructure-as-a-service-iaas-deployment"></a>Развертывание инфраструктуры как услуги (IaaS)

Независимо от причины развертывания развертывание в центр Azure Stack будет аналогично любому другому развертыванию IaaS. Пользователи часто считают, что IaaS — это просто виртуальные машины, но IaaS — еще больше. При развертывании виртуальной машины в Azure или Azure Stack компьютер поставляется с программно определенной сетью, включая DNS, общедоступные IP-адреса, правила брандмауэра (также называемые группами безопасности сети) и многие другие возможности. При развертывании виртуальной машины также создаются диски для виртуальных машин в определенном программном хранилище с помощью хранилища BLOB-объектов Azure.

Более подробные инструкции по развертыванию виртуальных машин на Azure Stack см. в разделе [Общие сведения о Azure Stack COMPUTE](https://docs.microsoft.com/azure-stack/user/azure-stack-compute-overview?view=azs-2002).

## <a name="platform-as-a-service-paas-deployment"></a>Развертывание платформы как услуги (PaaS)

В облаке все ресурсы PaaS выполняются в определенной форме службы инфраструктуры, например виртуальной машине. Однако службы Azure маскируются эти серверные ресурсы так, чтобы их не было управлять ими. Маскировка и координация этих ресурсов инфраструктуры осуществляется с помощью Azure Resource Manager. Вы могли увидеть один аспект диспетчер ресурсов при развертывании в Azure с помощью шаблона Azure Resource Manager. Эти шаблоны указывают Azure, какой поставщик ресурсов требуется вызвать, и способ настройки ресурсов.

Когда облако работает в вашем центре обработки данных, администраторам концентратора стеков придется немного познакомиться с уровнями запутывания. Прежде чем пользователи или разработчики смогут использовать ресурс PaaS, администратору центра Azure Stack потребуется установить поставщик ресурсов из Marketplace. Эти поставщики ресурсов позволяют экземпляру центра Azure Stack реплицировать функции поставщика ресурсов Azure в экземпляре Stack. Дополнительные сведения о развертывании поставщиков ресурсов центра Azure Stack см. в статье [блогов по Azure Stack IaaS](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/).

## <a name="deploy-workloads"></a>Развертывание рабочих нагрузок

После того как администратор центра Azure Stack правильно настроил ваш экземпляр стека, миграция может продолжаться, как и в случае с большинством других усилий по миграции Azure. Ниже приведены ссылки на несколько типов миграций, которые обычно выполняются для клиентов Azure Stack.

- [Ethereum блокчейн Network](https://docs.microsoft.com/azure-stack/user/azure-stack-ethereum?view=azs-2002)
- [Подсистема AKS](https://docs.microsoft.com/azure-stack/user/azure-stack-kubernetes-aks-engine-overview?view=azs-2002)
- [Azure Cognitive Services](https://docs.microsoft.com/azure-stack/user/azure-stack-solution-template-cognitive-services?view=azs-2002)
- [Веб-приложение C# ASP.NET](https://docs.microsoft.com/azure-stack/user/azure-stack-dev-start-howto-vm-dotnet?view=azs-2002)
- [Виртуальная машина Linux](https://docs.microsoft.com/azure-stack/user/azure-stack-dev-start-howto-deploy-linux?view=azs-2002)
- [Веб-приложение Java](https://docs.microsoft.com/azure-stack/user/azure-stack-dev-start-howto-vm-java?view=azs-2002)

## <a name="additional-considerations-during-migration"></a>Дополнительные рекомендации по миграции

Следующие статьи помогут команде во время миграции и модернизации:

- Службы [масштабируемости и доступности](https://azure.microsoft.com/blog/azure-stack-iaas-part-six/) , такие как оплата за использование, наборы доступности виртуальных машин, масштабируемые наборы виртуальных машины, сетевые адаптеры, а также возможность добавлять виртуальные машины и диски и изменять их размер.
- [Емкость хранилища](https://azure.microsoft.com/blog/azure-stack-iaas-part-3/), включая возможность отправки и загрузки, а также записи и развертывания образов виртуальных машин.
- [Шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates) быстрого запуска Azure Stack Репозиторий GitHub.
- [Шаблоны](https://github.com/Azure/Azure-QuickStart-Templates) быстрого запуска Azure Репозиторий GitHub.

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Следующий шаг. Интеграция этой стратегии в свое путешествие для внедрения в облако

Приведенный ниже список статей поможет вам найти рекомендации в конкретных точках в процессе внедрения в облако.

- [Управление центром Azure Stack](./govern.md)
- [Управление Azure Stack Hub](./manage.md)
