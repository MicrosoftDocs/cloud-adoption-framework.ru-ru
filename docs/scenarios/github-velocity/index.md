---
title: Как GitHub ускоряет внедрение облачных технологий
description: С помощью GitHub компании могут подключиться к сообществу разработчиков решений с открытым кодом и найти тысячи примеров повторяемых улучшенных и готовых к развертыванию облачных решений от организаций, которые успешно внедрили службы Azure.
author: nkpatterson
ms.author: janet
ms.date: 1/11/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: think-tank
ms.openlocfilehash: 9ef511df74fe14c0a2e9906bdf51e9fc3d219251
ms.sourcegitcommit: 9cd2b48fbfee229edc778f8c5deaf2dc39dfe2d6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2021
ms.locfileid: "99227038"
---
# <a name="how-github-accelerates-cloud-adoption"></a>Как GitHub ускоряет внедрение облачных технологий

## <a name="overview"></a>Обзор

Инновации — это новая валюта в современных конкурентных средах. Совместные поездки, потоковая передача контента, автомобили с автономным управлением и другие услуги в корне изменили повседневный образ жизни людей, осуществив маркетинговый переворот. Эти инновации наглядно демонстрируют переход конкурентной среды с физических активов на цифровые.

Использование этих превосходных цифровых возможностей приводит к революционным изменениям, когда солидные компании сталкиваются с жесткой конкуренцией со стороны других компаний, которые могут быстрее внедрять инновации и предоставлять преимущества своим клиентам. Чтобы оставаться конкурентоспособными и избегать резких изменений, компаниям необходимо формировать культуру инноваций и использовать лучшие и наиболее подходящие инструменты и облачные службы.

GitHub предоставляет ряд функций, которые помогают компаниям:

- пользоваться преимуществами служб и возможностей Azure;
- модернизировать свои методики;
- становиться более гибкими и инновационными во время этого культурного сдвига.

С помощью GitHub компании могут подключиться к сообществу разработчиков решений с открытым кодом и найти тысячи примеров повторяемых улучшенных и готовых к развертыванию облачных решений от организаций, которые успешно внедрили службы Azure. Они могут легко заимствовать эти решения и дорабатывать их, чтобы адаптировать их к своим бизнес-потребностям.

GitHub позволяет организациям легко обмениваться данными внутри подразделений, что ускоряет модернизацию и развертывание следующего приложения или рабочей нагрузки. Компании могут обратиться к подходу *innersource*, ключевому принципу инноваций, чтобы позаимствовать лучшие методики, такие как совместная работа, повторное использование, сотрудничество, обмен данными и многое другое, у сообщества разработчиков решений с открытым кодом и применять эти методы в своей организации.

От защиты пакетов с открытым кодом до интеллектуальной собственности, создаваемой ежедневно, — защита всей цепочки поставки программного обеспечения должна быть главным приоритетом для каждой компании. Для достижения этой цели требуются передовые технологии обеспечения безопасности, которые можно внедрять и автоматизировать на протяжении всего жизненного цикла. Собственные возможности GitHub, такие как расширенные средства безопасности GitHub и GitHub Actions, обеспечивают требуемую гибкость.

## <a name="take-advantage-of-open-source-assets"></a>Воспользуйтесь преимуществами ресурсов с открытым кодом

Высокоэффективные организации рассматривают программное обеспечение с открытым кодом (OSS) как необходимые, а не дополнительные средства современной разработки. Они взаимодействуют с сообществами разработчиков, от которых они зависят, и используют безопасную платформу для стратегических инвестиций в OSS. В итоге такие организации быстро внедряют инновации, опережают конкурентов, сокращают расходы и минимизируют риск.

Хотя OSS можно рассматривать как пакеты, библиотеки, скрипты и зависимости, включенные в приложения, существуют тысячи ресурсов с открытым кодом в виде инфраструктуры в виде кода (IaC), документации, руководств и схем для четко определенных архитектур Azure. Эти схемы были предоставлены сообществу разработчиков OSS корпорацией Майкрософт, партнерами, поставщиками, клиентами и отдельными лицами. Все они доступны в GitHub. Их можно легко изменять, повторно использовать и развертывать в определенной среде Azure.

### <a name="infrastructure-as-code"></a>Инфраструктура как код

