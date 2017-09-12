---
title: "UnionAggregate (тип данных geometry) | Документы Microsoft"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- UnionAggregate method (geometry)
ms.assetid: dc7929cc-55ca-4a2c-a4b9-f5452f95bde8
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 65759e7e4d7701b36d79b8ce27bb5bfe176ba3e3
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="unionaggregate-geometry-data-type"></a>UnionAggregate (тип данных geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Выполняет операцию объединения на наборе объектов типа geometry.
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
UnionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Аргументы  
 *geometry_operand*  
 — **Geometry** столбец таблицы типа, который содержит набор из **geometry** объектов для выполнения операции union.  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Тип возвращаемого значения: **геометрии**  
  
## <a name="exceptions"></a>Исключения  
 Вызывает исключение `FormatException` при наличии недопустимых входных значений. В разделе [STIsValid &#40; тип данных geometry &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Замечания  
 Метод возвращает **null** при входных данных пуст или содержит различными идентификаторами SRID. В разделе [идентификаторы пространственных ссылок &#40; SRID &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Метод игнорирует **null** входных данных.  
  
> [!NOTE]  
>  Метод возвращает **null** при входе присутствуют только значения **null**.  
  
## <a name="examples"></a>Примеры  
 Следующий пример возвращает объединение набор **geometry** объекты в табличной переменной.  
  
 `-- Setup table variable for UnionAggregate example`  
  
 `DECLARE @Geom TABLE`  
  
 `(`  
  
 `shape geometry,`  
  
 `shapeType nvarchar(50)`  
  
 `);`  
  
 `INSERT INTO @Geom(shape,shapeType)`  
  
 `VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),`  
  
 `('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');`  
  
 `-- Perform UnionAggregate on @Geom.shape column`  
  
 `SELECT geometry::UnionAggregate(shape).ToString()`  
  
 `FROM @Geom;`  
  
## <a name="see-also"></a>См. также:  
 [Расширенные статические геометрические методы](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

