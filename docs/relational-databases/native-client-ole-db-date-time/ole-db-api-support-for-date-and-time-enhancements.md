---
title: Поддержка API-Интерфейс OLE DB для даты и времени улучшения | Документы Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c7f6474a2c64d8387cdaee54a654e5b899e5ee26
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Поддержка API-Интерфейс OLE DB для даты и времени усовершенствования
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Следующие API-интерфейсы OLE DB поддерживают улучшенные возможности по работе с данными в формате даты-времени.  
  
|Функция|Описание|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Чтобы позволить приложениям различать структуры DBBINDING добавляется флаг **datetime**, **datetime2**, и **smalldatetime** значения. Дополнительные сведения см. в разделе [строк метаданные параметров и](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Дополнительные сведения см. в разделе [изменения массового копирования для улучшенной даты и времени &#40;OLE DB и ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Дополнительные сведения см. в разделе[строк метаданные параметров и](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Дополнительные сведения см. в разделе[строк метаданные параметров и](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Дополнительные сведения см. в разделе[строк метаданные параметров и](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Дополнительные сведения см. в разделе[строк метаданные параметров и](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Сведения о затронутых наборах строк схемы см. в разделе[даты и времени и наборы строк схемы](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Данный интерфейс поддерживает новые типы даты-времени, но он остается неизменным.|  
|ITableDefinition::CreateTable|Дополнительные сведения см. в разделе [поддержка типов данных даты OLE DB и улучшения времени](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>См. также  
 [Дата и время усовершенствования & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
