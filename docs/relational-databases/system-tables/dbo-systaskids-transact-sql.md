---
title: "dbo.systaskids (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs: TSQL
helpviewer_keywords: systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 91e06a49b7b61d8969ae4db2feb9e5629d0b1b30
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит сопоставление задач, созданных в более ранних версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], с заданиями среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] текущей версии. Эта таблица хранится в **msdb** базы данных.  
  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**TASK_ID**|**int**|Идентификатор задачи.|  
|**Аргумент job_id**|**uniqueidentifier**|Идентификатор задания, с которым сопоставляется задача.|  
  
  