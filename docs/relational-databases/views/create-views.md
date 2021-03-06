---
title: Создание представлений | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], creating
ms.assetid: 0b7bd2a1-544c-42ba-8e7b-4822f34d7b64
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 899bf2cdab8716927806042c1fce6532f8670dfa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="create-views"></a>Создание представлений
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
  Представления можно создать в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Представление можно использовать в следующих целях.  
  
-   Для направления, упрощения и настройки восприятия информации в базе данных каждым пользователем.  
  
-   В качестве механизма безопасности, позволяющего пользователям обращаться к данным через представления, но не предоставляя им разрешений на непосредственный доступ к базовым таблицам.  
  
-   Для предоставления интерфейса обратной совместимости, моделирующего таблицу, схема которой изменилась.  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [Ограничения](#Restrictions)  
  
     [безопасность](#Security)  
  
-   **Создание представления с использованием следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
 Представление может быть создано только в текущей базе данных.  
  
 Представление может включать не более 1 024 столбцов.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для выполнения этой инструкции требуется разрешение CREATE VIEW в отношении базы данных и разрешение ALTER в отношении схемы, в которой создается представление.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-create-a-view-by-using-the-query-and-view-designer"></a>Создание представления с использованием конструктора запросов и представлений  
  
1.  В **обозревателе объектов**разверните базу данных, в которой необходимо создать новое представление.  
  
2.  Щелкните правой кнопкой папку **Представления** и выберите **Создать представление...**  
  
3.  В диалоговом окне **Добавить таблицу** выберите один или несколько элементов, которые необходимо включить в новое представление, на одной из следующих вкладок: «Таблицы», «Представления», «Функции» и «Синонимы».  
  
4.  Щелкните **Добавить**, а затем выберите **Закрыть**.  
  
5.  На **Панели диаграмм**выберите столбцы или другие элементы для включения в новое представление.  
  
6.  На **Панели критериев**выберите дополнительные условия сортировки или фильтрации для столбцов.  
  
7.  В меню **Файл** выберите команду **Сохранить***имя представления*.  
  
8.  В диалоговом окне **Выбор имени** введите имя нового представления и щелкните **ОК**.  
  
     Дополнительные сведения о конструкторе запросов и представлений см. в статье [Инструменты конструктора запросов и представлений (визуальные инструменты для баз данных)](http://msdn.microsoft.com/library/12e4b5a5-b793-4b6c-a0e5-c450c49bf26f).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-create-a-view"></a>Создание представления  
  
1.  В **обозревателе объектов** подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
    GO  
    -- Query the view  
    SELECT FirstName, LastName, HireDate  
    FROM HumanResources.EmployeeHireDate  
    ORDER BY LastName;  
  
    ```  
  
 Дополнительные сведения см. в статье [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md).  
  
  
