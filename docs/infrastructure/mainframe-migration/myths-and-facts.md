---
title: Мифы и факты миграции мэйнфреймов
description: Научитесь отличать мифы от реальности к мэйнфреймам и оцените рабочие нагрузки мэйнфреймов, наиболее подходящие для Azure.
author: njray
ms.author: brblanch
ms.date: 12/27/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: think-tank
ms.openlocfilehash: 5c0a226143f62a08046382d59a58d4b34ca8282c
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102115039"
---
<!-- cSpell:ignore chargebacks IPLs -->

# <a name="mainframe-myths-and-facts"></a>Мифы и факты о мейнфрейме

Мейнфреймы занимают видное место в истории вычислительной техники и остаются жизнеспособными для высокоспециализированных рабочих нагрузок. Большинство согласятся с тем, что мэйнфреймы являются проверенной платформой с давно установленными операционными процедурами, которые делают их среды надежными и гибкими. Программное обеспечение выполняется на основе использования, которое измеряется в миллионах инструкций в секунду (MIPS), и подробные отчеты об использовании доступны для получения возмещений.

Надежность, доступность и вычислительная мощность мэйнфреймов приняли неслыханные масштабы. Чтобы оценить рабочие нагрузки мэйнфреймов, наиболее подходящие для Azure, сначала нужно отличить мифы от реальности.

## <a name="myth-mainframes-never-go-down-and-have-a-minimum-of-five-9s-of-availability"></a>Миф: большие ЭВМ никогда не выходят и имеют не менее пяти 9S доступности

Оборудование и операционные системы мэйнфреймов считаются надежными и стабильными. Но реальность заключается в том, что время простоя должно быть запланировано на обслуживание и перезагрузку, называемые начальной загрузкой программ (ИПЛС). При рассмотрении этих задач решение для мэйнфреймов часто имеет доступность, близкую к 99 % или 99,9 %, что эквивалентно высокопроизводительному серверу на базе Intel.

Мэйнфреймы также остаются такими же уязвимыми к повреждениям, как и любые другие серверы, поэтому им требуются системы бесперебойного питания (СБП) для устранения этих типов сбоев.

## <a name="myth-mainframes-have-limitless-scalability"></a>Миф: большие ЭВМ имеют неограниченную масштабируемость

Масштабируемость мэйнфрейма зависит от емкости системного программного обеспечения, например системы управления сведениями о клиентах (CICS), а также емкости новых экземпляров ядер и хранилища. Некоторые крупные компании, использующие мэйнфреймы, настроили свои CICS для производительности, а иначе бы они превысили возможности самых больших доступных мэйнфреймов.

## <a name="myth-intel-based-servers-are-not-as-powerful-as-mainframes"></a>Миф: серверы на базе Intel не так эффективны, как мэйнфреймы

Новые высокопроизводительные системы на базе процессоров Intel обладают такой же вычислительной мощностью, что и мэйнфреймы.

## <a name="myth-the-cloud-cant-accommodate-mission-critical-applications-for-large-companies-such-as-financial-institutions"></a>Миф: Облако не может поддерживать критически важные приложения для крупных компаний, таких как финансовые учреждения

Хотя могут существовать некоторые изолированные экземпляры, в которых облачные решения бывают короткими, обычно это обусловлено тем, что алгоритмы приложений не могут распространяться. Эти несколько примеров являются исключениями, а не правилом.

## <a name="summary"></a>Итоги

По сравнению с этим Платформа Azure предлагает альтернативную платформу, способную предоставлять эквивалентные функции и функции мэйнфрейма, а также значительно снизить затраты. Кроме того, Общая стоимость владения облачной моделью затрат на основе подписок гораздо дешевле, чем на мэйнфреймах.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Включение коммутатора с мэйнфреймов в Azure](./migration-strategies.md)
