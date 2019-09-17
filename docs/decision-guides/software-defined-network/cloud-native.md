---
title: 'Программно определяемая сеть: Облачная среда'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Обсуждение виртуальных сетевых служб, встроенных в облако.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 1c30e57761b12d00617296fb3f9d5a87b8b6cce7
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828335"
---
# <a name="software-defined-networking-cloud-native"></a>Программно определяемая сеть: Облачная среда

Виртуальная сеть, собственная в облаке, является обязательной при развертывании ресурсов IaaS, таких как виртуальные машины, на облачную платформу. Необходимо предоставить доступ к виртуальным сетям из внешних источников, аналогичных Интернету. Эти типы виртуальных сетей поддерживают создание подсетей, правил маршрутизации, виртуальных брандмауэров и устройств управления трафиком.

Облачная виртуальная сеть не зависит от локальных или других необлачных ресурсов вашей организации для поддержки рабочих нагрузок, размещенных в облаке. Все необходимые ресурсы предоставляются либо самой виртуальной сетью, либо с помощью предложений управляемых PaaS.

## <a name="cloud-native-assumptions"></a>Исходные допущения в облаке

Развертывание виртуальной сети, встроенной в облако, предполагает следующее:

- Рабочие нагрузки, которые вы развертываете в виртуальной сети, не зависят от приложений или служб, которые доступны только из вашей локальной сети. Если они не предоставляют доступ к конечным точкам через общедоступный Интернет, то приложения и службы, размещенные внутри локальной среды, не могут использоваться ресурсами, размещенными на облачной платформе.
- Управление идентификацией и доступ рабочей нагрузки зависят от служб идентификации или серверов IaaS облачной платформы, которые размещены в облачной среде. Вам не нужно будет выполнять прямое соединение со службами идентификации, размещенными в локальном или другом внешнем расположении.
- Службам идентификации не требуется поддержка единого входа (SSO) с локальными каталогами.

Виртуальные сети, собственные в облаке, не имеют внешних зависимостей. Это упрощает процесс развертывания и настройки, и в результате эта архитектура часто является наилучшим выбором для экспериментов или других небольших автономных или быстро повторяющихся развертываний.

Дополнительные вопросы, которые следует учитывать при обсуждении облачной архитектуры виртуальных сетей, могут быть следующие:

- Имеющиеся рабочие нагрузки, предназначенные для работы в локальном центре обработки данных, могут нуждаться в обширной модификации, чтобы воспользоваться преимуществами облачных функций, например службы хранения или проверки подлинности.
- Управление собственными сетями в облаке осуществляется исключительно с помощью средств управления облачными платформами, и поэтому может привести к расхождениям управления и политики от существующих ИТ-стандартов по мере того, как будет продолжено время.

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о виртуальных сетях, машинных в облаке, в Azure см. в следующих статьях:

- [Планирование виртуальных сетей](/azure/virtual-network/virtual-network-vnet-plan-design-arm). Вновь созданные виртуальные сети Azure по умолчанию являются облачными. Используйте эти руководства для планирования, проектирования и развертывания виртуальных сетей.
- [Ограничения сети. сеть](/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits). Любая отдельная виртуальная сеть и подключенные ресурсы могут существовать только в рамках одной подписки и связываться ограничениями подписки.