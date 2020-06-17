---
title: Группа управления и организация подписки
description: Группа управления и организация подписки
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e6188f4687595c96788478b12853a0b01dffd2ce
ms.sourcegitcommit: d88c1cc3597a83ab075606d040ad659ac4b33324
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2020
ms.locfileid: "84792458"
---
# <a name="management-group-and-subscription-organization"></a>Группа управления и организация подписки

![Иерархия группы управления](./media/sub-org.png)

_Рис. 1. иерархия групп управления._

## <a name="define-a-management-group-hierarchy"></a>Определение иерархии групп управления

Структуры группы управления в клиенте Azure Active Directory (Azure AD) поддерживают сопоставление организаций и должны быть тщательно учтены, когда Организация планирует переход Azure в масштабе.

**Рекомендации по проектированию:**

- Группы управления можно использовать для объединения политик и назначений инициатив с помощью политики Azure.
- Дерево группы управления может поддерживать до [шести уровней глубины](https://docs.microsoft.com/azure/governance/management-groups/overview#hierarchy-of-management-groups-and-subscriptions). Это ограничение не включает уровень корня или подписки.

**Рекомендации по проектированию:**

- Разстарайтесь, чтобы иерархия группы управления была достаточно простой, не более чем с трех до четырех уровней, в идеале. Это снижает затраты на управление и сложность.

- Избегайте дублирования организационной структуры в иерархию глубоко вложенной группы управления. Группы управления следует использовать для назначения политик и выставления счетов. Это требует использования групп управления в архитектуре корпоративного уровня, которая предоставляет политики Azure для рабочих нагрузок, которым требуется тот же тип безопасности и соответствия, что и на одном уровне группы управления.

- Создайте группы управления в группе управления корневого уровня, чтобы представить типы рабочих нагрузок (архетипа), которые будут размещены и на основе требований к безопасности, соответствию, подключению и функциональности. Это позволяет использовать набор политик Azure на уровне группы управления для всех рабочих нагрузок, которым требуются те же параметры безопасности, соответствия, подключения и функции.

- Используйте теги ресурсов, которые могут быть применены или добавлены с помощью политики Azure, для запроса и горизонтального перехода по иерархии группы управления. Это облегчает группирование ресурсов в целях поиска без использования сложной иерархии групп управления.

- Создайте группу управления "песочницу" верхнего уровня, чтобы позволить пользователям немедленно экспериментировать с Azure. Это позволяет пользователям экспериментировать с ресурсами, которые могут быть еще не разрешены в рабочих средах, и обеспечивает изоляцию от сред разработки, тестирования и рабочей среды.

- Используйте выделенное имя участника-службы (SPN) для выполнения операций управления группами управления, операций управления подписками и назначения ролей. Это сокращает число пользователей с повышенными правами, следуя рекомендациям по крайней мере по обеспечению привилегий.

- Назначьте `User Access Administrator` роль RBAC Azure в области корневой группы управления ( `/` ), чтобы предоставить имя субъекта-службы, упомянутое выше, с доступом на корневом уровне. После предоставления имени субъекта-службы `User Access Administrator` можно безопасно удалить эту роль. Это гарантирует, что только имя субъекта-службы является частью `User Access Administrator` роли.

- Назначьте `Contributor` разрешение для имени участника-службы, упомянутого выше, в области корневой группы управления ( `/` ), что позволяет выполнять операции на уровне клиента. Это гарантирует, что имя субъекта-службы можно использовать для развертывания ресурсов и управления ими в любой подписке в Организации.

- Создайте `Platform` группу управления в корневой группе управления для поддержки общей политики платформы и назначения управления доступом на основе ролей (RBAC). Это гарантирует, что к подпискам, используемым для Azure Foundation, можно применить различные политики, и выставление счетов за общие ресурсы осуществляется в одном наборе базовых подписок.

- Ограничьте число назначений политики Azure, сделанных в корневой области группы управления ( `/` ). Это позволяет избежать отладки наследуемых политик в группах управления более низкого уровня.

- Не создавайте подписки в корневой группе управления. Это гарантирует, что подписки не только наследуют небольшой набор политик Azure, назначенных в группе управления корневого уровня, что не представляет полный набор, необходимый для рабочей нагрузки.

## <a name="subscription-organization-and-governance"></a>Организация и управление подпиской

Подписки — это единица управления, выставления счетов и масштабирования в Azure, и они играют важную роль при проектировании для крупномасштабного внедрения Azure. В этом разделе приписываются требования к клиентской подписке и целевые подписки для разработки на основе критических факторов, таких как тип среды, владелец и модель управления, организационная структура и портфолио приложений.

**Рекомендации по проектированию:**

- Подписки служат границами для назначения политик Azure. Например, для обеспечения соответствия защищенным рабочим нагрузкам, таким как рабочие нагрузки в индустрии платежных карт (PCI), обычно требуются дополнительные политики. Вместо использования группы управления для группирования рабочих нагрузок, которым требуется соответствие требованиям PCI, можно добиться такой же изоляции с помощью подписки. Это гарантирует, что у вас не будет слишком много групп управления с небольшим количеством подписок.

- Подписки служат в качестве единицы масштабирования, чтобы рабочие нагрузки компонентов могли масштабироваться в пределах [подписки](https://docs.microsoft.com/azure/azure-subscription-service-limits)платформы. Не забудьте рассмотреть ограничения ресурсов подписки во время сеансов разработки рабочей нагрузки.

- Подписки обеспечивают границу управления и изоляцию, создавая четкое разделение проблем.

- Существует ручной процесс (запланированная будущая Автоматизация), который можно использовать для ограничения использования клиентом Azure AD подписок на корпоративную регистрацию. Это предотвращает создание подписок MSDN в области корневой группы управления.
  
**Рекомендации по проектированию:**

- Подписку следует рассматривать как демократичными единицу управления в соответствии с потребностями бизнеса и приоритетами.

- Владельцы подписки осведомлены о своих ролях и обязанностях:

  - Выполните проверку доступа в Azure AD Privileged Identity Management квартале или два раза в год, чтобы не допустить распространения прав по мере перемещения пользователей в Организации.

  - Проведите полное владение бюджетными затратами и использованием ресурсов.

  - Обеспечение соответствия политике и исправление при необходимости.

- При определении требований для новых подписок используйте следующие принципы.

  - **Ограничения масштабирования:** Подписки служат единицей масштабирования для рабочих нагрузок компонентов, чтобы масштабироваться в пределах подписок платформы. Например, большие специализированные рабочие нагрузки, такие как высокопроизводительные вычислительные системы, IoT и SAP, лучше подходят для использования отдельных подписок, чтобы избежать ограничений (например, ограничение 50 интеграции фабрики данных Azure).

  - **Граница управления:** Подписки обеспечивают разграничение управления и изоляции, что позволяет четко отделить проблемы. Например, различные среды, такие как разработка, тестирование и производство, часто изолируются с точки зрения управления.

  - **Граница политики:** Подписки служат в качестве границы для назначения политик Azure. Например, для обеспечения соответствия защищенным рабочим нагрузкам, таким как PCI, обычно требуются дополнительные политики, и эти дополнительные издержки не должны считаться глобальными, если используется отдельная подписка. Аналогичным образом, среды разработки могут иметь более строгие требования к политике, связанные с рабочими средами.

  - **Топология целевой сети:** Виртуальные сети нельзя совместно использовать в подписках, но они могут подключаться с помощью различных технологий, таких как пиринг виртуальных сетей или ExpressRoute. Поэтому важно учитывать, какие рабочие нагрузки должны взаимодействовать друг с другом при принятии решения о необходимости новой подписки.

- Группировка подписок в группах управления в соответствии со структурой группы управления и требованиями политики в масштабе. Это гарантирует, что подписки с одинаковым набором политик и назначениями RBAC могут наследовать их от группы управления, избегая дублирования назначений.

- Создайте выделенную подписку на управление в `Platform` группе управления для поддержки глобальных возможностей управления, таких как Azure Monitor log Analytics рабочих областей и модулей Runbook службы автоматизации Azure.

- При необходимости установите выделенную подписку на удостоверение в `Platform` группе управления для размещения контроллеров домена Windows Server Active Directory.

- Установите выделенную подписку на подключение в `Platform` группе управления, чтобы разместить виртуальный концентратор глобальной сети Azure, частный DNS-сервер, цепь ExpressRoute и другие сетевые ресурсы. Это гарантирует, что счета за все основные сетевые ресурсы будут выставляться вместе и изолированы от других рабочих нагрузок.

- Старайтесь не использовать модель жесткой подписки, вместо набора гибких критериев для группировки подписок в Организации. Это гарантирует, что при изменении структуры и рабочей нагрузки Организации вы сможете создавать новые группы подписок вместо фиксированного набора существующих подписок. Один размер не подходит для всех подписок. то, что работает для одного подразделения, может не работать для другого. Некоторые приложения могут сосуществовать в одной подписке на целевую зону, а другие могут потребовать собственную подписку.

## <a name="configure-subscription-quota-and-capacity"></a>Настройка квоты и емкости подписки

Каждый регион Azure содержит конечное количество ресурсов. При рассмотрении внедрения Azure корпоративного уровня, включающего большие объемы ресурсов, обеспечьте доступность достаточной емкости и номеров SKU, а также можно понять и отслеживать достижимую емкость.

**Рекомендации по проектированию:**

- Используйте ограничения и квоты на платформе Azure для каждой службы, требуемой рабочими нагрузками.

- Рассмотрим доступность требуемых номеров SKU в выбранных регионах Azure. Например, новые функции могут быть доступны только в определенных регионах. Доступность определенных номеров SKU для таких ресурсов, как виртуальные машины, может отличаться от одного региона к другому.

- Учтите, что квоты подписки не гарантируют емкость и применяются для каждого региона.

**Рекомендации по проектированию:**

- Используйте подписки в качестве единиц масштабирования, а также выполняйте масштабирование ресурсов и подписок по мере необходимости. Это гарантирует, что Рабочая нагрузка сможет использовать необходимые ресурсы для масштабирования при необходимости, не прибегая к ограничениям подписки на платформе Azure.

- Используйте зарезервированные экземпляры для определения приоритета зарезервированной емкости в обязательных регионах. Это гарантирует, что Рабочая нагрузка будет иметь требуемую емкость даже при высоком спросе на этот ресурс в определенном регионе.

- Создайте панель мониторинга с настраиваемыми представлениями для мониторинга используемых уровней емкости. Настройте оповещения, если использование емкости приближается к критическим уровням (например, 90 процента загрузки ЦП).

- Вызывайте запросы на поддержку для увеличения квоты в рамках подготовки подписки (например, общее количество доступных ядер виртуальных машин в подписке). Это гарантирует, что квоты будут установлены до тех пор, пока рабочие нагрузки не зайдут ограничения по умолчанию.

- Убедитесь, что необходимые службы и компоненты доступны в выбранных регионах развертывания.

## <a name="establish-cost-management"></a>Создание управления затратами

Затраты на прозрачность по техническим затратам — это критически важный вопрос управления, с которым сталкиваются каждая крупная корпоративная организация. В этом разделе рассматриваются ключевые аспекты, связанные с тем, как можно достичь прозрачности затрат в крупных средах Azure.

**Рекомендации по проектированию:**

- Потенциальная потребность в моделях беспрецедентных моделей, в которых связаны общие ресурсы платформы как услуга (PaaS), например Среда службы приложений Azure и служба Azure Kubernetes, которые могут быть доступны для достижения более высокой плотности.

- Используйте расписание завершения работы для непроизводственных рабочих нагрузок, чтобы оптимизировать затраты.

- Использование помощника по Azure для проверки рекомендаций по оптимизации затрат.

**Рекомендации по проектированию:**

- Используйте службу управления затратами Azure для агрегирования затрат и сделайте ее доступной для владельцев приложений.

- Используйте теги ресурсов Azure для классификации затрат и группирования ресурсов. Это позволяет использовать механизм для рабочих нагрузок, которые совместно используют подписку или для конкретной рабочей нагрузки, охватывающей несколько подписок.