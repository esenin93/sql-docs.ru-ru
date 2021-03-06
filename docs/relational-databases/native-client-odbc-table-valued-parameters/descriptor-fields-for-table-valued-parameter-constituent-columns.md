---
title: Поля дескриптора для столбцов, составляющих табличное значение параметра | Документы Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b86145c43b072361b20d1e7e8869091689fb831
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Поля дескриптора для столбцов, содержащих параметры, возвращающие табличные значения
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Поля дескриптора табличное значение параметра, описанные в этом разделе оперирует [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) и [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) с дескриптором (дескриптора параметра реализации IPD).  
  
## <a name="remarks"></a>Замечания  
 SQL_DESC_AUTO_UNIQUE_VALUE используется для параметров, возвращающих табличные значения, и других компонентов.  
  
|Имя атрибута|Тип|Описание|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE указывает, что этот столбец является столбцом идентификаторов.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Эти сведения можно использовать для оптимизации производительности, но приложения не требуется устанавливать это свойство для столбцов идентификаторов.|  
  
 Следующие атрибуты добавляются к параметрам всех типов в дескрипторе параметра приложения (APD) и дескрипторе параметра реализации (IPD).  
  
|Имя атрибута|Тип|Описание|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE указывает, что этот столбец является вычисляемым.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Эти сведения можно использовать для оптимизации производительности, но приложение не обязано устанавливать его для вычисляемых столбцов.<br /><br /> Этот атрибут пропускается в случае привязок, не являющихся столбцами параметров, возвращающих табличные значения.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE указывает, что столбец возвращающих табличное значение параметров является частью уникального ключа. Это может повысить производительность запросов. Этот атрибут пропускается в случае привязок, не являющихся столбцами параметров, возвращающих табличные значения.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Указывает порядок сортировки столбца возвращающих табличное значение параметров. Это может повысить производительность запросов. Этот атрибут пропускается в случае привязок, не являющихся столбцами параметров, возвращающих табличные значения. Возможные значения. <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> Значения, отличные от **SQL_SS_ASCENDING_ORDER** и **SQL_SS_DESCENDING_ORDER** выдана ошибка с **SQLSTATE HY024** и сообщение «Недопустимое значение атрибута», рассматриваются как **значения SQL_SS_ORDER_UNSPECIFIED**, который является значением по умолчанию для этого атрибута.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Указывает порядковый номер столбца параметра, возвращающего табличное значение, в наборе столбцов, которые определяют сквозной порядковый номер для параметра, возвращающего табличное значение. Это может повысить производительность запросов. Этот атрибут пропускается в случае привязок, не являющихся столбцами параметров, возвращающих табличные значения. Порядковые номера сортировки начинаются с 1. Значение 0 (устанавливаемое по умолчанию) указывает, что столбец параметра, возвращающего табличное значение, не упорядочен.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Указывает, будут ли все строки параметра, возвращающего табличное значение, иметь значение по умолчанию для этого столбца. Для параметров, возвращающих табличное значение, значение по умолчанию не может выбираться построчно. Значение SQL_FALSE указывает на то, что строки будут иметь значения отличные от значений по умолчанию. Это значение по умолчанию. Значение SQL_TRUE указывает, что этот столбец будет иметь значения по умолчанию для всех строк.<br /><br /> Если установлено значение SQL_TRUE, то данные не будут отправляться на сервер.<br /><br /> Это поле также используется со столбцами идентификаторов или вычисляемых столбцов, если их обработка на сервере не требуется.|  
  
 Эти атрибуты доступны только для столбцов возвращающих табличные значения параметров. Для других параметров они не учитываются.  
  
 Если для столбца, возвращающего табличное значение параметра, установлен атрибут SQL_CA_SS_COL_HAS_DEFAULT_VALUE, то SQL_DESC_DATA_PTR для этого столбца должен быть равен null. В противном случае SQLExecute или SQLExecDirect вернет значение SQL_ERROR. Будет создана диагностическая запись с кодом SQLSTATE = 07S01 и сообщением «недопустимое использование параметра по умолчанию для параметра \<p >, столбец \<c >», где \<p > имеет порядковый номер параметра и \<c > — Порядковый номер столбца.  
  
## <a name="see-also"></a>См. также  
 [Возвращающие табличные значения параметров &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
