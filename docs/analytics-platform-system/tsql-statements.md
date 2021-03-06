---
title: Инструкции T-SQL - Parallel Data Warehouse | Документы Microsoft
description: Инструкции T-SQL для аналитической Platform System (APS) SQL Server Parallel данных хранилища (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 86bf74778ab78fc42ad1151a341e5c2d232da7aa
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>Инструкции T-SQL для параллельного хранилища данных
Инструкции Transact-SQL (T-SQL) для аналитической Platform System (APS) SQL Server Parallel данных хранилища (PDW).

## <a name="data-definition-language-ddl-statements"></a>Данные инструкции языка определения (DDL)
* [ИЗМЕНЕНИЕ БАЗЫ ДАННЫХ](../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [ИЗМЕНЕНИЕ СХЕМЫ](../t-sql/statements/alter-schema-transact-sql.md)
* [ИНСТРУКЦИЯ ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [СОЗДАНИЕ ИНДЕКСА COLUMNSTORE](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [СОЗДАНИЕ БАЗЫ ДАННЫХ](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [СОЗДАНИЕ УРОВНЯ БАЗЫ ДАННЫХ УЧЕТНЫХ ДАННЫХ](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [СОЗДАЙТЕ ВНЕШНИЙ ИСТОЧНИК ДАННЫХ](../t-sql/statements/create-external-data-source-transact-sql.md)
* [СОЗДАЙТЕ ФОРМАТ ВНЕШНЕГО ФАЙЛА](../t-sql/statements/create-external-file-format-transact-sql.md)
* [СОЗДАЙТЕ ВНЕШНЮЮ ТАБЛИЦУ.](../t-sql/statements/create-external-table-transact-sql.md)
* [СОЗДАНИЕ ФУНКЦИИ](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [СОЗДАНИЕ СХЕМЫ](../t-sql/statements/create-schema-transact-sql.md)
* [CREATE STATISTICS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [СОЗДАНИЕ TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [УДАЛИТЬ ВНЕШНИЙ ИСТОЧНИК ДАННЫХ](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [УДАЛИТЕ ФОРМАТ ВНЕШНЕГО ФАЙЛА.](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [УДАЛЕНИЕ ВНЕШНЕЙ ТАБЛИЦЫ](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP PROCEDURE](../t-sql/statements/drop-procedure-transact-sql.md)
* [УДАЛЕНИЕ СТАТИСТИКИ](../t-sql/statements/drop-statistics-transact-sql.md)
* [DROP TABLE](../t-sql/statements/drop-table-transact-sql.md)
* [УДАЛЕНИЕ СХЕМ](../t-sql/statements/drop-schema-transact-sql.md)
* [УДАЛИТЬ ПРЕДСТАВЛЕНИЕ](../t-sql/statements/drop-view-transact-sql.md)
* [RENAME](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [UPDATE STATISTICS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>Инструкции языка Обработки данных
* [DELETE](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>Команды консоли базы данных
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](https://msdn.microsoft.com/library/mt204018.aspx)
* [DBCC SHRINKLOG](https://msdn.microsoft.com/library/mt204020.aspx)
* [DBCC PDW_SHOWEXECUTIONPLAN](https://msdn.microsoft.com/library/mt204017.aspx)
* [DBCC PDW_SHOWPARTITIONSTATS](https://msdn.microsoft.com/library/mt204013.aspx)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/mt204043.aspx)

## <a name="query-statements"></a>Операторы запроса
* [SELECT](../t-sql/queries/select-transact-sql.md)
* [WITH <обобщенное_табличное_выражение>](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT и INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [EXPLAIN](../t-sql/queries/explain-transact-sql.md)
* [FROM](../t-sql/queries/from-transact-sql.md)
* [Использование операторов PIVOT и UNPIVOT](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [OPTION](../t-sql/queries/option-clause-transact-sql.md)
* [UNION](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [WHERE](../t-sql/queries/where-transact-sql.md)
* [TOP](../t-sql/queries/top-transact-sql.md)
* [Совмещение имен](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [Условия поиска](../t-sql/queries/search-condition-transact-sql.md)
* [Вложенные запросы](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>Инструкции по безопасности
* Разрешения: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [ОТМЕНЫ](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [ALTER CERTIFICATE](../t-sql/statements/alter-certificate-transact-sql.md)
* [ИЗМЕНИТЬ КЛЮЧ ШИФРОВАНИЯ БАЗЫ ДАННЫХ](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [РАЗРЕШЕНИЕ ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [ALTER MASTER KEY](../t-sql/statements/alter-master-key-transact-sql.md)
* [ИЗМЕНЕНИЕ РОЛИ](../t-sql/statements/alter-role-transact-sql.md)
* [ALTER USER](../t-sql/statements/alter-user-transact-sql.md)
* [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
* [CLOSE MASTER KEY](../t-sql/statements/close-master-key-transact-sql.md)
* [СОЗДАНИЕ СЕРТИФИКАТА](../t-sql/statements/create-certificate-transact-sql.md)
* [СОЗДАНИЕ КЛЮЧА ШИФРОВАНИЯ БАЗЫ ДАННЫХ](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [СОЗДАНИЕ ИМЕНИ ВХОДА](../t-sql/statements/create-login-transact-sql.md)
* [СОЗДАНИЕ ГЛАВНОГО КЛЮЧА](../t-sql/statements/create-master-key-transact-sql.md)
* [СОЗДАНИЕ РОЛИ](../t-sql/statements/create-role-transact-sql.md)
* [СОЗДАНИЕ ПОЛЬЗОВАТЕЛЯ](../t-sql/statements/create-user-transact-sql.md)
* [УДАЛИТЬ СЕРТИФИКАТ](../t-sql/statements/drop-certificate-transact-sql.md)
* [УДАЛИТЬ КЛЮЧ ШИФРОВАНИЯ БАЗЫ ДАННЫХ](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [УДАЛИТЬ ИМЯ ВХОДА](../t-sql/statements/drop-login-transact-sql.md)
* [DROP MASTER KEY](../t-sql/statements/drop-master-key-transact-sql.md)
* [УДАЛЕНИЕ РОЛИ](../t-sql/statements/drop-role-transact-sql.md)
* [УДАЛИТЕ ПОЛЬЗОВАТЕЛЯ](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>Следующие шаги
Дополнительные справочные сведения см. в разделе [элементы языка T-SQL](tsql-language-elements.md) и [системных представлений T-SQL](tsql-system-views.md).

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
