---
title: Метод isWrapperFor (SQLServerXADataSource) | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d53da9b90b1b3b74cce924304c33fab50e82e315
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>Метод isWrapperFor (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Указывает, является ли этот объект оболочкой указанного интерфейса.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Параметры  
 *iface*  
  
 Объект **класса** определение интерфейса.  
  
## <a name="return-value"></a>Возвращаемое значение  
 **значение true,** , если этот объект реализует интерфейс или упаковывает объект, реализующий интерфейс. В противном случае — **false**.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Замечания  
 [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) метод и [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) метод определяются интерфейсом java.sql.Wrapper, который появился в спецификации JDBC 4.0.  
  
 Если этот метод возвращает значение true, вызов метода [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) с тем же аргументом будет выполнена успешно.  
  
 Дополнительные сведения см. в разделе [оболочки и интерфейсы](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>См. также  
 [Метод unwrap &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [Методы SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Элементы SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Класс SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
