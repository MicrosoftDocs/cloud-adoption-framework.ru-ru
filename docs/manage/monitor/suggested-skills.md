---
title: Готовность навыков мониторинга в облаке
description: Готовность навыков мониторинга в облаке
author: BrianBlanchard
ms.author: magoedte
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6672d86f215360f1024b233f62a48eb390b52a52
ms.sourcegitcommit: d88c1cc3597a83ab075606d040ad659ac4b33324
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2020
ms.locfileid: "84785180"
---
<!-- cSpell:ignore kusto ITIL -->

# <a name="skills-readiness-for-cloud-monitoring"></a>Готовность навыков мониторинга в облаке

На этапе планирования процесса миграции цель состоит в разработке планов, необходимых для пошагового внедрения. Эти планы также должны включать в себя способ работы с этими рабочими нагрузками перед их переходом или выпуском в рабочую среду, а не впоследствии. ИТ-заинтересованные лица предполагают наличие ценных услуг и предполагают их без перерывов в работе. Сотрудники отдела ИТ понимают, что им нужно изучить новые навыки и адаптировать их, чтобы они были готовы к уверенному использованию интегрированных служб Azure для эффективного мониторинга ресурсов в Azure и гибридных средах.

Для разработки необходимых навыков можно использовать следующие схемы обучения. Они организованы начиная с изучения основ, а затем делятся на три основных домена субъектов — инфраструктуру, приложение и анализ данных.  

## <a name="fundamentals"></a>Основы

- Общие сведения о [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) обсуждаются основные принципы управления и развертывания ресурсов Azure. ИТ-специалисты, управляющие мониторингом на предприятии, должны понимать области управления, управление доступом на основе ролей (RBAC), используя. Azure Resource Manager шаблоны и управление ресурсами с помощью Azure CLI и Azure PowerShell.

