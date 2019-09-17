---
title: Руководство по принятию решений о программно-конфигурируемой сети
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте о программно-конфигурируемых сетях, которые играют важнейшую роль при миграции в Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: bbe9815b12226c193073bff3c2298d4124034935
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023758"
---
# <a name="software-defined-networking-decision-guide"></a>Руководство по принятию решений о программно-конфигурируемой сети

Программно-конфигурируемая сеть (SDN) — это сетевая архитектура, поддерживающая функции виртуализированных сетей, которую можно централизованно администрировать, настраивать и изменять с помощью ПО. SDN позволяет создавать облачные сети с помощью виртуализированных эквивалентов физических маршрутизаторов, брандмауэров и других сетевых устройств, используемых в локальных сетях. SDN крайне важно использовать для создания защищенных виртуальных сетей на таких общедоступных облачных платформах, как Azure.

## <a name="networking-decision-guide"></a>Схема по принятию решений относительно сети

![Схема вариантов сети, отсортированных в порядке увеличения сложности, со ссылками для быстрого перехода](../../_images/decision-guides/decision-guide-software-defined-network.png)

Перейти к разделу: [Только PaaS](./paas-only.md) | [Облачная среда](./cloud-native.md) | [Сеть периметра в облаке](./cloud-dmz.md) [Гибридная среда](./hybrid.md) | [Звездообразная модель](./hub-spoke.md) | [Дополнительные сведения](#learn-more)

SDN предоставляет несколько вариантов различной стоимости и сложности. На представленной выше схеме кратко изложены эти варианты, чтобы вы могли быстро сопоставить их с конкретными технологическими и бизнес-стратегиями.

Важными факторами при выборе на основе этих рекомендаций являются несколько ключевых решений, которые приняла ваша команда по вопросам облачной стратегии, прежде чем принимать решения, касающиеся сетевой архитектуры. Наиболее важные ключевые решения связаны с [определением цифровых активов](../../digital-estate/index.md) и [проектом подписки](../subscriptions/index.md) (на которые также могут влиять решения об учете облачных затрат и глобальных маркетинговых стратегий).

Эти факторы не оказывают существенное влияние на небольшие развертывания в одном регионе (менее 1000 виртуальных машин). И наоборот, выбранный вариант SDN и описанные факторы могут в значительной степени определять скорость и сложность внедрения при наличии более чем 1000 виртуальных машин, нескольких подразделений или геополитических рынков.

## <a name="choosing-the-right-virtual-networking-architectures"></a>Выбор подходящих архитектур виртуальных сетей

Этот раздел дополняет схему по принятию решений, чтобы помочь вам выбрать подходящие архитектуры виртуальных сетей.

Реализовать технологии SDN для создания виртуальных сетей в облаке можно множеством способов. То, как вы структурируете виртуальные сети, используемые при миграции, и как эти сети взаимодействуют с вашей существующей ИТ-инфраструктурой, будет зависеть от сочетания требований к рабочим нагрузкам и системе управления.

При выборе архитектуры или сочетания архитектур виртуальных сетей во время планирования миграции в облако ответьте на следующие вопросы, чтобы определить правильное решение для вашей организации.

| Вопрос | "Только PaaS" | Облачная среда | Сеть периметра в облаке | Гибридная среда | Звездообразная модель |
|-----|-----|-----|-----|-----|-----|
| Будет ли ваша рабочая нагрузка использовать только службы PaaS и не требовать других сетевых возможностей, которые эти службы не предоставляют? | Yes | Нет | Нет | Нет | Нет |
| Требует ли рабочая нагрузка интеграции с локальными приложениями? | Нет | Нет | Yes | Да | Yes |
| Определили ли вы подходящие политики безопасности и установили ли безопасное подключение между локальными и облачными сетями? | Нет | Нет | Нет | Yes | Yes |
| Требуются ли для вашей рабочей нагрузки службы проверки подлинности, не поддерживаемые облачными службами идентификации, или вам нужен прямой доступ к локальным контроллерам доменов? | Нет | Нет | Нет | Yes | Yes |
| Нужно ли вам развертывать большое количество виртуальных машин и рабочих нагрузок и управлять ими? | Нет | Нет | Нет | Нет | Yes |
| Нужно ли вам обеспечивать централизованное управление и локальное подключение, делегируя контроль над ресурсами отдельным группам рабочих нагрузок? | Нет | Нет | Нет | Нет | Yes |

## <a name="virtual-networking-architectures"></a>Архитектуры виртуальных сетей

Ниже подробно описаны основные архитектуры программно-конфигурируемых сетей.

- **[Только PaaS](./paas-only.md).** Большинство решений платформы как услуги (PaaS) поддерживают ограниченный набор встроенных сетевых функций и могут не требовать явно определенной программно-конфигурируемой сети для поддержки требований к рабочей нагрузке.
- **[Облачная среда](./cloud-native.md).** Облачная архитектура поддерживает облачные рабочие нагрузки с использованием виртуальных сетей на основе программного обеспечения облачной платформы по умолчанию. При этом она не зависит от локальных или других внешних ресурсов.
- **[Сеть периметра в облаке](./cloud-dmz.md).** Это решение поддерживает ограниченный обмен данными между локальной и облачной сетью, защищенный с помощью реализации сети периметра для строгого контроля трафика между двумя средами.
- **[Гибридная среда](./hybrid.md).** Гибридная облачная сетевая архитектура обеспечивает двусторонний доступ между виртуальными сетями в доверенных облачных средах и локальными ресурсами.
- **[Звездообразная архитектура](./hub-spoke.md).** Позволяет централизованно управлять внешними подключениями и общими службами, изолировать отдельные рабочие нагрузки и преодолевать потенциальные ограничения на подписку.

## <a name="learn-more"></a>Подробнее

См. подробнее о программно-конфигурируемых сетях в Azure:

- [Что такое виртуальная сеть Azure?](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) В Azure основная возможность SDN предоставляется виртуальной сетью Azure, которая действует как облачный аналог физических локальных сетей. Виртуальные сети также выступают в качестве стандартной границы, изолирующей ресурсы на платформе.
- [Рекомендации Azure по обеспечению сетевой безопасности](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices). Рекомендации от группы безопасности Azure по настройке виртуальных сетей для минимизации уязвимостей безопасности.

## <a name="next-steps"></a>Дополнительная информация

Программно-конфигурируемая сеть — один из базовых компонентов инфраструктуры, решение о котором необходимо принять во время внедрения облачных решений. См. [общие сведения о принятии решений](../index.md), чтобы узнать об альтернативных шаблонах или моделях, используемых при принятии решений для других типов инфраструктуры.

> [!div class="nextstepaction"]
> [Руководства по принятию решений об архитектуре](../index.md)