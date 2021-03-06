---
title: Использование инструкций в SQL | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac74ec1c202341d6de099d97e2b7c719c2f72d27
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-sql"></a>Использование инструкций в SQL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  При работе с данными в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] базы данных с помощью [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] и встроенных инструкций SQL, различные классы, которые можно использовать. Выбор используемого класса зависит от типа SQL-инструкции, которую необходимо выполнить.  
  
 Если инструкция SQL не содержит параметров IN, используйте [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) класса, но если он содержит параметры, используйте [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) класса.  
  
> [!NOTE]  
>  Если необходимо использовать инструкции SQL, которые содержит параметр IN и параметров OUT, необходимо реализовать ее в виде хранимой процедуры и вызвать ее с использованием [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) класса. Дополнительные сведения об использовании хранимых процедур см. в разделе [с помощью инструкций с помощью хранимых процедур](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
 В следующих разделах описаны различные сценарии для работы с данными в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] базы данных с помощью инструкций SQL.  
  
## <a name="in-this-section"></a>В этом разделе  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Использование инструкции SQL без параметров](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|Описывает порядок использования инструкций SQL, которые не содержат параметров.|  
|[Использование инструкции SQL с параметрами](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|Описывает порядок использования инструкций SQL, которые содержат параметры.|  
|[Использование инструкции SQL для изменения объектов баз данных ](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|Описывает порядок использования инструкций SQL для изменения объектов базы данных.|  
|[Использование инструкции SQL для изменения данных](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|Описывает порядок использования инструкций SQL для изменения данных в базе данных.|  
  
## <a name="see-also"></a>См. также  
 [Использование инструкций с драйвером JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
