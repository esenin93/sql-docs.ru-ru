---
title: "Функции уровня 2 API-Интерфейс (драйвер ODBC для Oracle) | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb35e0e2dde90261e913ffd9ba3dc28e5859e012
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Функции уровня 2 API-Интерфейс (драйвер ODBC для Oracle)
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Вместо этого используйте драйвер ODBC, предоставляемого корпорацией Oracle.  
  
 Функции на этом уровне обеспечивают соответствие интерфейс уровня 1, а также дополнительные функциональные возможности, такие как поддержка закладок, динамических параметров и асинхронное выполнение функции ODBC.  
  
|API-функции|Примечания|  
|------------------|-----------|  
|**SQLBindParameter**|Связывает буфер с маркер параметра в инструкции SQL.|  
|**SQLBrowseConnect**|Возвращает последовательные уровни атрибутов и значений атрибутов.|  
|**SQLDataSources**|Список имен источников данных. Реализовано с помощью диспетчера драйверов.|  
|**SQLDescribeParam**|Возвращает описание маркер параметра, связанный с подготовленной инструкции SQL.<br /><br /> Возвращает наиболее подходящие того, какой параметр, при анализе инструкцию. Если не удается определить тип параметра, SQL_VARCHAR возвращается длина 2000.|  
|**SQLDrivers**|Реализовано с помощью диспетчера драйверов.|  
|**SQLExtendedFetch**|Аналогично **SQLFetch** , но возвращает несколько строк с помощью массива для каждого столбца. Результирующий набор может прокручиваться вперед и могут выполняться обратной прокрутки, если определено как статические, не однопроходный курсор. Для курсоров с привязкой по умолчанию столбец столбец данных в наборах данных, больше, чем атрибут соединения BUFFERSIZE выбирается непосредственно в буферов данных. Не поддерживает закладки переменной длины и не поддерживает извлечение строк со смещением (отличное от 0) относительно закладки.|  
|**SQLForeignKeys**|Возвращает список внешних ключей в одну таблицу или список внешние ключи в других таблицах, ссылающихся на одну таблицу.|  
|**SQLMoreResults**|Определяет, являются ли ожидающие Дополнительные результаты на дескрипторе инструкции hstmt, содержащий инструкции SELECT, UPDATE, INSERT или DELETE и если да, инициализирует обработки для этих результатов.<br /><br /> Oracle поддерживает несколько результирующих наборов только из хранимых процедур при использовании escape-последовательности {resultset}.|  
|**SQLNativeSql**|Сведения об использовании см. в разделе [возвращения массива параметров из хранимых процедур](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Возвращает число параметров в инструкции SQL. Число параметров должно быть равно числу вопросительных знаков в инструкции SQL, передаваемый **SQLPrepare**.|  
|**SQLPrimaryKeys**|Возвращает имена столбцов, которые составляют первичный ключ для таблицы.|  
|**SQLProcedureColumns**|Возвращает список входных данных и выходных параметров, возвращаемое значение, столбцы в результирующем наборе одну процедуру и два дополнительных столбца, ПЕРЕГРУЗКА и ORDINAL_POSITION. ПЕРЕГРУЗКА является ПЕРЕГРУЗКА столбец из таблицы ALL_ARGUMENTS представления словаря данных Oracle. ORDINAL_POSITION является столбец ПОСЛЕДОВАТЕЛЬНОСТИ из таблицы ALL_ARGUMENTS представления словаря данных Oracle. Упакованные процедур имя ПРОЦЕДУРЫ столбец находится в *packagename.procedurename* формат. Возвращает столбцы процедуры созданный синонима, который ссылается на процедуру или функцию.|  
|**SQLProcedures**|Возвращает список процедур в источнике данных. Упакованные процедур имя ПРОЦЕДУРЫ столбец находится в *packagename.procedurename* формат.<br /><br /> Поскольку Oracle не предоставляет способ различать упакованных процедуры из упакованных функций, драйвер возвращает SQL_PT_UNKNOWN для столбца PROCEDURE_TYPE.|  
|**SQLSetPos**|Задает положение курсора в набор строк. Можно использовать **SQLSetPos** с **SQLGetData** для получения строк из несвязанных столбцов после позиционирования курсора для конкретной строки в наборе строк. Строки добавляются к результирующему набору с помощью *fOption* SQL_ADD добавляются после последней строки в результирующем наборе.|  
|**SQLSetScrollOptions**|Задает параметры, которые управляют поведением курсоров, связанные с дескриптором инструкции hstmt. Дополнительные сведения см. в разделе [типа курсора и параллелизма сочетания](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|