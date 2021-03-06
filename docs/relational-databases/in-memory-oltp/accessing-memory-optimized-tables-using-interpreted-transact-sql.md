---
title: Доступ к таблицам, оптимизированным для памяти, с помощью интерпретируемых инструкций Transact-SQL | Документация Майкрософт
ms.custom: ''
ms.date: 05/31/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 554b1c2240d06fc0c9180594bc00ecc6473c9bd5
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2018
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Доступ к таблицам, оптимизированным для памяти, с помощью интерпретируемых инструкций Transact-SQL
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

 Лишь за некоторыми исключениями, можно получить доступ к оптимизированным для памяти таблицам с помощью любого запроса [!INCLUDE[tsql](../../includes/tsql-md.md)] или операции DML (SELECT, INSERT, UPDATE или DELETE), нерегламентированных пакетов и модулей SQL, таких как хранимые процедуры, триггеры, функции, возвращающие табличное значение, и представления.  
  
Интерпретируемый [!INCLUDE[tsql](../../includes/tsql-md.md)] — это пакеты или хранимые процедуры [!INCLUDE[tsql](../../includes/tsql-md.md)] , отличные от скомпилированных в собственном коде хранимых процедур. Доступ интерпретированного [!INCLUDE[tsql](../../includes/tsql-md.md)] к оптимизированным для памяти таблицам называется доступом взаимодействия.  

Начиная с версии [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], запросы в интерпретируемом [!INCLUDE[tsql](../../includes/tsql-md.md)] могут сканировать оптимизированные для памяти таблицы не только в последовательном, но и в параллельном режиме.

Доступ к оптимизированным для памяти таблицам можно также осуществлять с помощью скомпилированной в собственном коде хранимой процедуры. Скомпилированные в собственном коде хранимые процедуры рекомендуется использовать для важных с точки зрения производительности операций OLTP.  
  
Интерпретируемый доступ [!INCLUDE[tsql](../../includes/tsql-md.md)] рекомендуется в следующих случаях.  
  
- Нерегламентированные запросы и административные задачи.  
  
- Запросы для отчетов, в которых обычно используются конструкции, недоступные в скомпилированных в собственном коде хранимых процедурах (например, *оконные* функции, также известные как функции [OVER](../../t-sql/queries/select-over-clause-transact-sql.md) ).  
  
- Для переноса критически важных для производительности частей приложения в оптимизированные для памяти таблицы с минимальными изменениями кода приложения или без изменений. Потенциально перенесенные таблицы могут обеспечить улучшение производительности. Дополнительного роста производительности можно добиться путем переноса хранимых процедур в скомпилированные в собственном коде хранимые процедуры.  
  
- Когда инструкция [!INCLUDE[tsql](../../includes/tsql-md.md)] недоступна для скомпилированных в собственном коде хранимых процедур.  
  
Однако следующие конструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] не поддерживаются в хранимых процедурах интерпретированного [!INCLUDE[tsql](../../includes/tsql-md.md)] , которые обращаются к данным из оптимизированных для памяти таблиц.  
  
|Область|Не поддерживается|  
|----------|-----------------|  
|Доступ к таблицам|TRUNCATE TABLE<br /><br /> MERGE (оптимизированная для памяти таблица в качестве назначения)<br /><br /> Динамический курсор и курсор ключевого набора (они автоматически понижаются в статический).<br /><br /> Доступ из модулей CLR с использованием контекстного соединения.<br /><br /> Ссылка на оптимизированную для памяти таблицу из индексированного представления|  
|Между базами данных|Межбазовые запросы<br /><br /> Межбазовые транзакции<br /><br /> Связанные серверы|  
  
## <a name="table-hints"></a>Табличные указания

Дополнительные сведения о табличных указаниях см. в разделе. [Табличные указания (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md). Функция SNAPSHOT добавлена для поддержки [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
При доступе к оптимизированной для памяти таблице с использованием интерпретируемого кода [!INCLUDE[tsql](../../includes/tsql-md.md)]не поддерживаются следующие табличные указания.  

  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *целое число*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  

При доступе к оптимизированной для памяти таблице из явной или неявной транзакции с помощью интерпретируемого [!INCLUDE[tsql](../../includes/tsql-md.md)]необходимо выполнить как минимум одно из следующих действий:  
  
- указать [табличное указание уровня изоляции](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) , например SNAPSHOT, REPEATABLEREAD или SERIALIZABLE;  
  
- задать для параметра базы данных [MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT](../../t-sql/statements/alter-database-transact-sql-set-options.md) значение ON (включено).  
  
Табличное указание уровня изоляции не требуется при обращении к оптимизированным для памяти таблицам с помощью запросов с [автоматической фиксацией](http://msdn.microsoft.com/en-us/c8de5b60-d147-492d-b601-2eeae8511d00).  
  
## <a name="see-also"></a>См. также:

[Поддержка Transact-SQL для In-Memory OLTP](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   

[Миграция в In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  

