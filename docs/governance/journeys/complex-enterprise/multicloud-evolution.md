---
title: 'Руководство по управлению для сложных предприятий: Улучшение в облаке'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Большое руководство для предприятий: Улучшение в облаке'
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6f015fcc7a0cb4000502d90ff971341fd6d26ca5
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908648"
---
# <a name="large-enterprise-guide-multicloud-improvement"></a>Большое руководство для предприятий: Улучшение в облаке

## <a name="advancing-the-narrative"></a>Будущие описания

Корпорация Майкрософт понимает, что пользователи внедряют технологию нескольких облаков для определенных целей. Вымышленная компания в этом руководством не является исключением. Успех в бизнесе параллельно с процессом внедрения Azure привел к приобретению небольшой взаимодополняющей компании. Все ИТ-операции данного предприятия выполняются в другом поставщике облачных служб.

В этой статье описывается, как изменяются некоторые методы и процессы в случае интеграции новой организации. В качестве примера мы предполагаем, что эта компания выполнила все итерации по управлению, описанные в этом руководство по управлению.

### <a name="changes-in-the-current-state"></a>Изменения в текущем состоянии

На предыдущем этапе в этом предложении компания приступила к внедрению средств контроля затрат и контроля затрат, так как расходы на облачные ресурсы становятся частью стандартных эксплуатационных расходов компании.

С того времени изменились некоторые факторы, влияющие на систему управления.

- Удостоверением управляет локальный экземпляр Active Directory. Благодаря репликации в Azure Active Directory процесс гибридной идентификации стал проще.
- ИТ операции или облачные операции во многом управляются Azure Monitor и связанными возможностями автоматизации.
- Аварийное восстановление и непрерывность бизнес-процессов (ДРБК) контролируются экземплярами хранилища Azure.
- Центр безопасности Azure используется для мониторинга нарушений и атак безопасности.
- Центр безопасности Azure и Azure Monitor используются для мониторинга системы управления в облаке.
- Azure Blueprints, Политика Azure и группы управления используются для обеспечения соответствия политике.

### <a name="incrementally-improve-the-future-state"></a>Постепенно улучшайте будущее состояние

Целью является интеграция приобретенной компании в имеющиеся операции, там где это возможно.

## <a name="changes-in-tangible-risks"></a>Изменения в материальных рисках

**Стоимость приобретения бизнес-процессов:** Приобретение нового бизнеса будет считаться выгодным в течение приблизительно пяти лет. Правление хочет максимально контролировать расходы на приобретение из-за длительного срока окупаемости. Существует риск конфликта между управлением затратами и технической интеграцией.

Риски для бизнеса связаны со следующими техническими проблемами:

- При миграции в облако возникает риск приобретения дополнительных затрат на приобретение.
- Существует также риск того, что новая среда не будет должным образом регулироваться или приведет к нарушениям политики.

## <a name="incremental-improvement-of-the-policy-statements"></a>Добавочное улучшение операторов политики

Следующие изменения в политике помогут устранить новые риски и пошаговое внедрение.

- Все ресурсы из вторичного облака должны контролироваться с помощью имеющихся инструментов операционного управления и мониторинга безопасности.
- Все подразделения должны быть интегрированы для использования существующего поставщика удостоверений.
- Основной поставщик удостоверений должен управлять проверкой подлинности в ресурсах во вторичном облаке.

## <a name="incremental-improvement-of-the-best-practices"></a>Добавочное улучшение рекомендаций

В этом разделе статьи улучшена структура MVP по управлению, которая включает новые политики Azure и реализацию службы "Управление затратами Azure". Совокупно эти изменения проекта позволят внедрить новые правила корпоративной политики.

1. Подключение сетей. Поддерживается системой управления сетями и ИТ.
    1. Добавление подключения от поставщика MPLS или арендованной строки к новому облаку приведет к интеграции сетей. Добавление таблиц маршрутизации и параметров конфигурации брандмауэра позволит контролировать доступ и трафик между средами.
1. Консолидация поставщиков удостоверений. В зависимости от рабочих нагрузок, размещенных во вторичном облаке, существует несколько вариантов консолидации поставщиков удостоверений. Ниже приводятся несколько примеров.
    1. Для приложений, в которых проверка подлинности выполняется с помощью OAuth 2, пользователи Active Directory во вторичном облаке могут быть реплицированы в существующий клиент Azure AD.
    1. И наоборот, федерация двух локальных поставщиков удостоверений позволит выполнять репликацию пользователей из новых доменов Active Directory в Azure.
1. Добавление ресурсов в службу Azure Site Recovery.
    1. Azure Site Recovery был создан в качестве гибридного и многооблачного средства с самого начала.
    1. Для защиты виртуальных машин вторичного облака могут использоваться те же процессы Azure Site Recovery, которые используются для защиты локальных ресурсов.
1. Добавление ресурсов в службу "Управление затратами Azure".
    1. Служба "Управление затратами Azure" была разработана в виде многооблачного средства с самого начала.
    1. Виртуальные машины вторичного облака могут быть совместимы со службой "Управление затратами Azure" для некоторых поставщиков облачных служб. Может взиматься дополнительная плата.
1. Добавление ресурсов в Azure Monitor.
    1. Служба Azure Monitor изначально была создана как инструмент гибридного облака.
    1. Виртуальные машины вторичного облака могут быть совместимы с агентами Azure Monitor, что позволяет включать их в Azure Monitor для операционного мониторинга.
1. Средства обеспечения управления.
    1. Принудительное применение системы управления выполняется в облаке,
    1. Корпоративные политики, установленные в разделе Руководство по управлению, не относятся к конкретному облаку. Хотя их внедрение может варьироваться от облака к облаку, правила политики могут применяться ко вторичному поставщику.

По мере роста внедрения в рамках облака управление, приведенное выше, будет продолжаться.

## <a name="next-steps"></a>Следующие шаги

Во многих крупных предприятиях пять дисциплин управления облаком могут быть заблокированы для внедрения. В следующей статье содержатся некоторые дополнительные соображения о том, как сделать управление участником группы, чтобы обеспечить долгосрочное успешность в облаке.

> [!div class="nextstepaction"]
> [Использование нескольких уровней управления](./multiple-layers-of-governance.md)