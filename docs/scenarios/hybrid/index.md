---
title: Введение в гибридные и многооблачные среды
description: Сведения о гибридных и многооблачных средах.
author: brianblanchard
ms.author: brblanch
ms.date: 01/11/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: e2e-hybrid
ms.openlocfilehash: a60c843f48c833620c1fbdd385bb27b071f12fb1
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101793130"
---
# <a name="introduction-to-hybrid-and-multicloud"></a>Введение в гибридные и многооблачные среды

Microsoft Azure предоставляет все продукты и компоненты, необходимые для создания и эксплуатации технологических решений в облаке. Мы также понимаем, что необходимость использования нескольких частных и (или) общедоступных облаков вызвана весомыми бизнес-причинами. В этой статье с описанием первого шага внедрения гибридной или многооблачной среды подробно рассказывается об уникальном взгляде корпорации Майкрософт на важные термины из сферы облачных вычислений.

## <a name="defining-hybrid-and-multicloud"></a>Определение гибридных и многооблачных сред

Гибридное облако — это тип облачных вычислений, сочетающих технологии частного облака (локальная инфраструктура) с технологиями общедоступного облака (вычислительные службы, предлагаемые сторонними поставщиками через общедоступную сеть Интернет). Гибридные облака позволяют согласованно перемещать данные и приложения между двумя облачными средами. Многие организации выбирают стратегию гибридного облака с учетом своих бизнес-требований, например соблюдения нормативных требований и требований к независимости данных, максимальной отдачи от технологических инвестиций в локальную среду или устранения проблем с задержкой.

Гибридное облако развивается и теперь включает в себя пограничные рабочие нагрузки. Пограничные вычислительные устройства, управляемые в облаке, позволяют пользоваться всеми вычислительными возможностями общедоступного облака в частном облаке, ближе к точкам подключения для устройств Интернета вещей, в том числе при обработке данных в приложениях, на подключенных устройствах и в мобильных потребительских службах. Благодаря снижению задержки путем перемещения рабочих нагрузок в облако устройства могут тратить меньше времени на обмен данными облаком и автономно выполнять операции в течение длительного времени. Повышенная доступность вычислительных ресурсов, хранилищ и служб позволяет разместить ресурсы и возможности взаимодействия с ними ближе к клиентам.

Многооблачными вычислениями называют использование вычислительных служб нескольких облаков от более чем одного поставщика облачных служб (в том числе частных и общедоступных облаков) в гетерогенной среде. Стратегия многооблачной среды обеспечивает повышенную гибкость и снижение рисков. Вы можете выбрать службы от разных поставщиков облачных служб, которые оптимально подходят для выполнения определенной задачи, или воспользоваться преимуществами служб, предлагаемых определенным поставщиком в конкретном расположении.

## <a name="hybrid-and-multicloud-narrative"></a>Интерпретация гибридных и многооблачных сред

В этом сценарии используется типичная интерпретация гибридных и многооблачных сред, а также приведены рекомендации по успешному внедрению облака в организации. Эта общая интерпретация не ограничивается одной методикой внедрения облака, а учитывает все этапы этого процесса.

