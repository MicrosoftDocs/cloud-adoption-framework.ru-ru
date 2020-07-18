---
title: Машинное обучение
description: Эти контрольные списки и ресурсы помогут вам спланировать разработку и развертывание приложений.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3cbc697e979f741342c3a75f38de8f4086cb4871
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452256"
---
<!-- cSpell:ignore scikit RLlib ONNX Jupyter -->

# <a name="machine-learning"></a>Машинное обучение

Azure предоставляет вам более широкие возможности машинного обучения. Быстро и легко создавайте, обучите и развертывайте модели машинного обучения с помощью Машинное обучение Azure. Машинное обучение Azure можно использовать для любого рода машинного обучения, от классического машинного обучения до глубокого обучения, защищенного и неконтролируемого обучения. Если вы предпочитаете писать код Python или R, а также параметры с нулевым кодом или с низким кодом, такие как [конструктор](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score), вы можете создавать, обучать и отслеживанию высокоточных моделей машинного обучения и модели глубокого обучения в машинное обучение Azure рабочей области.

Вы даже можете начать обучение на локальном компьютере, а затем масштабировать его в облако. Служба также взаимодействует с популярными средствами для глубокого обучения и подкреплением с открытым исходным кодом, такими как PyTorch, TensorFlow, scikit-Learning, Ray и Рллиб.

Приступая к работе с [машинное обучение Azure](https://docs.microsoft.com/azure/machine-learning/). Вы найдете учебник по [началу работы с первым экспериментом машинного обучения](https://docs.microsoft.com/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Дополнительные сведения о формате модели с открытым исходным кодом и среде выполнения для машинного обучения см. в [среде выполнения ONNX](http://onnxruntime.ai).

Ниже приведены распространенные сценарии для решений машинного обучения.

- Прогнозное обслуживание
- Управление запасами
- Обнаружение мошенничества.
- Прогнозирование спроса
- Интеллектуальные рекомендации
- Прогнозирование продаж

## <a name="checklist"></a>Контрольный список

- Приступая к **работе, сначала ознакомьтесь с машинное обучение Azure**, а затем выберите, с каким опытом начать. Вы можете следовать инструкциям, чтобы использовать записную книжку Jupyter с Python, визуальный интерфейс перетаскивания или автоматизированное машинное обучение (Аутомл).

  - [Обзор Машинное обучение Azure](https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml)
  - [Создание первого эксперимента машинного обучения с помощью Jupyter Notebook с помощью Python](https://docs.microsoft.com/azure/machine-learning/tutorial-1st-experiment-sdk-setup)
  - [Визуальные эксперименты и перетаскивание](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score)
  - [Использование пользовательского интерфейса Аутомл](https://docs.microsoft.com/azure/machine-learning/tutorial-first-experiment-automated-ml)
  - [Настройка среды разработки](https://docs.microsoft.com/azure/machine-learning/how-to-configure-environment)

- **Поэкспериментируйте с более сложными руководствами** для прогнозирования расходов на такси, классификации образов и создания конвейера для пакетной оценки.

  - [Использование Аутомл для прогнозирования расходов на такси](https://docs.microsoft.com/azure/machine-learning/tutorial-auto-train-models)
  - [Классификация образов с помощью scikit — обучение](https://docs.microsoft.com/azure/machine-learning/tutorial-train-models-with-aml)
  - [Создание конвейеров Машинного обучения Azure для пакетной оценки](https://docs.microsoft.com/azure/machine-learning/tutorial-pipeline-batch-scoring-classification)

- Ознакомьтесь **с видеороликами** , чтобы узнать больше о преимуществах машинное обучение Azure, включая сборку модели без кода, Млопс, среду выполнения ONNX, интерпретацию модели и прозрачность, а также многое другое.

  - [Новые возможности Машинное обучение Azure](https://channel9.msdn.com/Shows/AI-Show/Allup-Azure-ML)
  - [Использование Аутомл для построения моделей](https://aka.ms/automlvideo)
  - [Создание моделей с нулевым кодом с помощью конструктора Машинное обучение Azure](https://aka.ms/studioanddesigner)
  - [Млопс для управления сквозным жизненным циклом](https://aka.ms/mlopsvideo)
  - [Включение среды выполнения ONNX в модели](https://www.youtube.com/watch?v=qy7X2JGLUC4)
  - [Интерпретируемость и прозрачность модели](https://aka.ms/azuremlinterpret)
  - [Создание моделей с помощью R](https://aka.ms/Rmodels)

- [Обзор эталонных архитектур для решений искусственного интеллекта](https://docs.microsoft.com/azure/architecture/browse/#ai--machine-learning)

## <a name="next-steps"></a>Дальнейшие действия

Изучите другие категории решений искусственного интеллекта:

- [Приложения и агенты AI](./ai-applications.md)
- [Интеллектуальный анализ знаний](./knowledge-mining.md)
