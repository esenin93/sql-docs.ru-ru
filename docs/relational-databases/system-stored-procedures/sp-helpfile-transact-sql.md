---
title: sp_helpfile (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4de2e386d30c718177482cd50d38f169922f5d8a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает физические имена и атрибуты файлов, связанных с текущей базой данных. Используйте эту хранимую процедуру для определения имен файлов, чтобы присоединять или отсоединять их от сервера.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@filename =** ] **"***имя***"**  
 Логическое имя любого файла в текущей базе данных. *имя* — **sysname**, значение по умолчанию NULL. Если *имя* — не указано, будут возвращены атрибуты всех файлов в текущей базе данных.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Логическое имя файла.|  
|**fileid**|**smallint**|Числовой идентификатор файла. Не возвращается, если *имя* указан *.*|  
|**Имя файла**|**nchar(260)**|Физическое имя файла.|  
|**filegroup**|**sysname**|Файловая группа, к которой принадлежит файл.<br /><br /> NULL = файл является файлом журнала. Такой файл никогда не является частью файловой группы.|  
|**size**|**nvarchar(15)**|Размер файла в килобайтах.|  
|**параметр MaxSize**|**nvarchar(15)**|Определяет максимальный размер, до которого может вырасти файл. Значение UNLIMITED в этом поле означает, что файл может расти, пока диск не будет заполнен.|  
|**Увеличение размера**|**nvarchar(15)**|Значение прироста размера файла. Оно указывает объем пространства, добавляемого к файлу каждый раз, когда требуется новое пространство.<br /><br /> 0 = файл имеет фиксированный размер и не может расти.|  
|**Использование**|**varchar(9)**|Для файла данных это значение равно **«данные»** и файла журнала, оно **только для журнала**.|  
  
## <a name="permissions"></a>Разрешения  
 Необходимо быть членом роли **public**.  
  
## <a name="examples"></a>Примеры  
 Следующий пример возвращает данные о файлах в базе данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Компонент Database Engine хранимой процедуры &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Файлы и файловые группы базы данных](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