Платформа гибридного облака предоставляет вашей организации множество преимуществ: повышенная гибкость, широкие возможности управления и масштабируемости, дополнительные варианты развертывания, глобальный масштаб, интегрированные кросс-платформенные средства безопасности, унифицированные средства для обеспечения соответствия, а также [повышенная производительность рабочих нагрузок, операций и экономичность](https://customers.microsoft.com/doclink/846315-ge-aviation-manufacturing-azure) в рамках всего предприятия, **что повышает отдачу от существующей инфраструктуры**. Если спрос на вычисления и возможности обработки изменяется, гибридное облако позволяет вам с легкостью вертикально масштабировать локальную инфраструктуру в общедоступное облако для недопущения перегрузки, не предоставляя при этом сторонним центрам обработки данных доступ ко всем вашим данным. Выполняя определенные рабочие нагрузки в облаке, организация получает все преимущества гибкости и инновационности общедоступного облака, сохраняя особо важные данные в собственном центре обработки данных для удовлетворения требований клиентов или для обеспечения соответствия нормативным требованиям.

Это позволяет вам масштабировать вычислительные ресурсы и при этом модернизировать и защитить [критически важные приложения и данные](https://azure.microsoft.com/solutions/business-critical-applications/). Вы можете устранить необходимость в значительных капитальных инвестициях для удовлетворения краткосрочных повышений спроса или в освобождении локальных ресурсов для более важных данных. При использовании моделей выставления счетов для облака ваша организация платит только за используемые ресурсы. Ей не нужно приобретать, программировать и поддерживать дополнительные ресурсы и оборудование, которые могут простаивать длительное время.

Еще одна строка капитальных издержек, которую можно ликвидировать, — это инвестиции в инфраструктуру аварийного восстановления и резервного копирования в сторонние расположения. Общедоступное облако для стратегий резервного копирования и аварийного восстановления представляет собой отличный выбор для таких локальных рабочих нагрузок и их данных, причем общедоступное облако никак не ограничивает их возможности. Благодаря использованию общедоступного облака для резервного копирования и восстановления клиенты получают доступ к эффективным системам для обеспечения конфиденциальности и безопасности, могут с легкостью выполнять масштабирование по запросу и ускорить скорость восстановления.

Компании используют одни и те же ресурсы в локальной среде, в различных облаках и на периферии. Клиенты часто говорят о таких четырех основных потребностях:

1. Доступ к данным о работоспособности всех существующих и будущих инфраструктур и приложений через единую панель управления.
2. Устранение сложностей, связанных с интеграцией локальных политик и обновлений с облачной инфраструктурой. Организации понимают необходимость в реализации стандарта управления.
3. Наличие специалистов с самыми разными навыками для работы с локальной и облачной средами, так как в организациях часто заняты разные команды разработки приложений. Клиенты нуждаются в согласованном взаимодействии между такими средами, чтобы обеспечить унификацию практик разработки.
4. Желание управлять состоянием безопасности без значительной модификации текущих операций. Облачная или многооблачная среда еще больше усложняют эту задачу, что может привести к снижению уровня доверия и появлению опасений.

Рассмотрите возможность развертывания облачных служб в гибридной и многооблачной среде. Под использованием облачных служб часто подразумевают только "перемещение данных и приложений в общедоступное облако". Гибридная стратегия обеспечивает полную поддержку операций клиента, которые делают невозможным использование общедоступного облака для некоторых рабочих нагрузок, например в сильно регулируемых отраслях, таких как правительственные инфраструктуры, здравоохранение и финансовые услуги. В зависимости от географического региона и требований к независимости данных, внутренние данные и данные клиента может потребоваться хранить строго в границах локальных центров обработки данных. Чувствительность к задержке данных вынуждает размещать вычислительные ресурсы близко к исходным данным в локальных центрах обработки данных, а прерывания подключений к Интернету при этом ожидаются или имеют критические последствия. В таких сценариях гибридные решения с облачными службами позволяют сократить расходы на управление (обслуживание таких служб в локальной среде), а также развернуть модель выставления счетов для облака с оплатой по мере использования в локальных центрах обработки данных.

## <a name="hybrid-and-multicloud-motivations"></a>Причины внедрения гибридных и многооблачных сред

Azure, как надежный поставщик облачных служб корпоративного уровня, поддерживает вас в достижении бизнес-целей с помощью общедоступного облака, гибридной или многооблачной среды. В этой серии рассматриваются различные лучшие методики, которые позволяют оптимально использовать среды с самым разным набором облаков — как сред, развернутых полностью в Azure, так и сред, которые минимально или совсем не используют инфраструктуру Azure.

Мы понимаем, что клиенты имеют множество веских причин для размещения своих цифровых активов в разных гибридных и многооблачных средах. Некоторые частые бизнес-факторы:

- необходимость минимизировать или не допустить привязку к одному поставщику облачных служб;
- подразделения, филиалы или приобретенные компании уже используют различные облачные платформы;
- разные поставщики облачных служб могут иметь в разных странах требования, относящиеся к соблюдению нормативных требований и независимости данных;
- необходимость повысить уровень непрерывности бизнес-процессов и аварийного восстановления путем дублирования рабочих нагрузок между двумя поставщиками облачных служб;
- необходимость повысить производительность путем выполнения приложений в среде, которая располагается максимально близко к пользователю, для чего может потребоваться внедрить гибридную или многооблачную среду;
- обеспечение простой миграции для некоторых платформ данных или отраслевых приложений путем реализации стратегий многооблачных среды.

## <a name="hybrid-and-multicloud-concerns"></a>Проблемы, касающиеся внедрения гибридных и многооблачных сред

Некоторые из приведенных выше факторов могут стать движущей силой бизнес-трансформации при наличии продуманной стратегии внедрения гибридной или многооблачной среды.

Для некоторых же требуется выполнить предварительную подготовку к развертыванию и обеспечить его последующую поддержку, чтобы организации могли в полной мере воспользоваться преимуществами инноваций. Например, компания может выбрать вариант с привязкой к поставщику облачных служб. Но если она хочет избежать такой привязки, ей необходимо будет смириться с некоторыми ограничениями при внедрении облака. Многие из самых эффективных продуктов и компонентов, предоставляемых поставщиками облачных служб, нельзя использовать в средах других поставщиков. Чтобы обеспечить переносимость данных и минимизировать привязку к поставщику, при внедрении облака организации часто бывают вынуждены ограничиться базовыми возможностями IaaS (инфраструктура как услуга) или вкладывать значительные инвестиции в использование облачных технологий, например контейнеров или Kubernetes.

После выпуска рабочих нагрузок и их запуска в рабочей среде часто возникает еще одно обстоятельство, связанное с развертыванием гибридной или многооблачной среды: если организации пытаются обеспечить поддержку управления операциями для рабочих нагрузок в новых средах, им приходится быстро адаптировать свой подход. Существующие платформы управления операциями (в том числе существующие политики и процессы управления операциями) не предназначены для таких сред. Пытаясь учесть все связанные с работой в облачной среде отклонения, компании часто прибегают к использованию разрозненных средств и практик, из-за чего расходы на операции увеличиваются пропорционально числу поддерживаемых сред.

## <a name="next-step-minimize-hybrid-and-multicloud-concerns-with-unified-operations"></a>Следующий шаг: минимизация проблем, возникающих при внедрении гибридных и многооблачных сред, с помощью унифицированных операций

Получите представление об унифицированных операциях, прежде чем приступать к внедрению гибридной или многооблачной среды. Согласованные практики по выполнению операций во всех облачных средах и общий уровень управления помогут избежать множества проблем, связанных с реализаций стратегий гибридных и многооблачных сред.

Определите, нужно ли вам дублировать операции для каждого поставщика облачных служб или реализовать [подход с использованием унифицированных операций при управлении облаком](./unified-operations.md), прежде чем вы начнете развертывать гибридную или многооблачную среду в большом масштабе.