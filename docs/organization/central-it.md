---
title: Центральные ИТ — возможности
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Узнайте о формировании централизованных ИТ.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: e6f9048ea6d7f9ae30fcf25c5058286f3b2b82ce
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908492"
---
# <a name="central-it-capabilities"></a>Центральные ИТ — возможности

Как и в случае внедрения в облако, самостоятельные возможности управления облаком могут быть недостаточно, чтобы управлять усилиями по внедрению. При постепенном переходе группы, как правило, разрабатывают навыки и процессы, необходимые для подготовки облака к работе с течением времени.

Однако если одна из облачных групп внедрения использует облако для достижения бизнес-результата с высоким уровнем профилирования, постепенное внедрение редко бывает случайным. Успешное завершение. Это также справедливо для внедрения в облако, но это происходит в масштабе облака. Когда внедрение облачных технологий расширяется от одной группы к нескольким командам в течение относительно короткого периода времени, требуется дополнительная поддержка от существующих ИТ-специалистов. Однако эти сотрудники могут не иметь возможности обучения и опыта, необходимых для поддержки облака с помощью собственных облачных средств ИТ. Это часто управляет обработкой Центральной ИТ-группы, управляющей облаком.

> [!CAUTION]
> Хотя это и является распространенным этапом зрелости, он может представлять высокий риск для внедрения, потенциально блокируя инновации и усилия по миграции, если это не так эффективно. Ознакомьтесь с разделом "риск" ниже, чтобы узнать, как уменьшить риск того, что в процессе централизации будет антишаблон культуры.

## <a name="possible-sources-for-central-it-expertise"></a>Возможные источники для Центральной ИТ – специалистов

Навыки, необходимые для предоставления централизованных ИТ, могут предоставлять следующие возможности:

- Существующая Центральная группа ИТ
- Корпоративные архитекторы
- Операции ИТ
- Управление ИТ
- ИТ-инфраструктура
- Сети
- идентификации
- Виртуализация
- Непрерывность бизнес-процессов и аварийное восстановление
- Владельцы приложений в ИТ

> [!WARNING]
> Центральное ИТ-подсеть следует применять только в облаке, если существующая доставка в локальной среде основана на центральной ИТ-модели. Если текущая локальная модель основана на делегированном контроле, рассмотрите возможность использования облачного центра (Ккое) для более совместимой альтернативы.

## <a name="key-responsibilities"></a>Основные обязанности

Адаптировать существующие ИТ-методики, чтобы убедиться в том, что усилия по переходу приводят к хорошо управляемым, хорошо контролируемым средам в облаке.

Следующие задачи обычно выполняются регулярно:

### <a name="strategic-tasks"></a>Стратегические задачи

- Эксперт
  - [результаты бизнеса](../business-strategy/business-outcomes/index.md)
  - [финансовые модели](../business-strategy/financial-models.md)
  - [мотивации для внедрения в облако](../business-strategy/motivations-why-are-we-moving-to-the-cloud.md)
  - [бизнес-риски](../governance/policy-compliance/risk-tolerance.md)
  - [рационализация цифрового пространства](../digital-estate/overview.md)