Инфраструктура как код (IaC) — это средства управления инфраструктурой (сетями, виртуальными машинами, подсистемами балансировки нагрузки и топологией подключений) в описательной модели с использованием той же системы управления версиями, которую команда DevOps использует для исходного кода. Подобно принципу, согласно которому один и тот же исходный код генерирует один и тот же двоичный файл, модель IaC генерирует одну и ту же среду каждый раз, когда она применяется. IaC — это ключевая практика DevOps, которая применяется наряду с [непрерывной поставкой (CD)](/azure/devops/learn/what-is-continuous-delivery).

Модель IaC была изменена для решения проблемы, связанной со смещением среды в конвейере выпуска. Без нее команды должны настраивать параметры отдельных сред развертывания, и несоответствие между средами приводит к проблемам во время развертывания. Каждая среда в конечном итоге становится чем-то вроде снежинки с уникальной конфигурацией, которую невозможно воспроизвести автоматически. Эта аналогия также предполагает, что операции администрирования и обслуживания инфраструктуры требуют выполнения некоторых процессов вручную. Они чаще сопряжены с ошибками и их трудно отследить. Развертывания инфраструктуры с помощью модели IaC являются повторяемыми и предотвращают проблемы во время выполнения, вызванные смещением конфигурации или отсутствием зависимостей.

