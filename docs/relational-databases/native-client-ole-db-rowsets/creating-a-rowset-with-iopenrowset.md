---
title: Создание набора строк с IOpenRowset | Документы Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5865b7bd961f1969f53b2e713c7f543d502de982
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Создание набора строк с помощью интерфейса IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Поддерживает поставщик OLE DB для собственного клиента **IOpenRowset::OpenRowset** метод со следующими ограничениями:  
  
-   Базовая таблица или представление должен быть указан в базе данных (DBID) идентификатор структуру, в которой *pTableID* указывает параметр.  
  
-   DBID *eKind* член должен указывать DBKIND_NAME.  
  
-   DBID *uName* элемента необходимо указать имя существующей базовой таблицы или представления, как строку символов Юникода.  
  
-   *PIndexID* параметр **OpenRowset** должен иметь значение NULL.  
  
 Результирующий набор **IOpenRowset::OpenRowset** содержит единственный набор строк. Результирующие наборы, содержащие единственный набор строк может поддерживаться [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] курсоров. Благодаря поддержке курсоров разработчик может использовать механизмы параллелизма [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>См. также:  
 [Наборы строк](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
