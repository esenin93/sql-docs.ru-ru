---
title: "GeomFromGML (тип данных geography) | Документы Microsoft"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geography Data Type)
- GeomFromGML method
ms.assetid: 470d0997-3cb0-4d34-9a45-b332fe432b14
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec0d21afb92b000f29fb91c4e3b848b4881b99c7
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="geomfromgml-geography-data-type"></a>GeomFromGML (тип данных geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Создает **geography** экземпляр заданному представлению на используемом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] подмножество языка разметки Geography (GML).
  
Дополнительные сведения о языке GML см. в разделе следующей спецификации консорциума Ogc: [спецификации OGC, географический язык разметки](http://go.microsoft.com/fwlink/?LinkId=93629)
  
Это **geography** поддерживает метод тип **FullGlobe** экземпляры или Пространственные экземпляры, размер которых превышает полусферу.
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>Аргументы  
 *GML_input*  
 Входные XML-данные, из которых GML-код получит возвращаемое значение.  
  
 *SRID*  
 — **Int** выражение, представляющее пространственной идентификатор ссылки (SRID) из **geography** возвращаемого экземпляра.  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Тип возвращаемого значения: **geography**  
  
 Возвращаемый тип CLR: **SqlGeography**  
  
## <a name="remarks"></a>Замечания  
 Этот метод создает исключение **FormatException** Если входные данные имеют неверный формат.  
  
 Этот метод вызывает исключение **ArgumentException** Если вход содержит противоположную границу.  
  
## <a name="examples"></a>Примеры  
 В следующем примере метод `GeomFromGml()` применяется для создания экземпляра `geography`.  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
 В следующем примере метод `GeomFromGml()` применяется для создания экземпляра `FullGlobe``geography`.  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<FullGlobe xmlns="http://schemas.microsoft.com/sqlserver/2011/geography" />';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>См. также:  
 [Расширенные статические географические методы](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
