---
title: Добавление столбца к таблице SQL Server | Документы Microsoft
description: Добавление столбца в таблицу SQL Server с помощью драйвера OLE DB для SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2f49f014e29401d0f99bd5f9bd59551c94255399
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Добавление столбца к таблице SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Драйвер OLE DB для SQL Server предоставляет **ITableDefinition::AddColumn** функции. Это позволяет пользователю добавить столбец в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] таблицы.  
  
 При добавлении столбца к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] таблица, драйвер OLE DB для SQL Server потребителя ограничен следующим образом:  
  
-   Если значение DBPROP_COL_AUTOINCREMENT равно VARIANT_TRUE, то значение DBPROP_COL_NULLABLE должно быть равно VARIANT_FALSE.  
  
-   Если столбец определен с помощью [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **timestamp** тип данных, DBPROP_COL_NULLABLE должно быть равно VARIANT_FALSE.  
  
-   Для столбца любого другого типа DBPROP_COL_NULLABLE должно быть равно VARIANT_TRUE.  
  
 Пользователь задает имя таблицы в виде символьной строки в Юникоде в *pwszName* членом *uName* объединения в *pTableID* параметра. *EKind* членом *pTableID* должен быть равен DBKIND_NAME.  
  
 Новое имя столбца указано как строку символов Юникода в *pwszName* членом *uName* объединения в *dbcid* член параметра DBCOLUMNDESC *pColumnDesc*. *EKind* член должен быть равен DBKIND_NAME.  
  
## <a name="see-also"></a>См. также  
 [Таблицы и индексы](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