Применяя IaC, команды вносят изменения в описание среды и управляют версиями модели конфигурации, которая обычно представлена в хорошо документированных форматах кода, таких как JSON (см. дополнительные сведения о [шаблонах Azure Resource Manager](/azure/azure-resource-manager/templates/overview)). Разработчики могут упростить свои рабочие процессы, разместив код IaC в том же репозитории GitHub, что и исходный код их приложений, и применить те же методы непрерывной интеграции (CI) / CD для IaC на базе [GitHub Actions](https://github.com/features/actions).

См. сведения о действии GitHub [AzOps](https://github.com/Azure/azops), чтобы узнать, как развернуть настраиваемые шаблоны Resource Manager в различных областях Azure. Если вы еще не работали с шаблонами Resource Manager или IaC, вы можете также посетить репозиторий [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) в GitHub, найти шаблон, который хотите развернуть, и нажать кнопку **Развернуть в Azure**, чтобы проверить, как он работает.

![Снимок экрана: кнопка **Развернуть в Azure**.](./media/deploy-to-azure.png)

### <a name="cloud-pattern-components-and-best-practices"></a>Компоненты облачного шаблона и рекомендации по его использованию

На следующей схеме архитектуры показаны проверки безопасности, выполняемые в компонентах GitHub и Azure среды GitHub DevSecOps:

![Схема архитектуры, на которой показаны проверки безопасности, выполняемые в компонентах GitHub и Azure среды GitHub DevSecOps.](./media/github-security-checks.png)

- [GitHub](https://docs.github.com) предоставляет платформу для размещения кода, которую разработчики могут использовать для совместной работы над проектами с открытым кодом и проектами innersource.

- [Codespaces](https://docs.github.com/github/developing-online-with-codespaces/about-codespaces) — это среда для разработки в подключенном режиме. Размещенный в GitHub и работающий на базе Microsoft Visual Studio Code, этот инструмент предоставляет комплексное решение для разработки в облаке.

- [Средства безопасности GitHub](https://github.com/features/security) устраняют угрозы несколькими способами. Агенты и службы выявляют уязвимости в репозиториях и зависимых пакетах. Они также обновляют зависимости до текущих и безопасных версий.

- [GitHub Actions](https://docs.github.com/actions/learn-github-actions) — это настраиваемые рабочие процессы, которые предоставляют возможности CI/CD непосредственно в репозиториях. Эти задания CI/CD выполняются на специальных компьютерах.

- [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis) — это многопользовательская облачная служба идентификации, которая контролирует доступ к Azure и другим облачным приложениям, таким как Microsoft 365 и GitHub.

- [Служба приложений Azure](https://azure.microsoft.com/services/app-service/) предоставляет платформу для создания, развертывания и масштабирования веб-приложений. Эта платформа предлагает встроенные возможности обслуживания инфраструктуры, установки обновлений для системы безопасности и масштабирования.

- [Политика Azure](/azure/governance/policy/overview) помогает командам управлять ИТ-задачами и предотвращать появление проблем с помощью определений политик, которые могут применять правила к облачным ресурсам. Например, если проект развертывает виртуальную машину с нераспознанным SKU, Политика Azure отправит предупреждения о проблеме и остановит развертывание.

- [Центр безопасности Azure](/azure/security-center/security-center-introduction) обеспечивает унифицированное управление безопасностью и расширенную защиту от угроз для рабочих нагрузок гибридного облака.

- [Azure Monitor](/azure/azure-monitor/overview) собирает и анализирует метрики производительности, журналы действий, а также другие данные телеметрии приложений. Эта служба информирует приложения и персонал об обнаружении нестандартных условий.

## <a name="innersource"></a>Подход innersource

### <a name="innersource-overview"></a>Общие сведения об innersource-разработке

Многие компании используют термин *innersource* для описания того, как команды инженеров совместно работают над кодом. Innersource — это подход к разработке, который позволяет инженерам создавать защищаемое программное обеспечение с использованием лучших методик, взятых из крупномасштабных проектов с открытым кодом, таких как Kubernetes или Visual Studio Code.

Крупномасштабные проекты с открытым кодом требуют координации и совместной работы тысяч участников. Наиболее успешные проекты основаны на видении будущего и определении повседневных ожиданий пользователей в отношении скорости, надежности и функциональности. Масштаб, в котором они работают, может послужить хорошим примером, помогая компаниям быстрее создавать лучшее программное обеспечение с помощью подхода innersource.

Благодаря запросам на вытягивание и рассмотрению проблем в GitHub совместная работа и проверка кода являются неотъемлемой частью процесса разработки. Команды штатных и внештатных сотрудников могут централизованно предоставлять доступ к своей работе, обсуждать изменения и получать отзывы. Это помогает организациям обмениваться опытом внутри компании и избегать повторного изобретения проверенных на практике решений, разработанных для других проектов.

### <a name="the-anatomy-of-an-innersource-project"></a>Анализ проекта innersource

Правильное сочетание отдельных сотрудников, команд и ресурсов может обеспечить успех проекта. Многие проекты с открытым кодом следуют аналогичной организационной структуре, которая помогает организациям создавать многофункциональные команды для управления проектами innersource. В типичном проекте с открытым кодом задействованы следующие сотрудники:

- **Специалисты по сопровождению ПО.** Эти участники несут ответственность за формирование видения и управление организационными аспектами проекта. Они могут не быть владельцами или авторами кода.

- **Соавторы.** Это люди, которые что-то вносят в проект.

- **Участники сообщества.** Это люди, которые пользуются проектом. Они могут активно вести диалоги или высказывать свое мнение о направлении проекта.

В более крупных проектах также могут быть подкомитеты или рабочие группы, занимающиеся различными задачами, такими как инструментирование, сортировка и модерация сообщества. Проекты innersource с большой вероятностью будут следовать аналогичной структуре. Во многих инженерных организациях разработчики разбиваются на команды по таким направлениям, как разработка приложений, разработка платформ и веб-разработка. Такое структурирование организаций чревато тем, что квалифицированные специалисты могут быть исключены из процесса. Создание основной группы по принятию решений, поддерживаемой командами в рамках всей организации, поможет аккумулировать знания и опыт, требуемые для ускоренного решения проблем.

В рамках предприятия соавторы — это разработчики компании, а специалисты по сопровождению — руководители проекта и ключевые лица, принимающие решения.

- **Специалисты по сопровождению ПО.** Разработчики, менеджеры по продуктам и другие ключевые лица, принимающие решения в компании и ответственные за реализацию видения проекта, а также управление ежедневным объемом работ.

- **Соавторы.** Разработчики, специалисты по обработке данных, менеджеры по продуктам, маркетологи и другие лица в компании, которые помогают продвигать программное обеспечение. Соавторы могут не входить непосредственно в команду проекта, но они помогают создавать программное обеспечение, внося код, отправляя исправления ошибок и т. д.

См. технический документ [Вводные сведения о подходе innersource](https://resources.github.com/whitepapers/introduction-to-innersource/).

## <a name="automation"></a>Автоматизация

Компонент GitHub Actions позволяет пользователям создавать настраиваемые рабочие процессы непосредственно в своих репозиториях GitHub. Пользователи могут обнаруживать, создавать действия и обмениваться ими для выполнения любой работы, включая CI/CD, а также объединять действия в полностью настраиваемый рабочий процесс. Они также могут создавать рабочие процессы CI, которые создают и тестируют проекты, написанные на разных языках программирования. Примеры можно найти в [руководствах по GitHub Actions](https://docs.github.com/actions/guides).

GitHub Actions можно использовать для объединения концепций IaC и практик CI/CD для автоматизации всего жизненного цикла сквозного развертывания, включая подготовку или обновление целевой среды повторяемым образом, а также упаковку и развертывание самого приложения.

### <a name="example"></a>Пример

[GitHub Actions для Azure](https://github.com/azure/actions) используется для упрощения автоматизации процессов развертывания для целевых служб Azure, таких как Служба приложений Azure, Служба Azure Kubernetes, Функции Azure и др. [Репозиторий с начальным набором рабочих процессов Azure](https://github.com/azure/actions-workflow-samples) включает комплексные рабочие процессы для создания и развертывания веб-приложений на любом языке и в любой экосистеме в Azure. Посетите [магазин marketplace GitHub](https://github.com/marketplace?query=azure&type=actions), чтобы узнать обо всех доступных действиях.

## <a name="security"></a>Безопасность

### <a name="githubs-shift-left-security-features"></a>Функции обеспечения безопасности GitHub с применением подхода "сдвиг влево"

С самых первых шагов разработки DevSecOps гарантирует применение лучших методик защиты. Используя стратегию сдвига влево, DevSecOps перенаправляет фокус, связанный с вопросами обеспечения безопасности. Вместо того чтобы фокусироваться на аудите по завершении процесса, во главу угла ставится разработка в его начале. Наряду с созданием надежного кода этот подход позволяет устранять ошибки на раннем этапе, когда их можно легко исправить.

Обладая множеством возможностей обеспечения безопасности, GitHub предлагает инструменты, которые поддерживают каждую часть рабочего процесса DevSecOps:

- IDE на основе браузера со встроенными расширениями безопасности;
- агенты, которые постоянно отслеживают рекомендации по обеспечению безопасности и заменяют уязвимые и устаревшие зависимости;
- функции поиска, сканирующие исходный код на наличие уязвимостей;
- рабочие процессы на основе действий, которые автоматизируют каждый этап разработки, тестирования и развертывания;
- пространства, позволяющие конфиденциально обсуждать и устранять угрозы безопасности, а затем публиковать информацию.
- В сочетании с возможностями Azure для мониторинга и оценки эти функции предоставляют превосходную службу для создания безопасных облачных решений.

### <a name="example"></a>Пример

Установки GitHub DevSecOps охватывают множество сценариев безопасности. Возможны следующие ситуации:

- разработчики, которые хотят использовать предварительно настроенные среды с возможностями по обеспечению безопасности;
- администраторы, которые рассчитывают на то, что всегда будут иметь под рукой актуальные отчеты о безопасности с указанием приоритетов, а также подробную информацию о затронутом коде и предлагаемые исправления;
- оптимизированные организации, которым нужны системы для автоматического получения новых и надежных устройств безопасности, когда секреты остаются открытыми в коде;
- команды разработчиков, которые могут получить выгоду от автоматического обновления, когда станут доступными новые или более безопасные версии внешних пакетов.

Дополнительные материалы:

- [DevSecOps в GitHub: идеи, связанные с решением Azure | Документация Майкрософт](/azure/architecture/solution-ideas/articles/devsecops-in-github)
- [Сканирование кода в репозитории GitHub с использованием расширенных средств безопасности GitHub в конвейере Azure DevOps](https://github.blog/2020-10-27-code-scanning-a-github-repository-using-github-advanced-security-within-an-azure-devops-pipeline/)
- [Применение DevSecOps к цепочке поставки ПО](https://github.blog/2020-12-03-applying-devsecops-to-your-software-supply-chain/)

## <a name="next-steps"></a>Следующие шаги

- Выберите команду внедрения (обычно это менеджер, управляющий разработчиками, и несколько разработчиков, определенных как администраторы) и разверните GitHub.
- Изучите общие и расширенные рабочие процессы Git, чтобы оптимизировать использование GitHub.

Дополнительные сведения о GitHub см. по приведенным ниже ссылкам.

- [Модули по GitHub в Microsoft Learn](/learn/browse/?products=github)
- [GitHub Learning Lab](https://lab.github.com/)
- [Документация по GitHub](https://docs.github.com/en)
- [Советы по началу работы с GitHub DevSecOps](https://resources.github.com/whitepapers/Architects-guide-to-DevOps/)
