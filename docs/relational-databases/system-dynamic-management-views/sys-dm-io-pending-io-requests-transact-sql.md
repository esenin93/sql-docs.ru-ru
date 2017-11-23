---
title: "sys.dm_io_pending_io_requests (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b6261d261d95a15abd18d66ed06031c74c3553a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmiopendingiorequests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Возвращает по строке для каждого ожидающего выполнения запроса ввода-вывода в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Вызов его из [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] или [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], используйте имя **sys.dm_pdw_nodes_io_pending_io_requests**.  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|Адрес запроса ввода-вывода в памяти. Не допускает значение NULL.|  
|**io_type**|**varchar(7)**|Тип запроса ввода-вывода, ожидающего выполнения. Не допускает значение NULL.|  
|**io_pending**|**int**|Указывает, ожидает ли запрос ввода-вывода выполнения или он завершен Windows. Запрос может продолжать ожидать выполнения, даже если операционная система Windows уже завершила соответствующий ввод-вывод, но [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] еще не выполнил переключение контекста, при котором запрос ввода-вывода должен быть обработан и удален из этого списка. Не допускает значение NULL.|  
|**io_completion_routine_address**|**varbinary(8)**|Внутренняя функция, которая должна вызываться по завершении запроса ввода-вывода. Допускает значение NULL.|  
|**io_user_data_address**|**varbinary(8)**|Только для внутреннего применения. Допускает значение NULL.|  
|**scheduler_address**|**varbinary(8)**|Планировщик, которым был назначен данный запрос ввода-вывода. Запрос ввода-вывода появляется в списке планировщика запросов ввода-вывода, ожидающих выполнения. Дополнительные сведения см. в разделе [sys.dm_os_schedulers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). Не допускает значение NULL.|  
|**io_handle**|**varbinary(8)**|Дескриптор файла, используемый в запросе ввода-вывода. Допускает значение NULL.|  
|**io_offset**|**bigint**|Смещение при выполнении запроса ввода-вывода. Не допускает значение NULL.|  
|**io_pending_ms_ticks**|**int**|Только для внутреннего применения. Не допускает значение NULL.|  
|**pdw_node_id**|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор для узла, это распределение.|  
  
## <a name="permissions"></a>Permissions  
На [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], требуется `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровней Premium необходимо `VIEW DATABASE STATE` разрешений в базе данных. На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровней Standard и Basic, требует **администратор сервера** или **администратора Azure Active Directory** учетной записи.  
 

  
## <a name="see-also"></a>См. также:  
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Я O связанные динамические административные представления и функции &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

