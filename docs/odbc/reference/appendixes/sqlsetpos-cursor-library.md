---
title: SQLSetPos (библиотека курсоров) | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8a683d5b523205aa369769a612cf2b27cdb4800
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (библиотека курсоров)
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этой возможности в новых разработках и запланируйте изменение приложений, которые сейчас ее используют. Корпорация Майкрософт рекомендует использовать функциональность курсора драйвера.  
  
 В этом разделе рассматриваются вопросы применения **SQLSetPos** функции в библиотеку курсоров. Общие сведения о **SQLSetPos**, в разделе [функция SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 Библиотека курсоров поддерживает операцию SQL_POSITION только для *операции* аргумент в **SQLSetPos**. Он поддерживает SQL_LOCK_NO_CHANGE значение только для *LockType* аргумент.  
  
 Если драйвер не поддерживает массовых операций, библиотеку курсоров возвращает SQLSTATE HYC00 (драйверы, не поддерживающих) при **SQLSetPos** вызывается с *RowNumber* равно 0. Это поведение драйвера не рекомендуется.  
  
 Библиотека курсоров не поддерживает операции SQL_UPDATE и SQL_DELETE при обращении к **SQLSetPos**. Реализует библиотеки курсоров позиционированные обновления или удаления инструкции SQL, создав поисковое обновление или удаление оператора с предложением WHERE, который перечисляет значения, хранящиеся в кэше для каждого привязанного столбца. Дополнительные сведения см. в разделе [обработки располагается обновление и удаление операторов](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Если драйвер не поддерживает статические курсоры, работе с библиотекой курсоров приложения должен вызывать **SQLSetPos** только для набора строк, возвращаемых при **SQLExtendedFetch** или **SQLFetchScroll** , а не по **SQLFetch**. Библиотека курсоров реализует **SQLExtendedFetch** и **SQLFetchScroll** , делая повторные вызовы из **SQLFetch** (с размером набора строк, 1) в драйвере. Библиотека курсоров передает вызовы **SQLFetch**, но другой стороны, с использованием драйвера. Если **SQLSetPos** вызывается для нескольких строк набора строк, выбранных **SQLFetch** Если драйвер не поддерживает статические курсоры, вызов завершится ошибкой, так как **SQLSetPos** не работает с помощью курсоров. Это происходит, даже если приложение успешно называется **SQLSetStmtAttr** SQL_ATTR_CURSOR_TYPE присваивается SQL_CURSOR_STATIC, который поддерживает библиотеку курсоров, даже если драйвер не поддерживает статические курсоры.
