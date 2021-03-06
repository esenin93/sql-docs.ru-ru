---
title: Функции (расширения интеллектуального анализа данных) | Документы Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- VBA [DMX]
- stored procedures [DMX]
- functions [DMX]
- Excel [DMX]
- Data Mining Extensions [Analysis Services], functions
ms.assetid: 75ab6346-f4a4-4699-90f3-66d35f930ed7
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 50a80c12549555f68a819de433faa39a1628a0c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="functions-dmx"></a>Функции (расширения интеллектуального анализа данных)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  При использовании расширений интеллектуального анализа данных (DMX) для запроса объектов в [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], можно использовать функции, чтобы получить дополнительные сведения, чем просто значения столбцов в модели интеллектуального анализа данных или входного набора данных. Например, с помощью запросов расширений интеллектуального анализа данных можно получить не только прогнозируемое значение столбца, но также и вероятность точности прогноза. Кроме функций расширений интеллектуального анализа данных можно использовать также функции языка Microsoft Visual Basic for Applications (VBA), Microsoft Excel, а также хранимые процедуры.  
  
## <a name="dmx-functions"></a>Функции (расширения интеллектуального анализа данных)  
 С помощью функций расширений интеллектуального анализа данных можно выполнять следующие задачи:  
  
-   получить прогноз;  
  
-   получить статистику по прогнозу, например вероятность и опорное значение;  
  
-   выполнить фильтрацию результатов запроса;  
  
-   повторно упорядочить табличное выражение.  
  
 Большинство функций расширений интеллектуального анализа данных возвращают скалярное значение, например опорное значение прогноза, но некоторые возвращают табличный результат. Например функция PredictHistogram возвращает таблицу, содержащую опорное значение и вероятность для каждого из состояний заданного прогнозируемого столбца. Результаты отображаются в виде нового табличного столбца.  
  
 **Дополнительные сведения:** [общие функции прогнозирования &#40;расширений интеллектуального анализа данных&#41;](../dmx/general-prediction-functions-dmx.md), [расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; функции ссылки](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Функции языка Visual Basic for Applications (VBA) и приложения Excel  
 В дополнение к функциям собственно расширений интеллектуального анализа данных в инструкциях расширений интеллектуального анализа данных можно также вызывать разнообразные функции языка VBA и приложения Excel. Например можно использовать функцию lCase изменить способ отображения столбца Attribute_Name в содержимом модели TM_Decision_Tree. Это показано в следующем образце кода.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Если же функция существует в VBA и Excel, необходимо добавить к имени функции в инструкции расширений интеллектуального анализа данных с помощью **VBA** или **Excel**. Например, можно вызвать функцию `VBA!Log` или `Excel!Log`. Если требуемая функция языка VBA или приложения Excel присутствует также в расширениях интеллектуального анализа данных и многомерных выражениях или она содержит символ знака доллара ($), необходимо заключить такую функцию в квадратные скобки ([]). Примером вызова подобной функции может быть `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Хранимые процедуры  
 Чтобы расширить функциональность расширений интеллектуального анализа данных можно создавать хранимые процедуры с помощью сред CLR. Например, модель интеллектуального анализа данных дерева регрессии возвращает коэффициенты, такие как A, B и т. д., описывающие уравнение регрессии, но модель не возвращает самого уравнения, например A + Bx = y. Однако можно написать хранимую процедуру, которая перемещается по схеме содержимого с помощью объекта модели интеллектуального анализа данных и возвращающую уравнение регрессии на выходе. Таким образом, инструкция расширений интеллектуального анализа данных может возвращать список уравнений регрессии как часть результата запроса.  
  
 **Дополнительные сведения:** [Управление сборками многомерной модели](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>См. также  
 [Расширения интеллектуального анализа данных & #40; расширений интеллектуального анализа данных & #41; Ссылка](../dmx/data-mining-extensions-dmx-reference.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; функции ссылки](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; Справочник по операторам](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Расширения интеллектуального анализа данных & #40; расширений интеллектуального анализа данных & #41; Справка по инструкции](../dmx/data-mining-extensions-dmx-statements.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; синтаксические обозначения](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; элементы синтаксиса](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Общие функции прогнозирования &#40;расширений интеллектуального анализа данных&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Структура и использовании прогнозирующих запросов расширений интеллектуального анализа данных](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Общие сведения об инструкции SELECT в расширении интеллектуального анализа данных](../dmx/understanding-the-dmx-select-statement.md)  
  
  
