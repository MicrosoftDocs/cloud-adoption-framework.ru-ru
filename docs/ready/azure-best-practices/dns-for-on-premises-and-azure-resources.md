---
title: DNS для локальной среды и Azure
description: Изучите ключевые вопросы и рекомендации по проектированию DNS для локальных и Microsoft Azure.
author: JefferyMitchell
ms.author: brblanch
ms.date: 02/18/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 5a3793322e66892d314b6291fd83d75a3bcbe932
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101797998"
---
# <a name="dns-for-on-premises-and-azure-resources"></a>DNS для локальных и ресурсов Azure

Служба доменных имен (DNS) является важнейшим разделом разработки в общей архитектуре корпоративного масштаба. Некоторым организациям может потребоваться использовать существующие вложения в DNS. Другие могут видеть внедрение облака как возможность модернизировать свою внутреннюю инфраструктуру DNS и использовать собственные возможности Azure.

**Рекомендации по проектированию:**

- Вы можете использовать сопоставитель DNS в сочетании с Azure Частная зона DNS для разрешения имен в нескольких локальных средах.

- Вам может потребоваться использовать существующие решения DNS в локальной среде и Azure.

- Максимальное число частных зон DNS, с которыми виртуальная сеть может связаться с автоматической регистрацией, — это один из них.

- Максимальное число частных зон DNS, с которыми может быть связана виртуальная сеть, — 1 000 без автоматической регистрации.

**Рекомендации по проектированию:**

- Для сред, где разрешение имен в Azure является обязательным, используйте Частная зона DNS Azure для разрешения. Создайте делегированную зону для разрешения имен (например, `azure.contoso.com` ).

- Для сред, где требуется разрешение имен в Azure и локальную среду, используйте существующую инфраструктуру DNS (например, Active Directory интегрированную службу DNS), развернутую по крайней мере на двух виртуальных машинах (ВМ). Настройте параметры DNS в виртуальных сетях, чтобы использовать эти DNS-серверы.

- Вы по-прежнему можете связать зону Частная зона DNS Azure с виртуальными сетями и использовать DNS-серверы в качестве гибридных арбитров конфликтов с условным перенаправлением в локальные DNS-имена, такие как `onprem.contoso.com` , с помощью локальных DNS-серверов. Вы можете настроить локальные серверы с условными пересылками на виртуальные машины сопоставителя в Azure для зоны Частная зона DNS Azure (например, `azure.contoso.com` ).

- Особые рабочие нагрузки, требующие и развертывающие собственные DNS (например, Red Hat OpenShift), должны использовать предпочтительное решение DNS.

- Включите автоматическую регистрацию для Azure DNS, чтобы автоматически управлять жизненным циклом записей DNS для виртуальных машин, развернутых в виртуальной сети.

- Используйте виртуальную машину как сопоставитель для междоменного разрешения имен DNS с помощью Azure Частная зона DNS.

- Создайте зону Частная зона DNS Azure в глобальной подписке с подключением. Вы можете создать другие зоны Частная зона DNS Azure (например, `privatelink.database.windows.net` или `privatelink.blob.core.windows.net` для частной связи Azure).