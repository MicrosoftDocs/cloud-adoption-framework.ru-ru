---
title: Определение машинного обучения во время развертывания
description: Сведения о том, как модель искусственного интеллекта делает прогнозы при развертывании в рабочей среде.
author: DonnaForlin
ms.author: brblanch
ms.date: 01/20/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: think-tank
ms.openlocfilehash: c6fe231f81324815f8004a6ed3408ab326a6be02
ms.sourcegitcommit: 9e4bc0e233a24642853f5e8acbeb9746b2444024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "102115107"
---
# <a name="machine-learning-inference-during-deployment"></a>Определение машинного обучения во время развертывания

При развертывании модели искусственного интеллекта во время рабочей среды необходимо учитывать, как она будет выполнять прогнозы. Ниже приведены два основных процесса для моделей искусственного интеллекта.

- **Вывод пакета:** Асинхронный процесс, который основывает свои прогнозы на пакете наблюдений. Прогнозы хранятся в виде файлов или в базе данных для конечных пользователей или бизнес-приложений.

- **Вывод в реальном времени (или интерактивное):** Освобождает модель для создания прогнозов в любое время и запускает немедленное реагирование. Этот шаблон можно использовать для анализа потоковой и интерактивной информации приложения.

Примите во внимание следующие вопросы, чтобы оценить модель, сравнить эти два процесса и выбрать ту, которая подходит для вашей модели:

- Как часто должны создаваться прогнозы?
- Как скоро будут нужны результаты?
- Должны ли прогнозы создаваться по отдельности, в небольших пакетах или в больших пакетах?
- Ожидается ли задержка от модели?
- Сколько мощности вычислений требуется для выполнения модели?
- Существуют ли эксплуатационные последствия и затраты на обслуживание модели?

Следующее дерево решений поможет определить, какая модель развертывания лучше подходит для вашего варианта использования:

[![Схема дерева принятия решений в режиме реального времени или вывода пакетов.](./media/inference-decision-tree.png)](./media/inference-decision-tree.png#lightbox)

## <a name="batch-inference"></a>Вывод пакета

Вывод пакета, иногда называемый «автономным выводом», является простым процессом вывода, который помогает моделям запускаться в течение интервалов времени и бизнес-приложений для хранения прогнозов.

Примите во внимание следующие рекомендации по выводу пакетов.

- **Оценка пакета активации:** Используйте Машинное обучение Azure конвейеры и `ParallelRunStep` функцию в машинное обучение Azure, чтобы настроить расписание или автоматизацию на основе событий. Перейдите к показу AI для выполнения [пакетного вывода с помощью `ParallelRunStep` машинное обучение Azure](https://channel9.msdn.com/Shows/AI-Show/How-to-do-Batch-Inference-using-AML-ParallelRunStep) и Узнайте больше о процессе.

- **Параметры вычисления для вывода пакета:** Поскольку процессы вывода пакетов не выполняются постоянно, рекомендуется автоматически запускать, прекращать и масштабировать многократно используемые кластеры, которые могут обрабатывать ряд рабочих нагрузок. Для разных моделей требуются разные среды, и решение должно иметь возможность развернуть определенную среду и удалить ее, когда вывод будет доступен для следующей модели. Чтобы определить нужный вычислительный экземпляр для модели, см. следующее дерево решений.

  [![Диаграмма дерева решений вычислений.](./media/compute-decision-tree.png)](./media/compute-decision-tree.png#lightbox)

- **Реализация вывода пакета:** Azure поддерживает несколько функций для вывода пакетов. Одна из функций находится `ParallelRunStep` в машинное обучение Azure, что позволяет клиентам получать ценные сведения из терабайтов структурированных или неструктурированных данных, хранящихся в Azure. `ParallelRunStep` предоставляет готовый параллелизм и работает в Машинное обучение Azure конвейерах.

- **Проблемы вывода пакетов:** Хотя вывод пакета — это более простой способ использования и развертывания модели в рабочей среде, он выдает проблемы.

  - В зависимости от частоты выполнения вывода получаемые данные могут быть несущественными по времени доступа.

  - Разновидность проблемы холодного запуска; результаты могут быть недоступны для новых данных. Например, если новый пользователь создает учетную запись и начинает покупку с розничной системой рекомендаций, рекомендации по продукту не будут доступны до следующего выполнения вывода пакета. Если это препятствием для вашего случая использования, рассмотрите возможность вывода в реальном времени.

  - Развертывание в нескольких регионах и высокий уровень доступности не является критически важным фактором в сценарии вывода пакета. Модель не требуется развертывать по регионам, а хранилище данных может быть развернуто с помощью стратегии высокого уровня доступности во многих местах. Как правило, это соответствует проектированию и стратегии высокого уровня доступности приложений.

## <a name="real-time-inference"></a>Вывод в реальном времени

В режиме реального времени или интерактивном выводе выводятся архитектуры, в которых определение модели может быть активировано в любое время, и ожидается немедленное реагирование. Этот шаблон можно использовать для анализа потоковых данных, интерактивных данных приложений и многого другого. Этот режим позволяет использовать преимущества модели машинного обучения в режиме реального времени и разрешает проблему холодного запуска, описанную выше в разделе "вывод пакета".

Следующие соображения и рекомендации доступны, если для вашей модели выводятся сведения о выводе в реальном времени.

- Проблемы, связанные с **выводом в реальном времени:** Требования к задержке и производительности делают архитектуру вывода в реальном времени более сложной для вашей модели. Системе может потребоваться ответить в течение 100 миллисекунд или менее, в течение которого ему необходимо получить данные, выполнить определение, проверить и сохранить результаты модели, выполнить необходимую бизнес-логику и вернуть результаты в систему или приложение.

- **Параметры вычисления для вывода в режиме реального времени:** Лучшим способом реализации вывода в режиме реального времени является развертывание модели в форме контейнера в кластере DOCKER или AKS и предоставление его в качестве веб-службы с REST API. Таким образом, модель выполняется в собственной изолированной среде и может управляться как любая другая веб-служба. Затем можно использовать возможности DOCKER и AKS для управления, мониторинга, масштабирования и многого другого. Модель может быть развернута локально, в облаке или на границе. Предыдущее решение по вычислению вычислений описывает вывод в реальном времени.

- **Развертывание в многорегионом и высокий уровень доступности:** Необходимо учитывать региональные развертывания и архитектуры высокого уровня доступности в сценариях вывода в режиме реального времени, так как задержка и производительность модели будут критически важными для устранения. Чтобы сократить задержку в многорегионовых развертываниях, рекомендуется нахождение модели как можно ближе к точке потребления. Модель и вспомогательная инфраструктура должны соответствовать принципам высокой доступности и стратегии аварийного восстановления бизнеса.

## <a name="many-models-scenario"></a>Сценарий "многие модели"

Модель в единственном числе может не иметь возможности захватывать сложную природу реальных проблем, например прогнозировать продажи для супермаркете, где демографические данные, марки, номера SKU и другие функции могут значительно варьироваться. Регионы могут существенно варьироваться в разработке прогнозируемого обслуживания для смарт-измерительных приборов. Наличие многих моделей для этих сценариев для захвата региональных данных или отношений уровня хранилища может привести к более высокой точности по сравнению с одной моделью. Этот подход предполагает, что для этого уровня гранулярности доступно достаточно данных.

На высоком уровне сценарий с множеством моделей происходит в три этапа: источник данных, обработка и анализ данных и многие модели.

[![Схема сценария с множеством моделей.](./media/many-models-scenario.png)](./media/many-models-scenario.png#lightbox)

**Источник данных:** Важно сегментировать данные без слишком большого количества элементов на этапе источника данных. КОД продукта или штрихкод не должен быть разделен на основной раздел, так как это приведет к созданию слишком большого количества сегментов и может препятствовать осмысленным моделям. Торговая марка, номер SKU или локализация могут быть более подгонки. Также важно хоможенизе данные, удалив аномалии, которые будут расклонять распределение данных.

Анализ и анализ **данных:** Несколько экспериментов выполняются параллельно для каждой секции данных на этапе обработки и анализа данных. Обычно это итеративный процесс, при котором модели из экспериментов оцениваются для определения наиболее подходящего из них.

**Многие модели:** Лучшие модели для каждого сегмента или категории регистрируются в реестре модели. Присвойте моделям значимые имена, что сделает их более обнаруживаемыми для определения. Используйте теги, если это необходимо, чтобы сгруппировать модель в определенные категории.

## <a name="batch-inference-for-many-models"></a>Вывод пакетов для многих моделей

Во время вывода пакета для многих моделей прогнозы обычно планируются, повторяются и могут работать с большими объемами данных, выполняемых одновременно. В отличие от сценария с одной моделью, одновременное определение многих моделей и важно выбрать правильные. На следующей схеме показан шаблон ссылки для вывода пакета многими моделями.

[![Схема эталонного шаблона для многих моделей вывода пакетов.](./media/many-models-batch-inference.png)](./media/many-models-batch-inference.png#lightbox)

Основная цель этого шаблона — наблюдать за моделью и запускать несколько моделей одновременно для достижения высокомасштабируемого решения о выводе, которое может обрабатывать большие объемы данных. Для достижения иерархической модели можно разделить многие модели на категории. Каждая категория может иметь собственное хранилище вывода, например Azure Data Lake. При реализации этого шаблона необходимо сбалансировать масштабирование моделей по горизонтали и вертикали, так как это повлияет на стоимость и производительность. Выполнение слишком большого количества экземпляров модели может повысить производительность, но повлияет на затраты. Слишком малое количество экземпляров с высокими узлами спецификаций может быть более экономичным, но может привести к проблемам с масштабированием.

## <a name="real-time-inference-for-many-models"></a>Вывод в режиме реального времени для многих моделей

Для вывода многих моделей в реальном времени требуется низкая задержка и запросы по запросу, обычно через конечную точку RESTFUL. Это полезно, когда внешним приложениям или службам требуется стандартный интерфейс для взаимодействия с моделью, обычно через интерфейс RESTFUL с полезной нагрузкой JSON.

[![Схема вывода данных из множества моделей в режиме реального времени.](./media/many-models-real-time-inference.png)](./media/many-models-real-time-inference.png#lightbox)

Основная цель этого шаблона — использовать службу обнаружения для обнаружения списка служб и их метаданных. Это может быть реализовано в виде функции Azure и позволяет клиентам получать релевантные сведения о службе, которые можно вызывать с помощью URI защищенной части. В службу отправляются полезные данные JSON, которые вызовите соответствующую модель и обеспечивают ответ JSON обратно клиенту.

Каждая служба имеет микрослужбу без отслеживания состояния, которая может одновременно обслуживать несколько запросов и ограничена физическим ресурсом виртуальной машины. Служба может развернуть несколько моделей, если выбрано несколько групп. для этого рекомендуются однородные группы, такие как категория, SKU и другие. Сопоставление между запросом на обслуживание и моделью, выбранной для данной службы, должно быть помогут в логику вывода, обычно через скрипт оценки. Если размер моделей относительно мал (несколько мегабайт), рекомендуется загружать их в память в целях повышения производительности. в противном случае каждая модель может динамически загружаться на каждый запрос.

## <a name="next-steps"></a>Дальнейшие действия

Изучите следующие ресурсы, чтобы узнать больше об использовании Машинное обучение Azure.

- [Создание конвейеров Машинного обучения Azure для пакетной оценки](/azure/machine-learning/tutorial-pipeline-batch-scoring-classification)
- [Выполнение прогнозирования пакетной службы с помощью конструктора Машинное обучение Azure](/azure/machine-learning/how-to-run-batch-predictions-designer)
- [Вывод пакета в Машинное обучение Azure](https://techcommunity.microsoft.com/t5/azure-ai/batch-inference-in-azure-machine-learning/ba-p/1417010#:~:text=%20Batch%20Inference%20in%20Azure%20Machine%20Learning%20,Learning%20Pipelines.%20ParallelRunStep%20is%20available%20through...%20More%20)