- Введение в [политику Azure](https://docs.microsoft.com/azure/governance/policy/overview) поможет вам узнать, как использовать политику Azure для создания и назначения политик, а также управления ими. Политика Azure позволяет развертывать и настраивать агенты Azure Monitor, включать мониторинг с помощью Azure Monitor для виртуальных машин и центра безопасности Azure, развертывать параметры диагностики, проверять параметры гостевой конфигурации и многое другое.

- Общие сведения о [интерфейсе командной строки Azure (CLI)](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), который представляет собой возможности командной строки для управления ресурсами Azure на разных платформах. Также ознакомьтесь с введением в [Azure PowerShell](https://docs.microsoft.com/powershell/azure/?view=azps-3.6.1). Предложения LinkedIn в рамках [обучающего курса обучение средствам управления Azure](https://www.linkedin.com/learning/learning-azure-management-tools), семинарам, охватывающим Azure CLI и языки программирования PowerShell:

  - [Используйте Azure CLI](https://www.linkedin.com/learning/learning-azure-management-tools/use-the-azure-cli).
  - [Getting started with Azure PowerShell](https://www.linkedin.com/learning/learning-azure-management-tools/understand-azure-powershell) (Приступая к работе с Azure PowerShell)

- Узнайте, как защитить ресурсы с помощью политик, управления доступом на основе ролей и других служб Azure, просмотрев [реализацию безопасности управления ресурсами в Azure](https://docs.microsoft.com/learn/paths/implement-resource-mgmt-security).

- Общие сведения о [мониторинге Microsoft Azure ресурсы и рабочие нагрузки](https://app.pluralsight.com/library/courses/microsoft-azure-resources-workloads-monitoring-update/table-of-contents) позволяют узнать, как использовать средства мониторинга Microsoft Azure для мониторинга сетевых ресурсов Azure, а также локальных ресурсов.

## <a name="infrastructure-monitoring"></a>Мониторинг инфраструктуры

- [Разработка стратегии мониторинга для инфраструктуры в Microsoft Azure](https://www.pluralsight.com/courses/microsoft-azure-monitoring-strategy-infrastructure-design-update) помогает изучить фундаментальные сведения о возможностях мониторинга и решениях в Azure.

- Сведения о мониторинге кластеров [Kubernetes](https://www.youtube.com/watch?time_continue=3&v=RjsNmapggPU&feature=emb_logo) см. в глубоком подробном обзоре мониторинга кластера Kubernetes с Azure Monitor для контейнеров.

- Узнайте, Azure Monitor как отслеживать данные из службы [хранилища Azure и HDInsight](https://www.pluralsight.com/courses/microsoft-azure-data-storage-monitoring).

- [Microsoft Azure мониторинг базы данных сборник тренировочных заданий](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) исследует ключевые возможности мониторинга, которые можно использовать для получения подробных сведений и действий, которые могут быть использованы для базы данных SQL Azure, хранилища данных SQL azure и Azure Cosmos DB.

- [Мониторинг Microsoft Azure гибридных облачных сетей](https://www.pluralsight.com/courses/microsoft-azure-hybrid-cloud-networks-monitoring) — это расширенный курс, который поможет вам узнать, как использовать средства мониторинга Azure для визуализации, обслуживания и оптимизации виртуальных сетей Azure и подключений виртуальной частной сети для реализации гибридного облака.

- С помощью [дуги Azure для серверов](https://docs.microsoft.com/azure/azure-arc/servers/overview)вы узнаете, как управлять компьютерами под управлением Windows и Linux, размещенными за пределами Azure, аналогично управлению собственными виртуальными машинами Azure.

## <a name="application-monitoring"></a>Мониторинг приложений

- Узнайте, как [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) помогает просматривать доступность и производительность приложений и служб вместе в одном месте. Pluralsight предлагает следующие курсы, которые помогут вам:

  - [Microsoft Azure инженер DevOps: оптимизация механизмов обратной связи](https://www.pluralsight.com/courses/microsoft-azure-optimize-feedback-mechanisms) помогает подготовиться к использованию Azure Monitor, включая Application Insights, для мониторинга и оптимизации веб-приложений.

  - [Microsoft Azure Developer: Мониторинг производительности](https://app.pluralsight.com/library/courses/microsoft-azure-performance-monitoring). Приступайте к работе с этим курсом по использованию Azure Monitor Application Insights для комплексного мониторинга компонентов приложений, работающих в Azure.
  
  - [Microsoft Azure мониторинга базы данных сборник тренировочных заданий](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) поможет вам узнать, как реализовать и использовать мониторинг базы данных SQL Azure, хранилища данных SQL azure и Azure Cosmos DB.

  - [Инструментирование приложений с помощью Azure Monitor Application Insights](https://app.pluralsight.com/library/courses/microsoft-azure-application-insights-web-application-instrument) является подробным курсом, посвященным использованию пакета SDK Application Insights для сбора данных телеметрии и событий из приложения с помощью угловых и Node.js компонентов.

  - [Отладка и профилирование приложений](https://www.pluralsight.com/courses/devintersection-azureai-session-31) — это запись из сеанса конференции Майкрософт по использованию и интерпретации данных, предоставляемых Azure Monitor Application Insights snapshot Debugger и Profiler.

## <a name="data-analysis"></a>Анализ данных

- Узнайте, как создавать [запросы журналов в Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries). Язык запросов Kusto — это основной ресурс для написания запросов журналов Azure Monitor для изучения и анализа данных журнала между собранными данными из Azure и зависимостями приложений с гибридными ресурсами, включая активное приложение.

- [Язык запросов Kusto (ККЛ) с нуля](https://www.pluralsight.com/courses/kusto-query-language-kql-from-scratch) — это полный курс, включающий в себя подробные примеры, охватывающие широкий спектр вариантов использования и методов для анализа журналов в Azure Monitor журналов.

## <a name="deeper-skills-exploration"></a>Углубленное изучение навыков

Помимо этих первоначальных вариантов развития навыков доступны различные варианты обучения.

### <a name="typical-mappings-of-cloud-it-roles"></a>Типичные сопоставления облачных ИТ-ролей

Корпорация Майкрософт и партнеры предлагают различные образовательные программы для любой аудитории в целях развития навыков работы со службами Azure.

- [Центр Microsoft IT Pro для карьеры](https://www.microsoft.com/itpro): служит бесплатным онлайн-ресурсом для соответствия пути вашей облачной карьеры. Узнайте, что эксперты из отрасли предлагают для вашей облачной роли и какие навыки там можно получить. Выполните учебный курс в удобном для вас темпе для развития наиболее необходимых навыков, чтобы оставаться ценным и востребованным сотрудником.

Ваши знания Azure заслуживают официального признания. [Воспользуйтесь нашими сертификационными программами и сдайте экзамены по Microsoft Azure]( https://www.microsoft.com/learning/certification-overview.aspx).

## <a name="azure-devops-and-project-management"></a>Управление DevOps и проектом Azure

Гибридная облачная среда прерывает работу с неопределенными ролями, обязанностями и действиями. Организациям необходимо перейти на современные методики управления службами, в том числе гибкие и DevOps методологии, чтобы лучше удовлетворить потребности преобразования и оптимизации современных бизнес-процессов с оптимизацией и эффективным способом.

В рамках миграции на облачную платформу мониторинга ИТ-группа, ответственная за управление мониторингом в Организации, должна включать в себя гибкие возможности обучения и участия в действиях DevOps. Это также _относится к разработке в DevOps_ , принимая требования и применяя их к гибким требованиям, чтобы обеспечить минимально приемлемые решения для мониторинга, которые последовательно обновляются и в соответствии с потребностями бизнеса. Чтобы система управления версиями управляла пакетами решений итеративного мониторинга и другими связанными материалами, подключите проект Azure DevOps Server к репозиторию GitHub Enterprise Server. Это обеспечивает связь между фиксациями и запросами на вытягивание для рабочих элементов GitHub. Вы можете использовать GitHub Enterprise для разработки при интеграции и развертывании непрерывного мониторинга, используя Azure Boards для планирования и отслеживания работы.

Чтобы узнать больше, ознакомьтесь со следующими сведениями.

- Приступая [к работе с Azure DevOps](https://docs.microsoft.com/learn/modules/get-started-with-devops).

- [Узнайте о курсе "DevOps dojo white belt foundation"](https://docs.microsoft.com/learn/paths/devops-dojo-white-belt-foundation)

- [Развитие практик DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)

- [Автоматизация развертываний с помощью Azure DevOps](https://docs.microsoft.com/learn/paths/automate-deployments-azure-devops)

## <a name="other-considerations"></a>Другие вопросы

Клиенты часто сталкиваются с затруднениями в управлении, обслуживании и доставке ожидаемого бизнеса (и ИТ-организации) для тех услуг, за которые она поставляется. Мониторинг считается базовым для управления инфраструктурой и бизнесом, и он посвящен измерению качества обслуживания и взаимодействия с клиентами. Чтобы достичь этих целей, разработайте фундамент с помощью ITSM в сочетании с DevOps, что поможет группе мониторинга, как она управляет, доставляет и поддерживает службу мониторинга. Внедрение ITSM Framework позволяет группе мониторинга работать как поставщик и получить признание в качестве доверенного бизнес-средства, выполнив согласование с стратегическими целями и потребностями Организации.

Ознакомьтесь со следующими сведениями, чтобы ознакомиться с обновлениями, внесенными в самый популярный [технический документ ITSM Framework версии 4 и облачных вычислений](https://www.axelos.com/case-studies-and-white-papers/itil-4-and-the-cloud), который посвящен присоединению существующих руководств по ITIL с рекомендациями от DevOps, Agile и экономичного. Также рассмотрим [эталонную архитектуру IT4IT](https://www.opengroup.org/it4it) , которая предоставляет альтернативную схему для преобразования ее с помощью независимой от процесса платформы.

## <a name="learn-more"></a>Подробнее

Чтобы найти дополнительные схемы обучения, перейдите к [каталогу Microsoft Learn](https://docs.microsoft.com/learn/browse). Используйте фильтр ролей для согласования путей обучения со своей ролью.
