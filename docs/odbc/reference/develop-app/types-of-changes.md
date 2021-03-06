---
title: Типы изменений | Документы Microsoft
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
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08e478da2080cf3d457d2c0a1ec5673e95ba2ea4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="types-of-changes"></a>Типы изменений
Трех типов изменений внесенных в ODBC 3. *x* (и любой версии ODBC). Каждый из них по-разному влияет на обратной совместимости и обрабатываются по-разному. Эти изменения описаны в следующей таблице.  
  
|Тип изменения|Описание|  
|--------------------|-----------------|  
|Новые возможности|Это функции, которые появились в ODBC 3. *x*, такие как привязка вне строки или дескрипторов. Они реализованы только в том случае, если приложение драйвера, а также диспетчера драйверов, имеют версии 3 *.x*, поэтому не выполняется, чтобы сделать эти обратной совместимости.|  
|Повторяющийся функции|Это функции, которые существуют в ODBC 2 *.x* а ODBC 3. *x* реализуется по-разному в каждой. Функции **SQLAllocHandle** и **SQLAllocStmt** приведен пример. Обратная совместимость выдает эти и другие повторяющиеся функции, главным образом обрабатываются сопоставления диспетчера драйверов.|  
|Изменения поведения|Это функции, которые обрабатываются по-разному в ODBC 2 *.x* а ODBC 3. *x*. Значения даты и времени **#define** приведен пример. Эти возможности обеспечиваются службами ODBC 3. *x* драйвер на основании атрибута параметры среды. (См. [изменения поведения](../../../odbc/reference/develop-app/behavioral-changes.md) подробнее.)|
