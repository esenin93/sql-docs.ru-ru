---
title: sys.dm_exec_xml_handles (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 66702418faae18f1c4582a28353e2f5ae7c156bc
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexecxmlhandles-transact-sql"></a>sys.dm_exec_xml_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Возвращает сведения об активных дескрипторах, открытых с **sp_xml_preparedocument**.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>Аргументы  
 *session_id* | 0,  
 Идентификатор сеанса. Если *session_id* указано, эта функция возвращает сведения о дескрипторах XML в указанном сеансе.  
  
 Если указано значение 0, функция возвращает сведения обо всех дескрипторах XML во всех сеансах.  
  
## <a name="table-returned"></a>Возвращаемая таблица  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Идентификатор сеанса, содержащего данный XML-документ.|  
|**document_id**|**int**|Возвращенный идентификатор дескриптора XML документа **sp_xml_preparedocument**.|  
|**namespace_document_id**|**int**|Идентификатор внутренний дескриптор, используемый для документа связанного пространства имен, которая была передана в качестве третьего параметра для **sp_xml_preparedocument**. NULL, если документ пространства имен отсутствует.|  
|**sql_handle**|**varbinary(64)**|Дескриптор текста кода SQL, в котором был определен дескриптор.|  
|**statement_start_offset**|**int**|Число символов в настоящий момент пакете или хранимой процедуре, с которой **sp_xml_preparedocument** вызов происходит. Можно использовать вместе с **sql_handle**, **statement_end_offset**и **sys.dm_exec_sql_text** функции динамического управления для получения в настоящее время выполнение инструкции для запроса.|  
|**statement_end_offset**|**int**|Число символов в настоящий момент пакете или хранимой процедуре, с которой **sp_xml_preparedocument** вызов происходит. Можно использовать вместе с **sql_handle**, **statement_start_offset**и **sys.dm_exec_sql_text** функции динамического управления для получения в настоящее время выполнение инструкции для запроса.|  
|**creation_time**|**datetime**|Отметка времени при **sp_xml_preparedocument** был вызван.|  
|**original_document_size_bytes**|**bigint**|Размер непроанализированного XML-документа в байтах.|  
|**original_namespace_document_size_bytes**|**bigint**|Размер непроанализированного документа пространства имен XML в байтах. NULL, если документ пространства имен отсутствует.|  
|**num_openxml_calls**|**bigint**|Число вызовов инструкции OPENXML с данным дескриптором документа.|  
|**row_count**|**bigint**|Число строк, возвращенных всеми предыдущими вызовами инструкции OPENXML для данного дескриптора документа.|  
|**dormant_duration_ms**|**bigint**|Число миллисекунд, прошедших с момента последнего вызова инструкции OPENXML. Если не был вызван OPENXML, возвращает в миллисекундах с момента **sp_xml_preparedocumen**t вызова.|  
  
## <a name="remarks"></a>Примечания  
 Время существования **sql_handles** используется для получения текста SQL, выполнившего запрос к **sp_xml_preparedocument** кэшированного плана, используемого для выполнения запроса превышает время существования. Если текст запроса в кэше недоступен, извлечь данные с помощью сведений, возвращаемых этой функцией, невозможно. Это может произойти при выполнении множества больших пакетов.  
  
## <a name="permissions"></a>Разрешения  
 Требуется разрешение VIEW SERVER STATE на сервер, чтобы просмотреть все сеансы или идентификаторы сеансов, которыми не владеет участник. Участник всегда может просмотреть данные для своего текущего идентификатора сеанса.      
  
## <a name="examples"></a>Примеры  
 В следующем примере выбираются все активные дескрипторы.  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>См. также  
 <br>[Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
 <br>[Динамические административные представления и функции (Transact-SQL), связанные с выполнением](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
 <br>[sp_xml_preparedocument (Transact-SQL)](../system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[sp_xml_removedocument (Transact-SQL)](../system-stored-procedures/sp-xml-removedocument-transact-sql.md)


 
  
  
