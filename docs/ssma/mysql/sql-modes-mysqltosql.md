---
title: "Режимы SQL (MySQLToSQL) | Документы Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 175e135f99f8ed96754ff255cbad7f32cc202479
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="sql-modes-mysqltosql"></a>Режимы SQL (MySQLToSQL)
SSMA для MySQL могут работать в разных режимах SQL, а также можно применить эти режимы по-разному для разных клиентов.  
  
Режимы определяют синтаксис SQL, MySQL должен поддерживать и проверяет тип проверки данных, его необходимо выполнить. Это упрощает использование MySQL в различных средах и MySQL с SQL Server.  
  
## <a name="sql-modes-grid"></a>Сетка режимы SQL:  
  
-   Сетка режимы SQL на корневом уровне содержит следующие столбцы: **имя режима SQL**, **загрузить режимах SQL**, и **действующие режимах SQL**.  
  
-   Сетка режимы SQL в баз данных категории, базы данных, таблицы категории, категории операторов, категории представлений, таблиц, представлений, функции, процедуры, определяемой пользователем функции и уровень события объекта содержит следующие столбцы: **имя режима SQL**, **наследуется режимах SQL**, и **действующие режимах SQL**.  
  
-   Сетка режимы SQL на уровне хранимой процедуры, функции, хранимые и триггер содержит следующие столбцы: **имя режима SQL**, **исходного режимах SQL**, и **действующие режимах SQL**.  
  
> [!NOTE]  
> Режимы группы будут отображаться в полужирным шрифтом, в столбце «Имя режима SQL».  
  
## <a name="loaded-sql-modes"></a>Загрузить SQL режимы  
Далее приводятся режимы SQL, которые ЗАДАЮТСЯ на уровне сеанса или корневой. Нельзя изменять режимы SQL, после загрузки в целевую базу данных или изменить.  
  
## <a name="inherited-sql-modes"></a>Режимы наследуемые SQL  
Далее приводятся режимы SQL, которые унаследованы от соответствующего родительского узла.  
  
Эти режимы SQL за исключением категории функций, Procedures, категория, категория событий и триггеры, присутствуют на всех уровнях (объект базы данных, таблицы категории, категории операторов, представления категории, таблицы, представления, функции, процедуры, определяемой пользователем функции и события).  
  
> [!NOTE]  
> Выбрав **наследовать от родителя** флажок, наследуется режимах SQL может быть унаследовано от родительского узла. По умолчанию этот флажок установлен.  
  
## <a name="original-sql-modes"></a>Режимы исходного SQL  
Это режимах SQL присутствует на уровнях функции, процедуры и триггеров.  
  
> [!NOTE]  
> Выбрав **используйте исходный** проверьте поле режимы SQL, которые изначально использовались в соответствующей функции или процедуры или триггера, можно использовать. По умолчанию этот флажок установлен.  
  
## <a name="effective-sql-modes"></a>Режимы эффективных SQL  
Действующие режимах SQL могут определяться на различных уровнях следующим образом:  
  
-   **На уровне сеанса.**  
  
    1.  Всех загружен SQL режимов может быть вызван, «Действующие режимах SQL».  
  
    2.  На этом уровне действующие режимах SQL может быть напрямую и явно изменен.  
  
    3.  Действующий режим SQL, которое задается явным образом не отражается в виде загружен режим SQL и наконец применяется к объекту.  
  
-   **На уровне функции или процедуры или триггера.**  
  
    1.  Исходный режимах SQL может вызываться, «Действующие режимах SQL».  
  
    2.  На этом уровне действующий режим SQL явно изменить только если **используйте исходный** флажок снят.  
  
    3.  Действующий режим SQL, которое задается явным образом не отражаются в исходном режиме SQL и наконец применяется к объекту.  
  
-   **На узлы, отличные от функции или процедуры или триггера, уровень:**  
  
    1.  Все наследуемые SQL режимов может быть вызван, «Действующие режимах SQL».  
  
    2.  На этом уровне действующий режим SQL явно изменить только если **наследовать от родителя** флажок снят.  
  
    3.  Действующий режим SQL, которое задается явным образом не отражается в виде наследуется режим SQL и наконец применяется к объекту.  
  
