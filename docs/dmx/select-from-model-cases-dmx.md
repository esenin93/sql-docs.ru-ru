---
title: SELECT FROM &lt;модели&gt;. ВАРИАНТЫ (DMX) | Документы Microsoft
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
- SELECT
- CASES
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <model>.CASES statement
- drillthrough [DMX]
ms.assetid: d58acb47-aaa6-40b7-b8c4-6a6700fbc1dd
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dfbac38cd1083ffe21c5e3117a8db2d9dbdb2ac1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM &lt;модели&gt;. ВАРИАНТЫ (РАСШИРЕНИЯ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Поддерживает детализацию и возвращает объекты, которые использовались для обучения модели. Кроме того, можно возвращать столбцы структуры, не включенные в модель, если и в структуре, и в модели интеллектуального анализа данных включена детализация и пользователь обладает необходимыми разрешениями.  
  
 Если детализация для модели интеллектуального анализа данных не включена, выполнение данной инструкции завершится ошибкой.  
  
> [!NOTE]  
>  Для расширений интеллектуального анализа данных активировать детализацию можно только при создании модели. Добавить детализацию в существующую модель можно с помощью среды [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], однако, прежде чем будет можно просматривать варианты и выполнять к ним запросы, необходимо выполнить повторную обработку модели.  
  
 Дополнительные сведения о включении детализации см. в разделе [CREATE MINING MODEL &#40;расширений интеллектуального анализа данных&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;расширений интеллектуального анализа данных&#41;](../dmx/select-into-dmx.md), и [ALTER MINING STRUCTURE &#40;Расширений интеллектуального анализа данных&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Аргументы  
 *n*  
 Необязательно. Целое число, указывающее количество возвращаемых строк.  
  
 *список выражений*  
 Список выражений с разделителями-запятыми. Выражение может включать в себя идентификаторы столбцов, определяемые пользователем функции, функции VBA и пр.  
  
 Чтобы включить столбец структуры, не включенный в модель интеллектуального анализа данных, используйте функцию `StructureColumn('<structure column name>')`.  
  
 *model*  
 Идентификатор модели.  
  
 *Условное выражение*  
 Условие ограничения значений, возвращаемых из списка столбцов.  
  
 *expression*  
 Необязательно. Выражение, возвращающее скалярное значение.  
  
## <a name="remarks"></a>Замечания  
 Если детализация включена как для модели, так и для структуры интеллектуального анализа данных, пользователи, являющиеся членами роли с разрешением на детализацию модели и структуры, могут обращаться к столбцам в структуре интеллектуального анализа данных, которые не включены в модель. Таким образом, чтобы защитить конфиденциальные или личные данные, следует создать представление источника данных для маскирования персональных данных и предоставления **AllowDrillthrough** для структуры интеллектуального анализа данных только в том случае, когда это необходимо.  
  
 [Запаздывания &#40;расширений интеллектуального анализа данных&#41; ](../dmx/lag-dmx.md) функция может использоваться совместно с временными рядами для вычислений и фильтрации на отрезках времени между выполнением вариантов начальное время.  
  
 С помощью [IsInNode &#40;расширений интеллектуального анализа данных&#41; ](../dmx/isinnode-dmx.md) функционировать в **ГДЕ** предложение возвращает только варианты, связанные с узлом, который указан в столбце NODE_UNIQUE_NAME набора строк схемы.  
  
## <a name="examples"></a>Примеры  
 Следующие примеры основаны на структуре интеллектуального анализа данных целевой рассылки, на котором основан [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]базы данных и связанные с ней модели. Дополнительные сведения см. в разделе [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>Пример 1. Детализация вариантов модели и столбцов структуры  
 В следующем примере возвращаются столбцы для всех вариантов, использованных для проверки модели «Целевая рассылка». Если структура интеллектуального анализа данных, на основе которой построена модель, не имеет контрольного проверочного набора данных, данный запрос не возвращает вариантов. Кроме того, можно использовать список выражений, чтобы возвращать только необходимые столбцы.  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>Пример 2. Детализация обучающих вариантов в конкретном узле  
 В следующем примере возвращаются только столбцы, использованные для обучения кластера 2. Узел кластера 2 имеет значение «002» в столбце NODE_UNIQUE_NAME. Кроме того, в этом примере возвращается один столбец структуры [Customer Key], который не входил в модель интеллектуального анализа данных. Этому столбцу присваивается псевдоним `CustomerID`. Обратите внимание, что имя столбца структуры передается как строковое значение, поэтому его следует заключать в кавычки, а не в скобки.  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 Чтобы вернуть столбец структуры, необходимы разрешения на детализацию как для модели, так и для структуры интеллектуального анализа данных.  
  
> [!NOTE]  
>  Детализация поддерживается не всеми типами моделей интеллектуального анализа данных. Сведения о модели, которые поддерживают детализацию, см. в разделе [запросов детализации &#40;интеллектуального анализа данных&#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>См. также  
 [ВЫБЕРИТЕ &AMP;#40;РАСШИРЕНИЙ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ&AMP;#41;](../dmx/select-dmx.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции определения данных](../dmx/dmx-statements-data-definition.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции управления данными](../dmx/dmx-statements-data-manipulation.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Справка по инструкции](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