- Отслеживайте планы внедрения и ход выполнения по приоритетной невыполненной [миграции](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Выявление и определение приоритетов изменений платформы, необходимых для поддержки невыполненной работы миграции.
- Выступают в качестве промежуточного или переводного слоя между потребностями внедрения облака и существующими ИТ группами.
- Используйте существующие ИТ группы для ускорения возможностей платформы и включения внедрения.

### <a name="technical-tasks"></a>Технические задачи

- Создавайте и обслуживайте облачную платформу для поддержки решений.
- Определение и реализация архитектуры платформы.
- Работа с облачной платформой и управление ею.
- Постоянно улучшайте платформу.
- Придерживайтесь новых нововведений в облачной платформе.
- Доставьте новые облачные возможности для поддержки создания ценности бизнеса.
- Предложить решения самообслуживания.
- Убедитесь, что решения соответствуют существующим требованиям к управлению и соответствию.
- Создание и проверка развертывания архитектуры платформы.
- Ознакомьтесь с планами выпуска для источников новых требований к платформе.

## <a name="meeting-cadence"></a>Ритмичность собрания

Центральная ИТ-специалист обычно поступает от рабочей группы. Предполагаю, что участники зафиксированы много ежедневных расписаний для выравнивания усилий. Вклады не ограничиваются собраниями и циклами обратной связи.

## <a name="central-it-risks"></a>Центральные ИТ – риски

Каждая из облачных возможностей и этапов зрелости организации имеет префикс "Cloud". Центральная ИТ — единственное исключение. Центральная ИТ стала очень распространенной, когда все ИТ-активы могут быть размещены в нескольких местах, под управлением небольшого количества команд и управляются с помощью единой платформы управления операциями. Глобальные бизнес-методики и цифровая экономичность значительно снижают количество экземпляров этих централизованно управляемых сред.

В современном представлении ИТ – ресурсы глобально распределены. Обязанности делегируются. Управление операциями доставляется смесью внутреннего персонала, поставщиков управляемых услуг и поставщиков облачных служб. В цифровом подходе методики ИТ-управления переходят в модель самообслуживания и делегированный контроль с четким снятие, чтобы обеспечить управление. Центральная ИТ-компания может быть ценным участником внедрения облачных технологий, стать облачным брокером и партнером для инноваций и гибкости бизнеса.

Центральная ИТ как функция хорошо размещается для получения ценных знаний и рекомендаций из существующих локальных моделей и применения этих методов к облачной доставке. Однако этот процесс потребуется изменить. Новые процессы, новые навыки и новые средства необходимы для поддержки внедрения в облако в масштабе. Когда Центральная ИТ адаптируется, он станет важным партнером в отношении внедрения в облако. Однако если Центральная ИТ не адаптируется к облаку или пытается использовать облако в качестве Catalyst для мелких элементов управления, Центральная ИТ быстро превращается в блок для внедрения, внедрения инноваций и миграции.

Меры этого риска — это скорость и гибкость. Облако упрощает внедрение новых технологий. Если новые возможности облака можно развернуть в течение нескольких минут, а центральная ИТ-подразделение будет добавлять в процесс развертывания недели или месяцы, то эти централизованные процессы становятся серьезным препятствием для успеха бизнеса. При обнаружении этого индикатора Рассмотрите альтернативные стратегии доставки ИТ-услуг.

### <a name="exceptions"></a>Исключения

Во многих отраслях требуется жесткое соблюдение требований сторонних производителей. Некоторые требования соответствия по-прежнему требуют централизованного управления ИТ. Доставка по этим показателям соответствия может добавить время для процессов развертывания, особенно для новых технологий, которые не использовались широко. В этих сценариях следует задерживать задержки при развертывании на ранних этапах внедрения. Аналогичные ситуации существуют для компаний, которые работают с конфиденциальными данными клиентов, но могут не контролироваться требованием соответствия сторонних разработчиков.

### <a name="operating-within-the-exceptions"></a>Работа в исключениях

Если требуются централизованные ИТ-процессы, и эти процессы создают соответствующие контрольные точки при внедрении новых технологий, эти инновации по-прежнему можно быстро устранить. Требования к управлению и соответствию требованиям предназначены для защиты конфиденциальных данных, а не для защиты всех элементов. Облако предоставляет простые механизмы для получения и развертывания изолированных ресурсов с сохранением надлежащих снятие.

Зрелая Центральная ИТ-группа обеспечивает необходимые средства защиты, но согласовывает приемы, позволяющие внедрять инновации. Демонстрация этого уровня зрелости зависит от правильной классификации и изоляции ресурсов.

### <a name="example-narrative-of-operating-within-exceptions-to-empower-adoption"></a>Пример описания работы внутри исключений для повышения производительности

В этом примере демонстрируется подход, выполняемый зрелой Центральной группой ИТ для повышения производительности.

Contoso LLC использует центральную ИТ-модель для поддержки облачных ресурсов бизнеса. Для реализации этой модели у них реализованы тесные элементы управления для различных общих служб, таких как входящие сетевые подключения. Это пошаговое движение снижает уязвимость облачной среды и предоставляет единое устройство с разделением для блокировки всего трафика в случае нарушения. Их базовые политики безопасности имеют состояние, что весь входящий трафик должен проходить через общее устройство, управляемое Центральной ИТ-группой.

Однако одной из своих групп по внедрению в облако теперь требуется среда с выделенным и специально настроенным входящим сетевым подключением, чтобы использовать определенную облачную технологию. Незрелая Центральная ИТ группа просто отказали запрос и расставит приоритеты для существующих процессов по мере необходимости. Центральная ИТ-группа компании Contoso отличается. Они быстро выявили простое решение из четырех частей для этого дилеммой: Классификация, согласование, изоляция и автоматизация.

**Обновлений** Так как группа внедрения в облако находилась на ранних стадиях создания нового решения и не имеет конфиденциальных данных или важных потребностей в поддержке, активы в среде были классифицированы как низкий риск и некритические. Эффективная классификация — это знак зрелости на центральном ИТ. Классификация всех ресурсов и сред обеспечивает более четкие политики.

**Переговоры** Только классификация недостаточна. Общие службы были реализованы для согласованной работы с важными и критически важными ресурсами. Изменение правил приведет к нарушению политик управления и соответствия требованиям, предназначенных для ресурсов, которым требуется более надежная защита. Предоставление возможности внедрения не может быть связано с затратами на стабильность, безопасность или управление. Это привело к согласованию с группой внедрения, чтобы ответить на определенные вопросы. Может ли группа DevOps, управляющая бизнесом, могла предоставлять управление операциями для этой среды? Требуется ли этому решению прямой доступ к другим внутренним ресурсам? Если команда по внедрению в облако хорошо работает с этими компромиссами, трафик входящего трафика может быть возможным.

**Isolation** Так как бизнес может предоставлять собственное управление операциями, а так как решение не зависит от прямого трафика к другим внутренним ресурсам, его можно блокируютсять в новой подписке. Эта подписка также добавляется в отдельный узел новой иерархии группы управления.

**Автоматизация** — Еще один знак зрелости этой команды — их принципы автоматизации. Группа использует политику Azure для автоматизации принудительного применения политик. Они также используют схемы Azure для автоматизации развертывания общих компонентов платформы и соблюдения требований к определенному базовому показателю удостоверения. Для этой подписки и других пользователей в новой группе управления политики и шаблоны немного отличаются. Политики, блокирующие пропускную способность, были ликвидированы. Они были заменены требованиями для маршрутизации трафика через подписку общих служб, как и любой входящий трафик, для обеспечения изоляции трафика. Поскольку локальные средства управления операциями не могут получить доступ к этой подписке, агенты для этого средства больше не требуются. Все остальные снятие управления, необходимые для других подписок в иерархии группы управления, по-прежнему применяются, обеспечивая достаточный снятие.

Развитый творческий подход к центральной ИТ-отделу компании Contoso предоставил решение, которое не нарушает управление или соответствие требованиям, но оно по-прежнему было рекомендуется. Этот подход к работе с брокерами, а не от собственных подходов, направленных в облако, — это первый шаг к созданию полноценного облачного центра (Ккое). Применение этого подхода для быстрой эволюции существующих политик позволяет централизованно управлять, когда это необходимо, а управление снятие, когда приемлема гибкость. Балансировка этих двух факторов снижает риски, связанные с центральным ИТ в облаке.

## <a name="next-steps"></a>Следующие шаги

По мере того, как ИТ-отдел работает в облаке, следующий этап погашения обычно является слабой присоединением [облачных операций](./cloud-operations.md). Доступность собственных средств управления операциями в облаке и снижение эксплуатационных расходов на решения PaaS, как правило, приводят к бизнес-группам (или, точнее, DevOpsным командам в организации), предполагая ответственность за облачные операции.

> [!div class="nextstepaction"]
> [Возможности облачных операций](./cloud-operations.md)