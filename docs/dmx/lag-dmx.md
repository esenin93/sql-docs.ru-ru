---
title: Lag (расширения интеллектуального анализа данных) | Документы Microsoft
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
f1_keywords:
- LAG
dev_langs:
- DMX
helpviewer_keywords:
- Lag function
ms.assetid: 2da6df1a-5506-4871-a0f0-83292f1df41e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 929924bc7ef571a64bc4d7f6c26d20dece081821
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="lag-dmx"></a>Lag (расширения интеллектуального анализа данных)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Возвращает временной срез между датой текущего варианта и последней датой тренировочного набора.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 Скалярное значение целочисленного типа.  
  
## <a name="remarks"></a>Замечания  
 Если **запаздывания** функция используется в модели, где размещен во вложенной таблице столбец KEY TIME, функция должна размещаться внутри вложенного списка выбора инструкции.  
  
## <a name="examples"></a>Примеры  
 Следующий пример возвращает варианты, которые были использованы для обучения модели за последние 12 месяцев.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>См. также  
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; функции ссылки](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Функции &#40;расширений интеллектуального анализа данных&#41;](../dmx/functions-dmx.md)   
 [Общие функции прогнозирования &#40;расширений интеллектуального анализа данных&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
