---
title: logmarkhistory (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c3498368a2c38f5e1c64d38c26920a7a9a9b5e1f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит одну строку для каждой зафиксированной помеченной транзакции. Эта таблица хранится в **msdb** базы данных.  
  

|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Локальная база данных, в которой возникла помеченная транзакция.|  
|**mark_name**|**nvarchar(128)**|Предоставляемое пользователем имя помеченной транзакции.|  
|**Описание**|**nvarchar(255)**|Предоставляемое пользователем описание помеченной транзакции. Может иметь значение NULL.|  
|**user_name**|**nvarchar(128)**|Имя пользователя базы данных, выполнившего помеченную транзакцию. Может иметь значение NULL.|  
|**lsn**|**numeric(25,0)**|Номер LSN записи транзакции с пометкой.|  
|**mark_time**|**datetime**|Время фиксации помеченной транзакции (локальное время).|  
  
## <a name="see-also"></a>См. также  
 [Восстановление базы данных до помеченной транзакции (среда SQL Server Management Studio)](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Использование помеченных транзакций для согласованного восстановления связанных баз данных (модель полного восстановления)](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Системные таблицы (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
