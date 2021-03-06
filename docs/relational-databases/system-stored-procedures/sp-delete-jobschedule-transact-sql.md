---
title: sp_delete_jobschedule (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_jobschedule
- sp_delete_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobschedule
ms.assetid: 82fbb48b-603a-4016-a7fb-1ce17fb76919
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7909cb6689db9610cd9a9a24482f7ce21d98f060
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="spdeletejobschedule-transact-sql"></a>sp_delete_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Удаляет расписание для задания.  
  
 **sp_delete_jobschedule** предоставляется только для обратной совместимости.  
  
  
## <a name="remarks"></a>Замечания  
 Расписанием задач теперь можно управлять независимо от них самих. Чтобы удалить расписание из задания, используйте **процедуру sp_detach_schedule**. Чтобы удалить расписание, используйте **sp_delete_schedule**.  
  
> **Примечание:****sp_delete_jobschedule** не поддерживает расписания, которые присоединены к нескольким заданиям. Если существующий скрипт вызывает **sp_delete_jobschedule** для удаления расписания, присоединенного к более чем одному заданию, процедура возвращает ошибку.  
  
## <a name="permissions"></a>Разрешения  
 По умолчанию эту хранимую процедуру могут выполнять только члены предопределенной роли сервера **sysadmin** . Другим пользователям должна быть предоставлена одна из следующих предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в базе данных **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Дополнительные сведения о разрешениях этих ролей см. в разделе [Предопределенные роли базы данных агента SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Члены **sysadmin** роли можно удалять любые расписания заданий. Пользователи, не являющиеся членами из **sysadmin** роли можно удалять только те расписания заданий, которыми они владеют.  
  
## <a name="see-also"></a>См. также  
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [процедуру sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [Просмотр или изменение заданий](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_help_jobschedule & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)   
 [sp_update_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
