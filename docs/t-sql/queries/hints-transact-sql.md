---
title: Указания (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a404f015c177fe38985c07470645e9a16e2cb716
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="hints-transact-sql"></a>Указания (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Подсказки являются параметрами или стратегиями, указанными для обеспечения выполнения инструкций SELECT, INSERT, UPDATE или DELETE обработчиком запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Указания имеют преимущество над любым планом выполнения, который может быть выбран оптимизатором запросов для запроса.  
  
> [!CAUTION]  
>  Так как оптимизатор запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обычно выбирает наилучший план выполнения для запроса, рекомендуется использовать указания \<join_hint>, \<query_hint> и \<table_hint> в последнюю очередь и только опытным разработчикам и администраторам баз данных.
  
 В этом разделе описаны следующие указания:  
  
-   [Указания в соединении](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Указания запросов](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Табличное указание](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
