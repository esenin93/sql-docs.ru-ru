---
title: YEAR (выражение служб SSIS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a0027c1f9d91e653878f5918e359f8f6bf13034
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="year-ssis-expression"></a>YEAR (выражение служб SSIS)
  Возвращает целое число, представляющее год указанной даты.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>Аргументы  
 *date*  
 Является датой в любом формате дат.  
  
## <a name="result-types"></a>Типы результата  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 Функция YEAR возвращает значение NULL, если аргумент — NULL.  
  
 Литерал даты должен быть явно приведен к одному из типов данных даты. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  Проверка выражения завершается ошибкой при явном приведении литерала даты к одному из следующих типов данных: DT_DBTIMESTAMPOFFSET и DT_DBTIMESTAMP2.  
  
 Функция YEAR является более компактным, но эквивалентным вариантом функции DATEPART("Year", date).  
  
## <a name="expression-examples"></a>Примеры выражений  
 Этот пример возвращает год из литерала даты. Если дата представлена в формате «мм/дд/гггг», то результатом данного примера будет «2002».  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Этот пример возвращает целое число, которое представляет собой год столбца **ModifiedDate** .  
  
```  
YEAR(ModifiedDate)  
```  
  
 Этот пример возвращает целое число, представляющее год в текущей дате.  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>См. также:  
 [DATEADD (выражение служб SSIS)](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF (выражение служб SSIS)](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART (выражение служб SSIS)](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY (выражение служб SSIS)](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH (выражение служб SSIS)](../../integration-services/expressions/month-ssis-expression.md)   
 [Функции (выражение служб SSIS)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
