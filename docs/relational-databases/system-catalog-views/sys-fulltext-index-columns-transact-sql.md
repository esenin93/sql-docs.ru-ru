---
title: sys.fulltext_index_columns (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb9a5d874765c10343106ed8d401193918d5ee6c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="sysfulltextindexcolumns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Содержит по одной строке для каждого столбца, являющегося частью полнотекстового индекса.    
 
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Идентификатор объекта, частью которого является этот столбец.|  
|**column_id**|**int**|Идентификатор столбца, который является частью полнотекстового индекса.|  
|**type_column_id**|**int**|Идентификатор столбца типа, в котором содержится заданное пользователем расширение файла («.doc», «.xls» и т.д.) для документа в данной строке. Столбец типа указан только для тех столбцов, данные которых требуют фильтрации во время полнотекстового индексирования. Значение NULL, если не применимо. Дополнительные сведения см. в разделе [Настройка фильтров для поиска и управление ими](../../relational-databases/search/configure-and-manage-filters-for-search.md).|  
|**language_id**|**int**|Код языка, у которого средство разбиения по словам используется для индексации этого полнотекстового столбца.<br /><br /> 0 = нейтральный<br /><br /> Дополнительные сведения см. в разделе [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).|  
|**statistical_semantics**|**int**|1 = для этого столбца, помимо полнотекстового индексирования, включена статистическая семантика.|  
  
## <a name="permissions"></a>Разрешения  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Представления каталога объектов (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
