---
title: Развертывание плана внедрения в облако в Azure DevOps
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Развертывание шаблона для плана внедрения в облако
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 91c1433f300efc3950cb54852a00b5020a992e8f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833730"
---
# <a name="cloud-adoption-plan-and-azure-devops"></a>План внедрения в облако и Azure DevOps

Azure DevOps — это набор облачных средств для клиентов Azure, которые управляют итеративными проектами. Он также включает средства для управления конвейерами развертывания и другие важные аспекты DevOps. 

В этой статье вы узнаете, как быстро развернуть невыполненную работу в Azure DevOps с помощью шаблона плана внедрения в облако. Этот шаблон соответствует усилиям по внедрению облака в стандартизированный процесс на основе руководств по облачной инфраструктуре внедрения.

## <a name="create-your-cloud-adoption-plan"></a>Создание плана внедрения в облако

Чтобы развернуть план внедрения в облако, откройте [демонстрационный генератор Azure DevOps](https://aka.ms/adopt/plan/generator). Этот инструмент развернет шаблон в клиенте Azure DevOps. Для использования этого средства необходимо выполнить следующие действия.

1. Убедитесь, что **выбранное поле шаблона** имеет значение **план внедрения в облако**. Если это не так, выберите **пункт Выбрать шаблон** , чтобы выбрать подходящий шаблон.
2. Выберите организацию Azure DevOps в раскрывающемся списке **выбрать организацию** .
3. Введите имя нового проекта. План внедрения в облако будет иметь это имя при развертывании в клиенте Azure DevOps.
4. Выберите **создать проект** , чтобы создать новый проект в клиенте на основе шаблона плана. Индикатор выполнения показывает ход выполнения развертывания проекта.
5. После завершения развертывания выберите **Переход к проекту** , чтобы увидеть новый проект.

После создания проекта перейдите к этой статье, чтобы увидеть, как можно изменить шаблон, чтобы он совпадал с планом внедрения в облако.

Дополнительную техническую поддержку и рекомендации по этому средству см. в разделе [Azure DevOps Services демонстрационный генератор](https://docs.microsoft.com/azure/devops/demo-gen/?toc=%2Fazure%2Fdevops%2Fdemo-gen%2Ftoc.json&bc=%2Fazure%2Fdevops%2Fdemo-gen%2Fbreadcrumb%2Ftoc.json&view=azure-devops).

## <a name="bulk-edit-the-cloud-adoption-plan"></a>Групповое изменение плана внедрения в облако

После развертывания проекта плана можно использовать Microsoft Excel для его изменения. Гораздо проще создавать новые рабочие нагрузки или активы в плане с помощью Excel, чем с помощью интерфейса браузера Azure DevOps.

Сведения о подготовке рабочей станции к групповому редактированию см. в разделе [Добавление или изменение рабочих элементов с помощью Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="use-the-cloud-adoption-plan"></a>Использование плана внедрения в облако

План внедрения в облако упорядочивает действия по типу действия:

- **Ситуаций**: *История* представляет собой общий этап жизненного цикла внедрения в облако.
- **Функции**: Функции используются для организации конкретных целей на каждом этапе. Например, миграция определенной рабочей нагрузки будет одной функцией.
- **Пользовательские истории**: Группа «истории пользователей» работает с логическими коллекциями действий на основе определенной цели.
- **Задачи**: Задачи — это фактическая работа, которую необходимо выполнить.

На каждом уровне действия последовательно определяются на основе зависимостей. Действия связаны с статьями в облачной инфраструктуре внедрения для уточнения цели или задачи.

Самое ясное представление плана внедрения в облако поступает из представления невыполненной работы **ситуаций** . Справку по переходу на представление невыполненной работы **ситуаций** см. в статье о просмотре невыполненной [работы](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops#view-a-backlog-or-portfolio-backlog). Из этого представления можно легко спланировать и управлять работой, необходимой для завершения текущего этапа жизненного цикла перехода.

> [!NOTE]
> Текущее состояние плана внедрения в облако сосредоточено на интенсивности миграции. Задачи, относящиеся к управлению, инновациям или операциям, необходимо заполнить вручную.

## <a name="align-the-cloud-adoption-plan"></a>Выровняйте план внедрения в облако

Обзорные страницы этапов стратегии и планирования жизненного цикла внедрения облака каждый ссылаются на [шаблон стратегии и планирования инфраструктуры внедрения в облако](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Этот шаблон организует решения и точки данных, которые выключают шаблон для плана внедрения в облако с конкретными планами для внедрения. Если вы еще не сделали этого, вам может потребоваться выполнить упражнения, связанные с [стратегией](../business-strategy/index.md) и [планированием](../plan/index.md) , до согласования нового проекта.

Следующие статьи поддерживают выравнивание плана внедрения в облако.

- [Рабочие нагрузки](./workloads.md): Выровняйте компоненты в Миграция в облаконой ситуации, чтобы записать каждую рабочую нагрузку, которую необходимо перенести или разместить в современном объеме. Добавьте и измените эти функции, чтобы зафиксировать усилия по переносу первых 10 рабочих нагрузок.
- [Активы](./assets.md): Каждый ресурс (виртуальная машина, приложение или данные) представляется пользовательскими историями в каждой рабочей нагрузке. Добавляйте и изменяйте эти пользовательские истории, чтобы они были согласованы с вашим цифровым пространством.
- [Рационализация](./review-rationalization.md): По мере определения каждой рабочей нагрузки изначальные предположения о рабочей нагрузке могут быть вызваны. Это может привести к изменениям задач в каждом ресурсе.
- [Создание планов выпуска](./iteration-paths.md): Пути итераций устанавливают планы выпусков путем согласования усилий с различными выпусками и итерациями.
- [Создание временных шкал](./timelines.md): Определение дат начала и окончания для каждой итерации создает временную шкалу для управления общим проектом.

Эти пять статей содержат сведения о каждой задаче выравнивания, необходимой для начала управления вашими усилиями по внедрению. Следующий шаг позволяет начать упражнение по выравниванию.

## <a name="next-steps"></a>Следующие шаги

Начните выровняйте проект плана путем [определения и приоритизации рабочих нагрузок](./workloads.md).

> [!div class="nextstepaction"]
> [Определение и определение приоритетов рабочих нагрузок](./workloads.md)