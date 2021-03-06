---
title: Определение корпоративной политики Cloud управление
description: Используйте платформу внедрения облачных технологий для Azure, чтобы научиться устанавливать политики, которые позволяют устранить известные риски и отказоустойчивость в процессе преобразования в облако.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: ff6a3836280dc213e63719b2c25ed4be5c2ea104
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101791366"
---
# <a name="define-corporate-policy-for-cloud-governance"></a>Определение корпоративной политики для управления облаком

После анализа известных рисков и связанных с рисками рисков для пути преобразования в облако вашей организации ваш следующий шаг заключается в установке политики, которая явно устранит эти риски и определит шаги, необходимые для устранения этих рисков там, где это возможно.

## <a name="how-can-corporate-it-policy-become-cloud-ready"></a>Подготовка корпоративной ИТ-политики к использованию в облаке

В традиционной системе управления с поэтапным подходом корпоративная политика создает рабочее определение управления. Большинство действий по управлению, выполняемых ИТ-отделами, ориентированы на внедрение технологий мониторинга, принудительного применения, эксплуатации и автоматизации этих корпоративных политик. Облачная система управления основана на аналогичных концепциях.

![Корпоративная система управления и дисциплины управления](../../_images/operational-transformation-govern-large.png)
*Рис. 1. Корпоративная система управления и дисциплины управления.*

На приведенном выше рисунке показана связь между бизнес-риском, политикой и соответствием, а также механизмами мониторинга и применения, которые должны взаимодействовать в рамках стратегии управления. Пять дисциплин управления облаком позволяют управлять этими взаимодействиями и реализовать стратегию.

Облачная система управления формируется в результате постоянного внедрения облачных технологий в течение длительного времени, так как настоящее устойчивое преобразование невозможно выполнить за один раз. Попытка быстро создать завершенную облачную систему управления без изменения ключевых аспектов корпоративной политики редко приносит желаемые результаты. Вместо этого мы рекомендуем применять поэтапный подход.

Отличия от платформы внедрения облачных технологий — это цикл покупки, который может включить подлинное преобразование. Так как не существует требования к приобретению больших капитальных расходов, инженеры могут начать эксперименты и провести внедрение быстрее. В большинстве корпоративных сред устранение ограничения в виде капитальных расходов на внедрение позволяет ускорить циклы обратной связи, а также обеспечить органичное развитие и поэтапное выполнение работ.

Переход в облако требует изменений и в системе управления. Во многих организациях преобразование корпоративной политики позволяет улучшить систему управления и повысить показатели соблюдения политики благодаря поэтапному подходу к изменениям. Кроме того, можно автоматизировать их применение на базе новых возможностей, которые настраиваются в системах поставщика облачной службы.

## <a name="review-existing-policies"></a>Изучение имеющихся политик

По мере того как управление является текущим процессом, политика должна быть регулярно проверена с учетом ИТ-специалистов и заинтересованных лиц, чтобы ресурсы, размещенные в облаке, продолжали поддерживать соответствие общим целям и требованиям Организации. Оценка новых рисков и их допустимости может стать поводом для [пересмотра имеющихся политик](./cloud-policy-review.md), который поможет определить необходимый уровень управления для конкретной организации.

> [!TIP]
> Если ваша организация использует поставщиков или других доверенных бизнес-партнеров, то одной из самых крупных бизнес-рисков может быть отсутствие соблюдения [нормативных требований](./regulatory-compliance.md) с учетом этих внешних организаций. Этот риск часто не может быть исправлен, и вместо этого может требоваться строгое соблюдение требований всех сторон. Прежде чем начать проверку политики, убедитесь, что вы определили и понимаете все требования к совместимости сторонних разработчиков.

## <a name="create-cloud-policy-statements"></a>Создание положений политики облака

Облачные ИТ-политики задают требования, стандарты и цели, которым нужно следовать ИТ-специалистам и автоматизированным системам. Решения на основе политики являются основным фактором в вашей [схеме архитектуры облака](./governance-alignment.md) и определяют способ реализации ваших [процессов соблюдения политики](./processes.md).

Отдельные правила облачной политики служат рекомендациями по устранению конкретных рисков, выявленных в процессе оценки рисков. Хотя эти политики могут быть интегрированы в вашу обширную документацию по политикам, в рамках рекомендаций по облачной инфраструктуре, обсуждаемых в рекомендациях по облачным платформам внедрения, рассматривается более краткая сводка рисков и планов, с которыми они работают. Каждое определение должно включать следующие элементы информации.

- **Бизнес-риск:** Сводка риска, который будет решать эта политика.
- **Инструкция политики:** Краткое описание требований и целей политики.
- **Проектирование или техническое руководство:** Практические рекомендации, спецификации или другие рекомендации по поддержке и реализации этой политики, которые ИТ и разработчики могут использовать при проектировании и построении облачных развертываний.

Если вам нужна помощь с началом определения политик, ознакомьтесь с [дисциплинами](../governance-disciplines.md) управления, представленными в разделе Обзор раздела "Управление". Статьи для каждой из этих дисциплин включают примеры распространенных бизнес-рисков, возникающих при переходе в облако, и примеры политик, используемых для устранения этих рисков. Например, см. [Пример определения политики](../cost-management/policy-statements.md)для управления затратами.

## <a name="incremental-governance-and-integrating-with-existing-policy"></a>Последовательное управление и интеграция с имеющейся политикой

Плановые дополнения к облачной среде всегда необходимо проверять на соответствие имеющейся политике и политике, обновленной с учетом любых не описанных вопросов. Следует также регулярно выполнять [проверку облачной политики](./cloud-policy-review.md), чтобы убедиться, что она не устарела и синхронизирована с другими новыми корпоративными политиками.

Необходимость интегрирования политики облака с устаревшими ИТ-политиками в значительной степени зависит от зрелости процессов управления облаком и размера ваших облачных ресурсов. Более подробное обсуждение по работе с интеграцией политики во время преобразования облака см. в этой статье [о последовательном управлении и MVP политики](./index.md).

## <a name="next-steps"></a>Дальнейшие действия

Определив политики, создайте руководство по проектированию архитектуры, чтобы предоставить практические рекомендации ИТ-специалистам и разработчикам.

> [!div class="nextstepaction"]
> [Соответствие руководства по проектированию руководства корпоративным политикам](./governance-alignment.md)
