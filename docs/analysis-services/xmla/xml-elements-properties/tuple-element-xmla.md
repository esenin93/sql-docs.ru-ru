---
title: Элемент Tuple (XML для Аналитики) | Документы Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f7f7d21f64c502e60ee0f6c95d2b6cbfd09c1b7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="tuple-element-xmla"></a>Элемент Tuple (XML для аналитики)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Содержит коллекцию элементов [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md), содержащихся в родительском элементе [Tuples](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|None|  
|Значение по умолчанию|None|  
|Количество элементов|от 0 до n: необязательный элемент, который может встречаться несколько раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[Кортежи](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
|Дочерние элементы|[Член](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="remarks"></a>Примечания  
 Когда клиентское приложение устанавливает для свойства **AxisFormat** значение *TupleFormat*, ось представляется в виде набора кортежей. Каждый элемент **Axis** содержит элемент **Tuples**, представляющий набор кортежей на этой оси. Каждый кортеж представлен с помощью элемента **Tuple**, содержащего элементы **Member** из каждой иерархии оси.  
  
## <a name="example"></a>Пример  
 В следующем примере демонстрируется структура элемента **Tuple**, если клиент указывает значение *TupleFormat* или *CustomFormat* для XMLA-свойства **AxisFormat**, а на оси имеются следующие элементы:  
  
|||||  
|-|-|-|-|  
|Иерархия **Time**|1999|1999|2000|  
|Иерархия **Category**|Actual|Budget|Budget|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>См. также:  
 [Свойства & #40; XML для Аналитики & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
