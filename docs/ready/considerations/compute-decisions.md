---
title: Решения по проектированию службы вычислений, готовой к работе в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Решения по проектированию службы вычислений, готовой к работе в Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bd31f07a24a17a50953eff54856118e9b22d054e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819391"
---
# <a name="compute-design-decisions"></a>Решения по проектированию службы вычислений

Определение требований к вычислениям для размещения рабочих нагрузок является ключевым моментом при подготовке к внедрению облачных вычислений. Вычислительные продукты и службы Azure поддерживают широкий спектр сценариев и возможностей для вычислительных рабочих нагрузок. Настройка среды зоны размещения для поддержки вычислительных требований, зависит от системы управления рабочей нагрузкой, технических и бизнес-потребностей.

## <a name="identify-compute-services-requirements"></a>Определение требований к службам вычислений

В процессе оценки и подготовки зоны размещения необходимо определить все вычислительные ресурсы, которые будут поддерживаться вашей зоной размещения. Этот процесс включает в себя оценку каждого приложения и службы, которые составляют рабочую нагрузку, чтобы определить требования к вычислениям и размещению. После определения и документирования своих требований можно создать политики для зоны размещения, чтобы проконтролировать, какие типы ресурсов разрешены, в зависимости от вашей рабочей нагрузки.

Для каждого приложения или службы, которые вы будете развертывать в среде зоны размещения, используйте следующее дерево принятия решений в качестве отправной точки, чтобы определить службы вычислений, которые нужно использовать.

![Дерево принятия решений для вычислительных служб Azure](../../_images/ready/compute-decision-tree.png)

> [!NOTE]
> Дополнительные сведения об оценке параметров службы вычислений для каждого приложения или службы см. в статье [Criteria for choosing a data store](/azure/architecture/guide/technology-choices/compute-overview) (Критерии выбора хранилища данных).

### <a name="key-questions"></a>Основные вопросы

Ответьте на следующие вопросы о рабочих нагрузках, которые помогут вам в принятии решения на основе дерева решений для служб вычислений Azure.

