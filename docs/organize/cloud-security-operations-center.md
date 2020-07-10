---
title: Облачные функции SOC
description: Общие сведения о функциях центра Cloud Security Operations (SOC).
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: ffb7f04de4a9d4b8e6b3d379269dc60ca161113b
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194295"
---
<!-- docsTest:ignore "Cyber Defense Operations Center" -->
<!-- cSpell:ignore CISO MTTA MTTR SIEM NIST SOCs CDOC -->

# <a name="cloud-soc-functions"></a>Облачные функции SOC

Основной целью центра Cloud Security Operations Center (SOC) является обнаружение, реагирование и восстановление из активных атак на корпоративные ресурсы.

По мере того, как SOC будет развить, операции безопасности должны:

- Реагирование на атаки, обнаруженные инструментами
- Упреждающий Поиск атак, в которых были обнаружены прошлые реактивные обнаружения

## <a name="modernization"></a>Модернизация

Обнаружение угроз и реагирование на них в настоящее время очень модернизации на всех уровнях.

- **Повышение уровня управления рисками для бизнеса:** Компания SOC растет в ключевой компонент управления бизнес-риском для Организации.
- **Метрики и цели:** Отслеживание эффективности SOC развивается с момента обнаружения следующих ключевых индикаторов:
  - _Скорость реагирования_ через среднее время подтверждения (мтта).
  - _Скорость исправления_ через среднее время восстановления (MTTR).
- **Развитие технологий:** Технология SOC развивается от монопольного использования статического анализа журналов в SIEM для добавления использования специализированных средств и сложных методов анализа. Это позволяет получить подробные сведения о ресурсах, предоставляющих высококачественные оповещения и возможности исследования, дополняющие представление SIEM. Оба типа инструментов все чаще используют AI и машинное обучение, аналитику поведения и интегрированную аналитику угроз для выявления и определения приоритетов аномальных действий, которые могут быть злоумышленниками.
- Поиск **угроз:** SOC — это добавление обнаружения угроз на основе гипотез, которое позволяет заранее определить опытных злоумышленников и сдвинуть помехи из очередей оказался аналитиков.
- **Управление инцидентами:** Дисциплина становится формальной для координации нетехнических элементов инцидентов с юридическими, взаимосвязями и другими группами.
**Интеграция внутреннего контекста:** Чтобы помочь в определении приоритетов для действий SOC, таких как относительные показатели рисков учетных записей и устройств, чувствительность данных и приложений, а также ключевые границы изоляции безопасности для тесной защиты.

 Дополнительные сведения см. в следующих источниках.

- [Стратегии и &mdash; операции безопасности стандартов архитектуры](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks)
- [Модуль перспективы Workshop 4b: стратегия защиты от угроз](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-4b)
- Блог кибератак оборон Operations Center (КДОК), часть [1](https://www.microsoft.com/security/blog/2019/02/21/lessons-learned-from-the-microsoft-soc-part-1-organization), [часть 2A](https://www.microsoft.com/security/blog/2019/04/23/lessons-learned-microsoft-soc-part-2-organizing-people), [часть 2b](https://www.microsoft.com/security/blog/2019/06/06/lessons-learned-from-the-microsoft-soc-part-2b-career-paths-and-readiness), [часть 3a](https://www.microsoft.com/security/blog/2019/10/07/ciso-series-lessons-learned-from-the-microsoft-soc-part-3a-choosing-soc-tools), [часть 3b](https://www.microsoft.com/security/blog/2019/12/23/ciso-series-lessons-learned-from-the-microsoft-soc-part-3b-a-day-in-the-life)
- [Руководством по обработке инцидентов для компьютерной безопасности NIST](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)
- [Рекомендации NIST по восстановлению событий кибербезопасности](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-184.pdf)

## <a name="team-composition-and-key-relationships"></a>Компоновка команды и основные связи

Центр облачных операций безопасности обычно состоит из следующих типов ролей.

- ИТ-операции (закрытие обычного контакта)
- Анализ угроз
- Архитектура безопасности
- Программа для оценки рисков
- Юридические ресурсы и персонал
- Группы взаимодействия
- Организация рисков (при наличии)
- Отраслевые ассоциации, сообщества и поставщики (до возникновения инцидента)

## <a name="next-steps"></a>Дальнейшие действия

Изучите функцию [архитектуры безопасности](./cloud-security-architecture.md).
