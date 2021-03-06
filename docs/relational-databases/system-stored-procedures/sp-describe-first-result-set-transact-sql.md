---
title: sp_describe_first_result_set (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 12890dc6282f879259730530b3ff8f03fc6de8b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Возвращает метаданные для первого возможного результирующего набора [!INCLUDE[tsql](../../includes/tsql-md.md)] пакета. Возвращает пустой результирующий набор, если пакет не вернул результатов. Вызывает ошибку, если [!INCLUDE[ssDE](../../includes/ssde-md.md)] не удается определить метаданные для первого запроса, который будет выполнен при выполнении статического анализа. Динамическое административное представление [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) возвращает те же сведения.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@tsql =** ] **"***Transact SQL_batch***"**  
 Одна или несколько инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)]. *Transact SQL_batch* может быть **nvarchar (***n***)** или **nvarchar(max)**.  
  
 [  **@params =** ] **N'***параметры***"**  
 @params обеспечивает строку объявления параметров для [!INCLUDE[tsql](../../includes/tsql-md.md)] пакета, схожего с sp_executesql. Параметры могут быть **nvarchar(n)** или **nvarchar(max)**.  
  
 Строка, содержащая определения всех параметров, внедренных в [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*. Строка должна представлять собой константу в Юникоде либо переменную в этом же формате. Определение каждого параметра состоит из имени параметра и типа данных. *n* — заполнитель, означающий определения дополнительных параметров. Каждый параметр, указанный в инструкции должен быть определен в @params. Если [!INCLUDE[tsql](../../includes/tsql-md.md)] инструкцию или пакет в инструкции не содержит параметров, @params не требуется. Значением по умолчанию для этого аргумента является NULL.  
  
 [  **@browse_information_mode =** ] *tinyint*  
 Указывает, происходит ли возврат дополнительных ключевых столбцов и сведений об исходной таблице. Если он имеет значение 1, то каждый запрос анализируется аналогично анализу запроса с параметром FOR BROWSE. Возвращаются дополнительные ключевые столбцы и сведения об исходной таблице.  
  
-   Если задано значение 0, то данные не возвращаются.  
  
-   Если он имеет значение 1, то каждый запрос анализируется аналогично анализу запроса с параметром FOR BROWSE. Это приводит к возврату имен базовых таблиц в качестве сведений об исходном столбце.  
  
-   Если задано значение 2, то каждый запрос анализируется так, как если бы он использовался для подготовки или выполнения курсора. Тогда в качестве сведений об исходном столбце возвращаются имена представлений.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **sp_describe_first_result_set** всегда возвращает состояние 0 в случае успешного выполнения. Если процедура вызывает ошибку и процедура вызывается через RPC, возвращаемое состояние заполняется типом ошибки, описанным в столбце error_type sys.dm_exec_describe_first_result_set. Если процедура вызывается из [!INCLUDE[tsql](../../includes/tsql-md.md)], то возвращаемое значение всегда равно нулю, даже при наличии ошибок.  
  
## <a name="result-sets"></a>Результирующие наборы  
 Эти общие метаданные возвращаются в виде результирующего набора с одной строкой для каждого столбца в результирующих метаданных. Каждая строка описывает тип и допустимость значений NULL в столбце в формате, описанном в следующем разделе. Если первая инструкция не существует для каждого пути управления, возвращается результирующий набор с нулем строк.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**бит NOT NULL**|Указывает, что столбец является дополнительным, добавленным для целей просмотра сведений, и что он фактически не отображается в результирующем наборе.|  
|**column_ordinal**|**int NOT NULL**|Содержит порядковый номер столбца в результирующем наборе. Позиция первого столбца будет указана как 1.|  
|**name**|**sysname NULL**|Содержит имя столбца, если его можно определить. В противном случае будет содержать значение NULL.|  
|**is_nullable**|**бит NOT NULL**|Содержит значение 1, если столбец допускает значения NULL, значение 0, если столбец не допускает значения NULL, и значение 1, если не удалось определить, допускает ли столбец значения NULL.|  
|**system_type_id**|**int NOT NULL**|Содержит system_type_id для типа данных столбца, как указано в sys.types. Для типов CLR, даже если system_type_name возвращает NULL, этот столбец вернет значение 240.|  
|**system_type_name**|**nvarchar(256) значение NULL**|Содержит имя и аргументы (длина, точность, масштаб и т. д.), указанные для типа данных столбца. Если тип данных является пользовательским псевдонимом, то здесь указывается базовый системный тип данных. Если это определяемый пользователем тип данных CLR, то в этом столбце вернется NULL.|  
|**max_length**|**Smallint, не NULL**|Максимальная длина столбца (в байтах).<br /><br /> -1 = тип данных столбца — **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, или **xml**.<br /><br /> Для **текст** столбцы, **max_length** значение будет равно 16 или значение, установленное **sp_tableoption «text in row»**.|  
|**precision**|**tinyint NOT NULL**|Точность столбца, если он является числовым. В противном случае возвращается 0.|  
|**масштаб**|**tinyint NOT NULL**|Масштаб значений столбца в случае числового выражения. В противном случае возвращается 0.|  
|**collation_name**|**sysname NULL**|Имя параметров сортировки столбца, если он символьный. В противном случае возвращается NULL.|  
|**user_type_id**|**int NULL**|Для типов CLR и псевдонимов содержит user_type_id для типа данных столбца, как указано в sys.types. В противном случае значение равно NULL.|  
|**user_type_database**|**sysname NULL**|Для типов CLR и псевдонимов содержит имя базы данных, в которой этот тип определен. В противном случае значение равно NULL.|  
|**user_type_schema**|**sysname NULL**|Для типов CLR и псевдонимов содержит имя схемы, в которой этот тип определен. В противном случае значение равно NULL.|  
|**user_type_name**|**sysname NULL**|Для типов CLR и псевдонимов содержит имя типа. В противном случае значение равно NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Для типов CLR возвращает имя сборки и класса, определяющего тип. В противном случае значение равно NULL.|  
|**xml_collection_id**|**int NULL**|Содержит xml_collection_id для типа данных столбца, как указано в sys.columns. Этот столбец возвратит NULL, если возвращаемый тип не связан с коллекцией схем XML.|  
|**xml_collection_database**|**sysname NULL**|Содержит базу данных, в которой определена коллекция схем XML, связанная с этим типом. Этот столбец возвратит NULL, если возвращаемый тип не связан с коллекцией схем XML.|  
|**xml_collection_schema**|**sysname NULL**|Содержит схему, в которой определена коллекция схем XML, связанная с этим типом. Этот столбец возвратит NULL, если возвращаемый тип не связан с коллекцией схем XML.|  
|**xml_collection_name**|**sysname NULL**|Содержит имя коллекции схем XML, связанной с этим типом. Этот столбец возвратит NULL, если возвращаемый тип не связан с коллекцией схем XML.|  
|**is_xml_document**|**бит NOT NULL**|Возвращает значение 1, если возвращается тип данных XML, который гарантированно будет полным XML-документом (включая корневой узел), а не фрагментом XML. В противном случае возвращается 0.|  
|**is_case_sensitive**|**бит NOT NULL**|Возвращает значение 1, если столбец относится к строковому типу с учетом регистра, либо значение 0 в противном случае.|  
|**is_fixed_length_clr_type**|**бит NOT NULL**|Возвращает значение 1, если столбец относится имеет тип CLR с фиксированной длиной, либо в противном случае значение 0.|  
|**source_server**|**sysname**|Имя исходного сервера, возвращаемое столбцом этого результата (если он исходит от удаленного сервера). Имя дается так, как оно отображается в представлении sys.servers. Возвращает NULL, если столбец поступает с локального сервера или если невозможно определить, с какого сервера он поступил. Заполняется только при запросе просмотра информации.|  
|**база_данных_источник**|**sysname**|Имя исходной базы данных, возвращаемое столбцом этого результата. Возвращает NULL, если не удалось определить базу данных. Заполняется только при запросе просмотра информации.|  
|**source_schema**|**sysname**|Имя исходной схемы, возвращаемое столбцом в этом результате. Возвращает NULL, если не удалось определить схему. Заполняется только при запросе просмотра информации.|  
|**source_table**|**sysname**|Имя исходной таблицы, возвращаемое столбцом в этом результате. Возвращает NULL, если не удалось определить таблицу. Заполняется только при запросе просмотра информации.|  
|**source_column**|**sysname**|Имя исходного столбца, возвращаемое результирующим столбцом. Возвращает NULL, если не удалось определить столбец. Заполняется только при запросе просмотра информации.|  
|**is_identity_column**|**бит NULL**|Возвращает значение 1, если столбец является столбцом идентификаторов, либо значение 0 в противном случае. Возвращает NULL, если не удалось определить, является ли столбец столбцом идентификаторов.|  
|**is_part_of_unique_key**|**бит NULL**|Возвращает значение 1, если столбец является частью уникального индекса (включая ограничение уникальности и первичности), либо значение 0 в противном случае. Возвращает NULL, если не удалось определить, является ли столбец частью уникального индекса. Заполняется только при запросе просмотра информации.|  
|**is_updateable**|**бит NULL**|Возвращает значение 1, если столбец можно обновлять, либо значение 0 в противном случае. Возвращает NULL, если не удалось определить, можно ли обновлять столбец.|  
|**is_computed_column**|**бит NULL**|Возвращает значение 1, если столбец является вычисляемым столбцом, либо значение 0 в противном случае. Возвращает NULL, если не удалось определить, является ли столбец вычисляемым столбцом.|  
|**is_sparse_column_set**|**бит NULL**|Возвращает значение 1, если столбец является разреженным, и значение 0 в противном случае. Возвращает NULL, если не удалось определить, является ли столбец частью набора разреженных столбцов.|  
|**ordinal_in_order_by_list**|**smallint NULL**|Позиция этого столбца в списке ORDER BY. Возвращает NULL, если столбец не отображается в списке ORDER BY, или если список ORDER BY нельзя однозначно определить.|  
|**order_by_list_length**|**smallint NULL**|Длина списка ORDER BY. Возвращает NULL, если нет списка ORDER BY или если список ORDER BY нельзя однозначно определить. Обратите внимание, что это значение будет одинаковым для всех строк, возвращенных **sp_describe_first_result_set.**|  
|**order_by_is_descending**|**smallint NULL**|Если значение ordinal_in_order_by_list не равно NULL, **order_by_is_descending** столбца сообщает направление предложение ORDER BY для этого столбца. В противном случае возвращается значение NULL.|  
|**tds_type_id**|**int NOT NULL**|Для внутреннего использования.|  
|**tds_length**|**int NOT NULL**|Для внутреннего использования.|  
|**tds_collation_id**|**int NULL**|Для внутреннего использования.|  
|**tds_collation_sort_id**|**тип tinyint и значение NULL**|Для внутреннего использования.|  
  
## <a name="remarks"></a>Замечания  
 **sp_describe_first_result_set** гарантирует, что если процедура возвращает метаданные первого результирующего набора для (гипотетического) пакета A и пакета (A) при последующем выполнены затем пакета будет либо (1), возникает ошибка во время оптимизации (2) вызывает ошибку времени выполнения, (3) не возвращает никаких результатов установите или (4) возвращает первого результирующего набора с одинаковыми метаданными, описываемого **sp_describe_first_result_set**.  
  
 Имя, допустимость значений NULL и тип данных могут различаться. Если **sp_describe_first_result_set** возвращает пустой результирующий набор, гарантия — что пакетное выполнение будет возвращать нет результирующих наборов.  
  
 При этом предполагается, что на сервере не было внесено изменений в соответствующие схемы. Не включать создание временных таблиц или табличных переменных в пакете A в промежутке между изменениям соответствующих схем на сервере, **sp_describe_first_result_set** вызывается и временем, результирующий набор возвращается во время выполнения, включая изменения схем пакетом B.  
  
 **sp_describe_first_result_set** возвращает сообщение об ошибке в любом из следующих случаев.  
  
-   Если входные данные @tsql не является допустимым [!INCLUDE[tsql](../../includes/tsql-md.md)] пакета. Действия определяется синтаксического разбора и анализа [!INCLUDE[tsql](../../includes/tsql-md.md)] пакета. Все ошибки, вызванных пакетом во время оптимизации запроса или во время выполнения не учитываются при определении ли [!INCLUDE[tsql](../../includes/tsql-md.md)] пакета является допустимым.  
  
-   Если @params не равно NULL и содержит строку, не является синтаксически правильной строкой объявления для параметров, или если она содержит строку, в котором объявлен какого-либо параметра более одного раза.  
  
-   Если входные данные [!INCLUDE[tsql](../../includes/tsql-md.md)] пакет объявляет локальную переменную с тем же именем, как параметр, объявленный в @params.  
  
-   Если инструкция использует временную таблицу.  
  
-   В запрос включено создание постоянной таблицы, к которой он будет обращен.  
  
 При успешном выполнении остальных проверок учитываются все возможные пути потоков управления. Это учитывались все управление потоком инструкций (GOTO, IF/ELSE, WHILE, и [!INCLUDE[tsql](../../includes/tsql-md.md)] блоки TRY/CATCH) и процедуры и динамические [!INCLUDE[tsql](../../includes/tsql-md.md)] пакетов или вызывается из входного пакета с помощью инструкции EXEC, инструкцию DDL, которая запускает триггеры Срабатывание триггеров DDL или DML-инструкции, которое вызывает срабатывание триггеров в целевой таблице или в таблице, изменено из-за каскадные действия на ограничение внешнего ключа. При наличии нескольких возможных путей управления на определенном этапе выполнение алгоритма прерывается.  
  
 Для всех путей потоков управления первая инструкция (если таковые имеются), возвращает результирующий набор, определяется **sp_describe_first_result_set**.  
  
 При наличии в пакете нескольких первых инструкций результаты могут различаться, т.е. могут быть получены различные количества столбцов, имена столбцов, допустимости значений NULL и типы данных. Ниже более подробно описывается обработка этих различий:  
  
-   При получении различного количества столбцов в результатах вызывается ошибка и результат не возвращается.  
  
-   Если отличаются имена столбцов, для имен возвращаемых столбцов задается значение NULL.  
  
-   Если различается допустимость значений NULL, то будет разрешено задание значений NULL.  
  
-   Если типы данных различаются, будет вызвана ошибка и не будет возвращен результат, за исключением следующих случаев:  
  
    -   **varchar(a)** для **varchar(a')** где ">.  
  
    -   **varchar(a)** для **varchar(max)**  
  
    -   **nvarchar(a)** для **nvarchar(a')** где ">.  
  
    -   **nvarchar(a)** для **nvarchar(max)**  
  
    -   **varbinary(a)** для **varbinary(a')** где ">.  
  
    -   **varbinary(a)** для **varbinary(max)**  
  
 **sp_describe_first_result_set** не поддерживает косвенную рекурсию.  
  
## <a name="permissions"></a>Разрешения  
 Требуется разрешение на выполнение @tsql аргумент.  
  
## <a name="examples"></a>Примеры  
  
### <a name="typical-examples"></a>Наиболее распространенные примеры  
  
#### <a name="a-simple-example"></a>A. Простой пример  
 В следующем примере описывается результирующий набор, возвращаемый одним запросом.  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 В следующем примере описывается результирующий набор, возвращаемый одним запросом, в котором содержится параметр.  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>Б. Примеры режима просмотра  
 В следующих трех примерах показаны ключевые различия между разными режимами просмотра сведений. В результаты запроса включены только столбцы, относящиеся к теме.  
  
 В примере используется значение 0, которое указывает, что возврата сведений не происходит.  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|имя|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 В примере используется значение 1, которое указывает, что возврат сведений происходит так, как если бы в запросе был указан параметр FOR BROWSE.  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|имя|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 В примере используется значение 2, которое показывает, что анализ выполняется так же, как и при подготовке курсора.  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|имя|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>Примеры проблем  
 Ниже во всех примерах используются две таблицы. Для создания примеров таблиц выполните следующие инструкции.  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>Ошибка, вызванная различием в количестве столбцов  
 В этом примере различается количество столбцов в возможных первых результирующих наборах.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>Ошибка, вызванная различием типов данных  
 Типы столбцов различаются в возможных первых результирующих наборах.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 Результат: Ошибка, несовпадающие типы (**int** и **smallint**).  
  
#### <a name="column-name-cannot-be-determined"></a>Не удается определить имя столбца  
 У столбцов в различных первых результирующих наборах различается длина в одном типе переменной длины, допустимость значений NULL и имена столбцов:  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 Результат: \<неизвестное имя столбца > **varchar(20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>Для имен столбцов принудительно обеспечивается соответствие с помощью присвоения псевдонимов  
 Аналогично предыдущему, но имена столбцов идентичны благодаря присвоению псевдонимов.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 Результат: b **varchar (20) значение NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>Ошибка, вызванная невозможностью сопоставления типов столбцов  
 Типы столбцов различаются в возможных первых результирующих наборах.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 Результат: Ошибка, несовпадающие типы (**varchar(10)** и **nvarchar(10)**).  
  
#### <a name="result-set-can-return-an-error"></a>Результирующий набор может вернуть ошибку  
 Первым результирующим набором передается либо ошибка, либо действительно результирующий набор.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 Результат: **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>Некоторые кодовые пути не возвращают результаты  
 Первым результирующим набором передается либо значение NULL, либо действительно результирующий набор.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 Результат: **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>Результат динамического SQL  
 Первый результирующий набор является динамическим SQL, который можно обнаружить, поскольку он является строковым литералом.  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 Результат: **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>Результат: ошибка динамического SQL  
 Невозможно определить первый результирующий набор из-за динамического SQL.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 Результат: ошибка. Результат невозможно обнаружить из-за динамического SQL.  
  
#### <a name="result-set-specified-by-user"></a>Результирующий набор, указываемый пользователем  
 Первый результирующий набор указывается пользователем вручную.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 Результат: Column1 **bigint NOT NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>Ошибка вызвана неоднозначным результирующим набором  
 В этом примере предполагается, что другой пользователь с именем user1 имеет таблицу с именем t1 в схеме по умолчанию s1 со столбцами ( **int NOT NULL**).  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 Результат: ошибка. T1 может быть dbo.t1 или s1.t1 с Разное количество столбцов.  
  
#### <a name="result-even-with-ambiguous-result-set"></a>Результат возвращается даже при неоднозначном результирующем наборе  
 Используйте те же предположения, что и в предыдущем примере.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 Результат: **int NULL** поскольку dbo.t1.a и s1.t1.a имеют тип **int** и различную допустимость значений NULL.  
  
## <a name="see-also"></a>См. также  
 [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
