---
title: sys.fn_db_backup_file_snapshots (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085bf32115bfe84b00471de27e1fd9c11b3a1ab9
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/01/2018
ms.locfileid: "33231353"
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Возвращает моментальные снимки Azure, связанных с файлами базы данных. Если указанная база данных не найден или если файлы базы данных не хранятся в службе хранилища больших двоичных объектов Microsoft Azure, строки не возвращаются. Использовать в сочетании с системной функцией **sys.sp_delete_backup_file_snapshot** системной хранимой процедуры для идентификации и удаление потерянных резервных копий моментальных снимков. Дополнительные сведения см. в разделе [Резервные копии моментальных снимков файлов для файлов базы данных в Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Аргументы  
 *Database_name*  
 Имя запрашиваемой базы данных. Если значение равно NULL, эта функция выполняется в текущей области базы данных.  
  
## <a name="table-returned"></a>Возвращаемая таблица  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|file_id|**int**|Идентификатор файла для базы данных. Не допускает значение NULL.|  
|snapshot_time|**nvarchar(260)**|Отметка времени моментального снимка, возвращаемый API-интерфейса REST. Возвращает значение NULL, если моментальный снимок не существует.|  
|snapshot_url|**nvarchar(360)**|Полный URL-адрес файла моментального снимка. Возвращает значение NULL, если моментальный снимок не существует.|  
  
## <a name="permissions"></a>Разрешения  
 Необходимо разрешение VIEW DATABASE STATE на базу данных.  
  
## <a name="see-also"></a>См. также  
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
