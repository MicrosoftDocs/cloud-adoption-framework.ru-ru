---
title: Рационализация облака
description: Сведения о согласовании в облаке. процесс оценки активов для определения лучшего способа переноса или модернизировать каждого ресурса в облаке.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: internal
ms.openlocfilehash: 3885cda1a320b52c3f66e780a1f9bca5e84a8adb
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101787745"
---
# <a name="cloud-rationalization"></a>Рационализация облака

Рациональное определение облачных ресурсов — это процесс оценки активов для определения лучшего способа переноса или модернизировать каждого ресурса в облаке. Дополнительные сведения о процессе рационализации см. [в разделе что такое цифровое пространство?](./index.md).

## <a name="rationalization-context"></a>Контекст рациональности

*Пять RS* , приведенные в этой статье, являются отличным способом пометки потенциального будущего состояния для любой рабочей нагрузки, которая считается облачным кандидатом. Этот процесс пометки должен быть переведен в правильный контекст, прежде чем вы попытаетесь рационализировать среду. Чтобы предоставить этот контекст, ознакомьтесь со следующим мифы:

### <a name="myth-its-easy-to-make-rationalization-decisions-early-in-the-process"></a>Миф: простые решения по обоснованиям можно легко сделать на ранних этапах процесса

 Точная рационализация требует глубокого знания рабочей нагрузки и связанных ресурсов (приложений, инфраструктуры и данных). Самое важное, точное решение по рациональному обоснованию занимает время. Рекомендуется использовать [процесс инкрементного рационализации](./rationalize.md#incremental-rationalization).

### <a name="myth-cloud-adoption-has-to-wait-for-all-workloads-to-be-rationalized"></a>Миф: внедрение в облако должно дожидаться рационального распределения всех рабочих нагрузок

Рационализацию весь ИТ-портфель или даже один центр обработки данных может задержать реализацию ценности бизнеса по месяцам или даже годам. По возможности следует избегать полной рациональности. Вместо этого используйте [преимущества 10, чтобы выпустить планирование](./rationalize.md#release-planning) , чтобы принимать разумные решения о следующих 10 рабочих нагрузках, которые приводятся для внедрения в облако.

### <a name="myth-business-justification-has-to-wait-for-all-workloads-to-be-rationalized"></a>Миф: коммерческое обоснование должно дожидаться рационального распределения всех рабочих нагрузок

Чтобы разработать Деловое обоснование для усилий по внедрению в облако, сделайте несколько базовых допущений на уровне портфеля. При согласовании мотиваций с нововведениями Предположим, что используется реархитектура. При согласовании мотиваций с миграцией предполагается повторное размещение. Эти предположения могут ускорить процесс делового обоснования. После этого предполагается, что в ходе фазы оценки цикла перехода каждой рабочей нагрузки выявляются такие предположения и бюджеты.

Теперь ознакомьтесь со следующими пятью процессами рационализации, чтобы ознакомиться с долгосрочным процессом. При разработке плана внедрения в облако выберите вариант, который наилучшим образом соответствует вашим мотивациям, результатам бизнеса и текущей среде состояния. Целью в процессе систематизации цифровых площадок является установка базовых показателей, а не рационализировать каждой рабочей нагрузке.

## <a name="the-five-rs-of-rationalization"></a>Пять принципов рационализации

Пять RS, приведенные здесь, описывают наиболее распространенные параметры для рационализации.

## <a name="rehost"></a>Повторное размещение

Так же известно, как миграция с *прогнозированием и сдвигом* , перемещение текущего актива штата в выбранный поставщик облачных служб приводит к минимальному изменению общей архитектуры.

К общим драйверам могут относиться:

- Уменьшение капитальных затрат.
- Освобождение пространства центра обработки данных.
- Быстрое возвращение инвестиций в облако.

Факторы количественного анализа:

- Размер виртуальной машины (ЦП, память, хранилище).
- Зависимости (сетевой трафик).
- Совместимость ресурсов активов.

Факторы качественного анализа:

- Допуск для изменения.
- Бизнес-приоритеты.
- Критические бизнес-события.
- Зависимости процессов.

## <a name="refactor"></a>Рефакторинг

Параметры "платформа как услуга" (PaaS) позволяют снизить эксплуатационные расходы, связанные с множеством приложений. Рекомендуется немного реорганизовать приложение в соответствии с моделью на основе PaaS.

"Рефакторинг" также относится к процессу разработки приложений для рефакторинга кода, чтобы позволить приложению предоставлять новые возможности для бизнеса.

К общим драйверам могут относиться:

- Более быстрые и короткие обновления.
- Переносимость кода.
- Повышение эффективности работы в облаке (ресурсы, скорость, стоимость, управляемые операции).

Факторы количественного анализа:

- Размер ресурса приложения (ЦП, память, хранилище).
- Зависимости (сетевой трафик).
- Пользовательский трафик (Просмотры страниц, время на странице, время загрузки).
- Платформа разработки (языки, платформа данных, службы среднего уровня).
- База данных (ЦП, память, хранилище, версия).

Факторы качественного анализа:

- Непрерывные инвестиции в бизнес.
- Параметры ускорения или временные шкалы.
- Зависимости бизнес-процессов.

## <a name="rearchitect"></a>Перепроектирование

Некоторые приложения для работы с образами не совместимы с поставщиками облачных решений в связи с архитектурными решениями, которые были сделаны при создании приложения. В таких случаях может потребоваться изменение архитектуры приложения перед преобразованием.

В других случаях приложения, совместимые с облаком, но не являющиеся собственными в облаке, могут повысить экономичность и эффективность работы, переменив архитектуру решения на собственное облачное приложение.

К общим драйверам могут относиться:

- Масштабирование и гибкость приложения.
- Упрощенное внедрение новых возможностей облака.
- Сочетание технологических стеков.

Факторы количественного анализа:

- Размер ресурса приложения (ЦП, память, хранилище).
- Зависимости (сетевой трафик).
- Пользовательский трафик (Просмотры страниц, время на странице, время загрузки).
- Платформа разработки (языки, платформа данных, службы среднего уровня).
- База данных (ЦП, память, хранилище, версия).

Факторы качественного анализа:

- Растущие инвестиции в бизнес.
- Эксплуатационные расходы.
- Потенциальные циклы обратной связи и вложения DevOps.

## <a name="rebuild"></a>Перестроение

В некоторых сценариях Дельта, которая должна быть преодолена для переноса приложения, может быть слишком большой, чтобы выровнять дополнительные инвестиции. Это особенно справедливо для приложений, которые ранее соответствовали потребностям бизнеса, но теперь не поддерживаются или неправильно соответствуют текущим бизнес-процессам. В этом случае создается новая база кода для согласования с подходом, [присущим облачным](https://azure.microsoft.com/overview/cloudnative/) технологиям.

К общим драйверам могут относиться:

- Ускорение инноваций.
- Быстрое создание приложений.
- Сокращение эксплуатационных расходов.

Факторы количественного анализа:

- Размер ресурса приложения (ЦП, память, хранилище).
- Зависимости (сетевой трафик).
- Пользовательский трафик (Просмотры страниц, время на странице, время загрузки).
- Платформа разработки (языки, платформа данных, службы среднего уровня).
- База данных (ЦП, память, хранилище, версия).

Факторы качественного анализа:

- Отклонение удовлетворенности конечным пользователем.
- Бизнес-процессы, ограниченные функциональными возможностями.
- Потенциальные расходы, опыт или прибыль.

## <a name="replace"></a>Заменить

Решения обычно реализуются с помощью лучших технологий и подходов, доступных в данный момент. Иногда приложения SaaS (программное обеспечение как услуга) могут предоставлять все необходимые функции для размещенного приложения. В этих сценариях рабочую нагрузку можно запланировать для последующей замены, фактически удалив ее из усилий по преобразованию.

К общим драйверам могут относиться:

- Стандартизация рекомендаций по отраслевым стандартам.
- Ускорение внедрения подходов, основанных на бизнес-процессах.
- Перераспределение инвестиций в разработку приложений, которые создают конкурентные отличия или преимущества.

Факторы количественного анализа:

- Общие сокращения эксплуатационных расходов.
- Размер виртуальной машины (ЦП, память, хранилище).
- Зависимости (сетевой трафик).
- Ресурсы для снятия с учета.
- База данных (ЦП, память, хранилище, версия).

Факторы качественного анализа:

- Анализ выгодной стоимости текущей архитектуры и решения SaaS.
- Схемы бизнес-процессов.
- Схемы данных.
- Настраиваемые или автоматизированные процессы.

## <a name="next-steps"></a>Дальнейшие действия

В совокупности вы можете применить эти пять RS-нерациональных решений к цифровому расведению, чтобы принимать решения об обоснованиях в будущем состоянии каждого приложения.

> [!div class="nextstepaction"]
> [Что такое цифровые активы](./index.md)
