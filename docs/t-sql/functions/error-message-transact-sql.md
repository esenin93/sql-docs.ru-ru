---
title: ERROR_MESSAGE (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 68439f7a9ea22078660d6e0465961c052002e8be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает текст сообщения об ошибке, которая возникла в блоке CATCH конструкции TRY…CATCH при выполнении.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>Возвращаемое значение  
 При вызове в блоке CATCH возвращает полный текст сообщения об ошибке, запустившей блок CATCH. Текст содержит значения подставляемых параметров, таких как длина, имена объектов или время.  
  
 Возвращает значение NULL в случае вызова вне блока CATCH.  
  
## <a name="remarks"></a>Remarks  
 Функция ERROR_MESSAGE может быть вызвана в любом месте области блока CATCH.  
  
 Функция ERROR_MESSAGE возвращает сообщение об ошибке независимо от количества ее появлений или от ее конкретного месторасположения внутри блока CATCH. В этом и заключается отличие от таких функций, как @@ERROR, которые возвращают номер ошибки в инструкции только сразу после ее обнаружения или в первой инструкции блока CATCH.  
  
 Во вложенных блоках CATCH функция ERROR_MESSAGE возвращает сообщение об ошибке, соответствующее области блока CATCH, в котором она возникла. Например, блок CATCH внешней конструкции TRY...CATCH может содержать вложенную конструкцию TRY...CATCH. Внутри вложенного блока CATCH функция ERROR_MESSAGE возвращает сообщение об ошибке, вызвавшей вложенный блок CATCH. Если функция ERROR_MESSAGE выполняется во внешнем блоке CATCH, она возвращает сообщение об ошибке, вызвавшей этот блок CATCH.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. Использование функции ERROR_MESSAGE в блоке CATCH  
 В следующем примере кода приведена инструкция `SELECT`, формирующая ошибку деления на ноль. Возвращается сообщение об ошибке.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>Б. Использование функции ERROR_MESSAGE в блоке CATCH с другими средствами обработки ошибок  
 В следующем примере кода приведена инструкция `SELECT`, формирующая ошибку деления на ноль. Вместе с сообщением об ошибке возвращаются сведения, имеющие отношение к ней.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>В. Использование функции ERROR_MESSAGE в блоке CATCH с другими средствами обработки ошибок  
 В следующем примере кода приведена инструкция `SELECT`, формирующая ошибку деления на ноль. Вместе с сообщением об ошибке возвращаются сведения, имеющие отношение к ней.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  

