---
title: Константы (драйверы Майкрософт для PHP для SQL Server) | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
caps.latest.revision: 72
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a09ba7744f03fca15bb60db7979d31bb141f75c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>Константы (драйверы Майкрософт для PHP для SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Эта статья описывает константы, которые определены [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="pdosqlsrv-driver-constants"></a>Константы драйвера PDO_SQLSRV  
Константы, перечисленные на [веб-сайте PDO](http://php.net/manual/book.pdo.php) допустимы в [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Ниже описаны константы систем Microsoft в драйвере PDO_SQLSRV.  
  
### <a name="transaction-isolation-level-constants"></a>Константы уровня изоляции транзакции  
Ключ **TransactionIsolation** , который используется с [PDO::__construct](../../connect/php/pdo-construct.md), принимает одну из следующих констант:  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
Дополнительные сведения о ключе **TransactionIsolation** см. в статье [Connection Options](../../connect/php/connection-options.md).  
  
### <a name="encoding-constants"></a>Константы кодировки  
Атрибут PDO::SQLSRV_ATTR_ENCODING можно передать [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md), [PDO::prepare](../../connect/php/pdo-prepare.md), [PDOStatement: : bindColumn](../../connect/php/pdostatement-bindcolumn.md), и [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md).  
  
Для передачи в PDO::SQLSRV_ATTR_ENCODING доступны следующие значения:  
  
|Константа драйвера PDO_SQLSRV|Описание|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|Данные представляют собой поток необработанных байтов с сервера без применения кодировки или преобразования.<br /><br />Не является допустимым для PDO::setAttribute.|  
|PDO::SQLSRV_ENCODING_SYSTEM|Данные представлены 8-битными символами, как указано в кодовой странице языкового стандарта Windows, установленного в системе. Любой многобайтовых символов или символов, не соответствующих этой кодовой странице, подставляется символ однобайтовый вопросительный знак (?).|  
|PDO::SQLSRV_ENCODING_UTF8|Данные имеют кодировку UTF-8. Эта кодировка используется по умолчанию.|  
|PDO::SQLSRV_ENCODING_DEFAULT|Использует PDO::SQLSRV_ENCODING_SYSTEM, если указано во время соединения.<br /><br />Используйте кодировку соединения, если указано в инструкции prepare.|  
  
### <a name="query-timeout"></a>Время ожидания запроса  
Атрибут PDO::SQLSRV_ATTR_QUERY_TIMEOUT — это неотрицательное целое число, представляющее время ожидания в секундах. По умолчанию использует нуль (0), означающий отсутствие времени ожидания.  
  
Можно указать атрибут PDO::SQLSRV_ATTR_QUERY_TIMEOUT с [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md), и [PDO::prepare](../../connect/php/pdo-prepare.md).  
  
### <a name="direct-or-prepared-execution"></a>Прямое или подготовленное выполнение  
С помощью атрибута PDO::SQLSRV_ATTR_DIRECT_QUERY можно выбрать выполнение прямого запроса или подготовленной инструкции. Можно задать PDO::SQLSRV_ATTR_DIRECT_QUERY [PDO::prepare](../../connect/php/pdo-prepare.md) или [PDO::setAttribute](../../connect/php/pdo-setattribute.md). Дополнительные сведения о PDO::SQLSRV_ATTR_DIRECT_QUERY см. в разделе [выполнение прямых и подготовленных инструкций в драйвере PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  

### <a name="handling-numeric-fetches"></a>Обработка числовых выборки
Атрибут PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE можно использовать для обработки числовых выборки из столбцов с числовыми типами SQL (бит, целое число со знаком, smallint, tinyint, float и real). Когда PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE имеет значение true, в результате целочисленном столбце представлены в виде целых чисел, пока смещает SQL и reals представляются в виде значений с плавающей запятой. Этот атрибут можно установить с [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md). 


## <a name="sqlsrv-driver-constants"></a>SQLSRV  
Следующие разделы содержат константы, используемые драйвером SQLSRV.  
  
### <a name="err-constants"></a>Константы ERR  
В следующей таблице перечислены константы, которые используются для указания, если [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) возвращает ошибки и предупреждения.  
  
|Значение|Описание|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Возвращаются ошибки и предупреждения, созданные при последнем вызове функции **sqlsrv** . Это значение по умолчанию.|  
|SQLSRV_ERR_ERRORS|Возвращаются ошибки, созданные при последнем вызове функции **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Возвращаются предупреждения, созданные при последнем вызове функции **sqlsrv** .|  
  
### <a name="fetch-constants"></a>Константы FETCH  
Следующая таблица содержит константы, которые используются для указания типа массива, возвращаемого [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
|Константа SQLSRV|Описание|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** возвращает следующую строку данных в виде ассоциативного массива.|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** возвращает следующую строку данных в виде массива с числовыми и ассоциативными ключами. Это значение по умолчанию.|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** возвращает следующую строку данных в виде массива с числовым индексом.|  
  
### <a name="logging-constants"></a>Константы ведения журнала  
Этот раздел содержит константы, которые используются для изменения параметров ведения журнала с помощью [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). Дополнительные сведения об ведении журнала см. в статье [Logging Activity](../../connect/php/logging-activity.md).  
  
Следующая таблица содержит константы, которые можно использовать в качестве значения для параметра **LogSubsystems** :  
  
|Константа SQLSRV (целочисленный эквивалент в скобках)|Описание|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Включает ведения журнала для всех подсистем.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Включает ведения журнала по соединениям.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Включает ведения журнала по инициализации.|  
|SQLSRV_LOG_SYSTEM_OFF (0)|Отключает ведение журнала.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Включает ведения журнала по инструкциям.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Включение ведения журнала ошибок (например, **handle_error** и **handle_warning**).|  
  
Следующая таблица содержит константы, которые можно использовать в качестве значения для параметра **LogSeverity** :  
  
|Константа SQLSRV (целочисленный эквивалент в скобках)|Описание|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Указывает, что будут регистрироваться ошибки, предупреждения и уведомления.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Указывает, что будут регистрироваться ошибки.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Указывает, что будут регистрироваться уведомления.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Указывает, что будут регистрироваться предупреждения.|  
  
### <a name="nullable-constants"></a>Константы, допускающие значение NULL  
Следующая таблица содержит константы, которые можно использовать для определения того, допускает ли столбец значение NULL или такие сведения недоступны. Можно сравнить значение ключа **Nullable** , который возвращается [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) для определения состояния поддержки значений NULL столбца.  
  
|Константа SQLSRV (целочисленный эквивалент в скобках)|Описание|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|Этот столбец допускает значение NULL.|  
|SQLSRV_NULLABLE_NO (1)|Столбец не допускает значение NULL.|  
|SQLSRV_NULLABLE_UNKNOWN (2)|Неизвестно, допускает ли столбец значение NULL.|  
  
### <a name="param-constants"></a>Константы PARAM  
Следующий список содержит константы для указания направления параметров при вызове [sqlsrv_query](../../connect/php/sqlsrv-query.md) или [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
|Константа SQLSRV|Описание|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|Указывает параметр ввода.|  
|SQLSRV_PARAM_INOUT|Указывает двунаправленный параметр.|  
|SQLSRV_PARAM_OUT|Указывает параметр вывода.|  
  
### <a name="phptype-constants"></a>Константы PHPTYPE  
Следующая таблица содержит константы, которые используются для описания типов данных PHP. Сведения о типах данных PHP см. в разделе [типы PHP](http://php.net/manual/en/language.types.php).  
  
|Константа SQLSRV|Тип данных PHP|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Целочисленный|  
|SQLSRV_PHPTYPE_DATETIME|DateTime|  
|SQLSRV_PHPTYPE_FLOAT|Число с плавающей запятой|  
|SQLSRV_PHPTYPE_STREAM (кодировка $<sup>1</sup>)|STREAM|  
|SQLSRV_PHPTYPE_STRING (кодировка $<sup>1</sup>)|Строковые значения|  
  
1. **SQLSRV_PHPTYPE_STREAM** и **SQLSRV_PHPTYPE_STRING** принимают параметр, который указывает кодировку потока. Следующая таблица содержит константы SQLSRV, которые являются допустимыми параметрами, а также описание соответствующей кодировки.  
  
|Константа SQLSRV|Описание|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|Данные возвращаются в виде потока необработанных байтов с сервера без применения кодировки или преобразования.|  
|SQLSRV_ENC_CHAR|Данные возвращаются в виде 8-битных символов, как указано в кодовой странице языкового стандарта Windows, установленного в системе. Любой многобайтовых символов или символов, не соответствующих этой кодовой странице, подставляется символ однобайтовый вопросительный знак (?).<br /><br />Эта кодировка используется по умолчанию.|  
|"UTF-8"|Данные возвращаются с кодировкой UTF-8. Эта константа была добавлена в версии 1.1 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Дополнительные сведения о поддержке UTF-8 см. в разделе [как: отправки и получения UTF-8 данных с помощью встроенной поддержки UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|  
  
> [!NOTE]  
> При использовании **SQLSRV_PHPTYPE_STREAM** или **SQLSRV_PHPTYPE_STRING**, должна быть указана кодировка. Если параметр не указан, возвращается ошибка.  
  
Дополнительные сведения об этих константах см. в статье [Практическое руководство. Указание типов данных PHP](../../connect/php/how-to-specify-php-data-types.md)и [Практическое руководство. Извлечение символьных данных в виде потока с помощью драйвера SQLSRV](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md).  
  
### <a name="sqltype-constants"></a>Константы SQLTYPE  
Следующая таблица содержит константы, которые используются для описания типов данных SQL Server. Некоторые константы подобный функции и может занять параметры, которые соответствуют точности, масштаба или длины.  При привязке параметров, следует использовать константы подобный функции. Для сравнения типов требуются стандартные константы (не как функция). Сведения о типах данных SQL Server см. в разделе [типы данных (Transact-SQL).](../../t-sql/data-types/data-types-transact-sql.md) Сведения о точности, масштаба и длины см. в разделе [точность, масштаб и длина (Transact-SQL).](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
|Константа SQLSRV|Тип данных SQL Server|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|bigint|  
|SQLSRV_SQLTYPE_BINARY|BINARY|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|char<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char;|  
|SQLSRV_SQLTYPE_DATE|date<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|datetime|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|десятичное число<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|Decimal|  
|SQLSRV_SQLTYPE_FLOAT|float|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|int|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|nchar<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|числовые<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|numeric|  
|SQLSRV_SQLTYPE_NVARCHAR|nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|nvarchar|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|real|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|smallint|  
|SQLSRV_SQLTYPE_SMALLMONEY|smallmoney|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|TIMESTAMP|  
|SQLSRV_SQLTYPE_TINYINT|tinyint|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|uniqueidentifier|  
|SQLSRV_SQLTYPE_UDT|определяемый пользователем тип|  
|SQLSRV_SQLTYPE_VARBINARY|varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary(MAX)|  
|SQLSRV_SQLTYPE_VARCHAR|varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARCHAR('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|xml|  
  
1.  Это устаревший тип, соответствующий типу varbinary(max).  
  
2.  Это устаревший тип, соответствующий более новому типу nvarchar.  
  
3.  Это устаревший тип, соответствующий более новому типу varchar.  
  
4.  Поддержка PDO для этого типа была добавлена в версии 1.1 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

5.  Эти константы должны использоваться в операциях сравнения типа и не замените синтаксис, похожий константы подобный функции. Для параметров привязки, следует использовать функцию как константы.

  
Следующая таблица содержит константы SQLTYPE, которые принимают параметры, а также диапазон допустимых значений для параметра.  
  
|SQLTYPE|Параметр|Диапазон допустимых значений для параметра|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR,<br /><br />SQLSRV_SQLTYPE_VARCHAR|charCount|1–8000|  
|SQLSRV_SQLTYPE_NCHAR,<br /><br />SQLSRV_SQLTYPE_NVARCHAR|charCount|1–4000|  
|SQLSRV_SQLTYPE_BINARY,<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1–8000|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|precision|1–38|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|масштаб|1 — точность|  
  
### <a name="transaction-isolation-level-constants"></a>Константы уровня изоляции транзакции  
Ключ **TransactionIsolation** , который используется с [sqlsrv_connect](../../connect/php/sqlsrv-connect.md), принимает одну из следующих констант:  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>Курсор и прокрутка констант  
Следующие константы указывают тип курсора, который можно использовать в результирующем наборе:  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
Следующие константы указывают, какую строку следует выбрать в результирующем наборе:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Сведения об использовании этих констант см. в статье [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
## <a name="see-also"></a>См. также  
[Справочник по API для драйвера SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
