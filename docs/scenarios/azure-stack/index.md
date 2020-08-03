---
title: Стратегический вариант запуска Azure в вашем центре обработки данных
description: Разверните Azure в своем центре обработки данных с помощью Azure Stack Hub.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 5b0f1e25f542a2e13403707ea5604ecc29159d66
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451586"
---
# <a name="strategic-option-to-run-azure-in-your-datacenter"></a>Стратегический вариант запуска Azure в вашем центре обработки данных

Корпорация Майкрософт использует подход с приоритетной ориентацией на облако. Приоритет заключается в том, чтобы переместить приложения и данные в одно или несколько облаков с поддержкой гипермасштабирования, включая глобальное облако Azure или национальные облака, ориентированные на определенный языковой стандарт, такие как Azure для Германии или Azure для государственных организаций. Azure Stack Hub действует в качестве другого экземпляра национального облака, управляемого клиентами в их собственных центрах обработки данных или используемого через поставщика облачных служб. Но Azure Stack Hub не поддерживает гипермасштабирование, и корпорация Майкрософт не публикует и не поддерживает соглашения об уровне обслуживания для Azure Stack Hub.

## <a name="understand-your-cloud-journey"></a>Основные сведения о переходе к облаку

У каждой организации уникальный путь к облаку, который зависит от ее истории, особенностей бизнеса, культуры и, что, возможно, наиболее важно, от отправной точки. Переход к облаку предоставляет множество возможностей, функций, средств, а также вариантов улучшения существующих и внедрения новых систем управления и операций и даже перепроектирования приложений для использования преимуществ облачных архитектур.

При планировании можно четко обозначить преимущества использования облака в рамках ИТ-стратегии и бизнес-стратегии. Но в процессе перехода могут определиться настолько же веские причины использовать облако в пределах собственного центра обработки данных, _по крайней мере на этом этапе_. Если перед вами стоят эти две, казалось бы, противоречащие друг другу задачи, вам не придется выбирать между ними. По сути, система Azure Stack Hub — это [инфраструктура как услуга (IaaS)](https://azure.microsoft.com/blog/azure-stack-iaas-part-one). Но кроме этого, она работает в качестве решения PaaS (платформа как услуга). Это позволяет запускать ряд служб Azure в собственном центре обработки данных.

## <a name="azure-stack-hub-in-your-strategy"></a>Включение Azure Stack Hub в вашу стратегию

Миграция с применением Azure Stack Hub предоставляет альтернативный подход к переносу используемых приложений, которые работают на физических серверах или на существующих платформах виртуализации. Перемещая эти рабочие нагрузки в среду IaaS Azure Stack Hub, команды могут воспользоваться преимуществами бесперебойных операций, самостоятельного развертывания, стандартизированных конфигураций оборудования и согласованности, обеспечиваемой Azure. При использовании Azure Stack Hub для модернизации или внедрения инноваций команды могут подготавливать приложения и рабочие нагрузки для использования всех преимуществ облака.

Следуя согласованным рекомендациям по внедрению облачных технологий Azure и Azure Stack Hub, можно применять одни и те же модели системы управления и операций к ресурсам в общедоступном облаке или в вашем собственном центре обработки данных. Azure Stack Hub использует ту же модель Azure Resource Manager, что и Azure. Это обеспечивает единое представление для управления всеми решениями.

## <a name="understand-the-differences"></a>Общие сведения о различиях

Между Azure и Azure Stack Hub есть несколько различий. Некоторые из них очень заметны, другие же видны только на поздних этапах реализации. Ниже описано несколько различий, которые следует учитывать:

- Azure обеспечивает почти неограниченную емкость. Система Azure Stack Hub работает на физическом оборудовании в вашем центре обработки данных, что приводит к ограничениям емкости.
- Версии API и механизмы проверки подлинности в Azure и Azure Stack Hub могут немного отличаться друг от друга.
- Отличия Azure Stack Hub связаны с тем, _кто_ именно работает с облаком, что влияет на уровень операций рабочей нагрузки.
- Необходимо учитывать то, с какой частью службы Azure Stack Hub работает оператор системы, так как он определяет, какую службу вызывает конечный клиент (PaaS или SaaS).

Другие отличия будут рассматриваться в других статьях по Azure Stack Hub на различных этапах жизненного цикла внедрения облачных технологий.

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Следующий шаг: интеграция этой стратегии в план внедрения облачных технологий

В указанных ниже статьях вы найдете рекомендации по конкретным этапам внедрения облачных технологий.

- [Планирование миграции с использованием Azure Stack Hub](./plan.md)
- [Подготовка среды](./ready.md)
- [Оценка рабочих нагрузок для использования Azure Stack Hub](./migrate-assess.md)
- [Развертывание рабочих нагрузок в Azure Stack Hub](./migrate-deploy.md)
- [Система управления Azure Stack Hub](./govern.md)
- [Управление Azure Stack Hub](./manage.md)