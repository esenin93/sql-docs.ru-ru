---
title: sys.remote_data_archive_databases (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 599621bb64cb11ee70646204689a4b1d0bf43574
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="stretch-database-catalog-views---sysremotedataarchivedatabases"></a>Растянуть представления каталога базы данных - sys.remote_data_archive_databases
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Содержит по одной строке для каждой удаленной базы данных, которая хранит данные из локальной базы данных с включенным Stretch.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|Автоматически созданный локальный идентификатор удаленной базы данных.|  
|**remote_database_name**|**sysname**|Имя удаленной базы данных.|  
|**data_source_id**|**int**|Источник данных, используемый для подключения к удаленному серверу|  
  
## <a name="see-also"></a>См. также  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