- **Создаете ли вы новые сетевые приложения и службы или переходите с существующих локальных рабочих нагрузок на другие?** Разработка новых приложений в рамках внедрения облачных вычислений позволяет в полной мере использовать преимущества современных облачных серверных технологий уже на этапе проектирования.
- **Если вы перемещаете существующие рабочие нагрузки, могут ли они воспользоваться преимуществами современных облачных технологий?** Перемещение локальных рабочих нагрузок требует выполнения анализа. Можете ли вы легко оптимизировать существующие приложения и службы, чтобы воспользоваться преимуществами современных облачных технологий, или подход *lift-and-shift* будет работать лучше для ваших рабочих нагрузок?
- **Могут ли приложения или службы воспользоваться преимуществами контейнеров?** Если приложения являются хорошими кандидатами для контейнерного размещения, можно воспользоваться преимуществами эффективности ресурса, масштабируемости и возможностей оркестрации, предоставляемых [Контейнерными службами Azure](https://azure.microsoft.com/product-categories/containers). Обе службы [Хранилище дисков Azure](/azure/virtual-machines/windows/managed-disks-overview) и [Файлы Azure](/azure/storage/files/storage-files-introduction) можно использовать для постоянного хранения приложений в контейнерах.
- **Основаны ли приложения на веб-интерфейсе или API и используют ли они PHP, ASP.NET, Node.js или похожие технологии?** Веб-приложения можно развертывать на управляемые экземпляры [Службы приложений Azure](/azure/app-service/overview), поэтому вам не нужно поддерживать работу виртуальных машин в целях размещения.
- **Необходим ли полный контроль над операционной системой и средой размещения рабочей нагрузки?** Если необходимо контролировать среду размещения, включая ОС, диски, локально запущенное программное обеспечение и другие конфигурации, вы можете использовать [Виртуальные машины Azure](https://azure.microsoft.com/services/virtual-machines) для размещения своих приложений и служб. Помимо выбора размеров и уровней производительности виртуальных машин, решения относительно виртуального хранилища дисков будут влиять на производительность и SLA, связанные с вашей рабочей нагрузкой на базе инфраструктуры как услуги (IaaS). Дополнительные сведения см. в документации по [Хранилищу дисков Azure](/azure/virtual-machines/windows/managed-disks-overview).
- **Будете ли вы работать с высокопроизводительными вычислительными возможностями (HPC)?** [Пакетная служба Azure](/azure/batch/batch-technical-overview) предоставляет возможности для планирования заданий и автоматического масштабирования вычислительных ресурсов в качестве службы платформы, тем самым упрощая выполнение масштабных параллельных и высокопроизводительных вычислительных приложений в облаке.
- **Будут ли приложения использовать архитектуру микрослужб?** Приложения, использующие архитектуру, основанную на микрослужбах, могут использовать преимущества нескольких оптимизированных технологий вычислений. Автономные, управляемые событиями рабочие нагрузки могут использовать [Функции Azure](/azure/azure-functions/functions-overview) для создания масштабируемых, бессерверных приложений, которые не нуждаются в инфраструктуре. Для приложений, требующих большего контроля над средой, в которой работают микрослужбы, можно использовать службы контейнеров, такие как [Экземпляры контейнеров Azure](/azure/container-instances/container-instances-overview), [Служба Azure Kubernetes](/azure/aks/intro-kubernetes) и [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).

> [!NOTE]
> Большинство служб вычислений Azure используются в сочетании с хранилищем Azure. Информацию о соответствующих решениях по хранению см. в [руководстве по принятию решений о хранении](./storage-guidance.md).

## <a name="common-compute-scenarios"></a>Распространенные сценарии вычислений

В следующей таблице приведено несколько распространенных сценариев использования и рекомендуемых служб вычислений для работы с ними.

| **Сценарий** | **Служба вычислений** |
| --- | --- |
| Мне нужно подготовить к работе виртуальные машины Linux и Windows в считанные секунды в любой удобной конфигурации. | [Виртуальные машины Azure](https://azure.microsoft.com/services/virtual-machines) |
| Мне нужно достичь высокой доступности путем автомасштабирования для создания тысяч виртуальных машин за считанные минуты. | [Масштабируемые наборы виртуальных машин](https://azure.microsoft.com/services/virtual-machine-scale-sets) |
| Мне нужно упростить развертывание, управление и работу Kubernetes. | [Служба Azure Kubernetes (AKS)](https://azure.microsoft.com/services/kubernetes-service) |
| Мне нужно ускорить разработку приложений с помощью управляемой событиями бессерверной архитектуры. | [Функции Azure](https://azure.microsoft.com/services/functions) |
| Мне нужно разработать микрослужбы и оркестрировать контейнеры в Windows и Linux. | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) |
| Мне нужно быстро создавать облачные приложения для Интернета и мобильных устройств, используя полностью управляемую платформу. | [Служба приложений Azure](https://azure.microsoft.com/services/app-service) |
| Мне нужно помещать приложения в контейнеры и легко запускать контейнеры с помощью одной команды. | [Экземпляры контейнеров Azure](https://azure.microsoft.com/services/container-instances); |
| Мне нужно планировать задания и управлять вычислительными ресурсами в облачном масштабе с возможностью масштабирования до десятков, сотен или тысяч виртуальных машин. | [Пакетная служба Azure](https://azure.microsoft.com/services/batch) |
| Мне нужно создавать облачные приложения с высоким уровнем доступности и масштабируемости, а также программные интерфейсы, которые позволят сконцентрироваться на приложениях, не заботясь об оборудовании. | [Oблачныe службы Azure2} |

## <a name="regional-availability"></a>Доступность в регионах

Azure позволяет доставлять службы в том масштабе, который необходим для охвата клиентов и партнеров  _где бы они ни находились_. Ключевым фактором при планировании развертывания облака является определение того, какой регион Azure будет размещать ресурсы рабочей нагрузки.

Некоторые функции вычислений, такие как Служба приложений Azure, обычно доступны в большинстве регионов Azure. Однако некоторые вычислительные службы поддерживаются только в выбранных регионах. Некоторые типы виртуальных машин и связанные с ними типы хранилищ имеют ограниченную региональную доступность. Прежде чем решить, в какие регионы необходимо развернуть вычислительные ресурсы, мы рекомендуем обратиться к странице [Страница регионов](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=azure-vmware-cloudsimple,cloud-services,batch,container-instances,app-service,service-fabric,functions,kubernetes-service,virtual-machine-scale-sets,virtual-machines) ,чтобы проверить последний статус региональной доступности.

Дополнительные сведения о глобальной инфраструктуре Azure, см. на  [странице регионов Azure](https://azure.microsoft.com/global-infrastructure/regions). Вы также можете просмотреть  [доступность продуктов по регионам](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) для получения сведений об общих службах, доступных в каждом регионе Azure.

## <a name="data-residency-and-compliance-requirements"></a>Местонахождение данных и соответствие требованиям

Юридические и договорные требования, связанные с хранением данных, часто будут применяться к рабочей нагрузке. Эти требования могут варьироваться в зависимости от местоположения организации, юрисдикции, в которой хранятся и обрабатываются файлы и данные, а также от применимого бизнес-сектора. Компоненты обязательств по данным, которые необходимо учитывать, включают классификацию данных, расположение данных и соответствующие обязанности для защиты данных в соответствии с моделью общей ответственности. Многие решения вычислений зависят от связанных ресурсов хранилища. Это требование также может повлиять на ваши решения по вычислениям. Дополнительные сведения об этих требованиях см. в техническом документе  [Achieving Compliant Data Residency and Security with Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure) (Выполнение требований к месту расположения и безопасности данных с помощью Azure).

Процесс обеспечения соответствия может включать контроль физического расположения вычислительных ресурсов. Регионы Azure объединены в группы, называемые географическими регионами.  [География Azure](https://azure.microsoft.com/global-infrastructure/geographies) гарантирует соблюдение требований к местонахождению, соответствию нормам и устойчивости в определенных географических и политических границах. Если на рабочие нагрузки распространяются независимость данных или другие требования соответствия, вы должны развернуть ресурсы хранилища в регионах в соответствующем географическом регионе Azure.

## <a name="establish-controls-for-compute-services"></a>Установка элементов управления для служб вычислений

При подготовке среды зоны размещения вы можете установить элементы управления, ограничивающие возможности развертывания ресурсов для каждого пользователя. Элементы управления помогут управлять затратами и ограничить риски безопасности, в то же время позволяя разработчикам и ИТ-специалистам развертывать и настраивать ресурсы, необходимые для поддержки рабочих нагрузок.

После определения и документирования требований вашей целевой зоны вы можете использовать [Политику Azure](/azure/governance/policy/overview) для управления ресурсами вычислений, которые позволено создавать пользователям. Элементы управления могут [разрешать или запрещать создание типов вычислительных ресурсов](/azure/governance/policy/samples/allowed-resource-types). Например, вы можете разрешить пользователям создавать только ресурсы Службы приложений Azure или Функций Azure. Вы можете также использовать политику для управления допустимыми параметрами при создании ресурса, например [для ограничения того, какие виртуальные машины SKU могут быть подготовлены](https://docs.microsoft.com/azure/governance/policy/samples/allowed-skus-storage) или [для разрешения только определенных образов виртуальных машин](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

Политика может быть масштабирована на ресурсы, группы ресурсов, подписки и группы управления. Вы можете включить свои политики в определения [Azure Blueprint](/azure/governance/blueprints/overview) и многократно применять их в своей облачной организации.
