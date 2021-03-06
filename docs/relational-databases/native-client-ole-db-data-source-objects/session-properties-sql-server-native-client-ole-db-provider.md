---
title: Свойства сеанса — поставщик SQL Server OLE DB для собственного клиента | Документы Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 98a39aeb057be8d955b65efe36d7ee0b392961f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>Свойства сеанса — поставщик собственного клиента OLE DB SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Поставщика OLE DB для собственного клиента интерпретирует свойства сеанса OLE DB следующим образом.  
  
|Идентификатор свойства|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Поставщика OLE DB для собственного клиента поддерживает все уровни изоляции транзакций автоматической фиксации за исключением уровня хаоса, DBPROPVAL_TI_CHAOS.|  
  
 В специфический для поставщика наборе свойств DBPROPSET_SQLSERVERSESSION [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поставщик OLE DB для собственного клиента определяет следующее дополнительное свойство.  
  
|Идентификатор свойства|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Тип: VT_BOOL<br /><br /> R Чтение и запись: чтение и запись<br /><br /> По умолчанию: значение VARIANT_FALSE<br /><br /> Описание: Заключенные в кавычки идентификаторы допускаются в ограничение КАТАЛОГА.<br /><br /> VARIANT_TRUE: Заключенные в кавычки идентификаторы распознаются ограничением каталога для наборов строк схемы, предоставляющих поддержку распределенным запросам.<br /><br /> VARIANT_FALSE: Заключенные в кавычки идентификаторы не распознаются ограничением каталога для наборов строк схемы, предоставляющих поддержку распределенным запросам.<br /><br /> Дополнительные сведения о наборах строк схемы, предоставляющих поддержку распределенным запросам см. в разделе [поддержка распределенных запросов в наборах строк схемы](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|Свойство SSPROP_ALLOWNATIVEVARIANT|Тип: VT_BOOL<br /><br /> R Чтение и запись: чтение и запись<br /><br /> По умолчанию: значение VARIANT_FALSE<br /><br /> Описание: Определяет, является ли данные, полученные в качестве DBTYPE_VARIANT или DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: Dbtype_sqlvariant в котором случае в буфере сохраняется структура SSVARIANT возвращается тип столбца.<br /><br /> VARIANT_FALSE: Тип столбца возвращается DBTYPE_VARIANT и буфер будет иметь структура VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Для использования асинхронного режима задайте значение VARIANT_TRUE характерного для поставщика свойства SSPROP_ASYNCH_BULKCOPY сеанса до вызова метода BCPExec. Это свойство доступно в наборе свойств DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>См. также:  
 [Объекты источника данных & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
