---
title: Метод getDouble (java.lang.String) | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8eab6a8e-91f3-47b1-8707-5e57368ad0c6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 483a735699670160bee6faab3f762c4b3b052c30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="getdouble-method-javalangstring"></a>Метод getDouble (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Получает значение указанного параметра в виде **двойные** на Java по заданному имени параметра языка программирования.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public double getDouble(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Параметры  
 *sCol*  
  
 Объект **строка** , содержащее имя параметра.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Объект **двойные** значение.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Замечания  
 Этот метод getDouble указывается с помощью getDouble метода в интерфейсе java.sql.CallableStatement.  
  
 Этот метод возвращает все типы числовых данных с помощью Java **двойные** точность.  
  
## <a name="see-also"></a>См. также  
 [Метод getDouble &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [Члены SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Класс SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
