---
title: Дескрипторы среды | Документы Microsoft
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
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a84e7d5939eb4d4c57b7f59db6d719627cf4be3b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="environment-handles"></a>Дескрипторы среды
*Среды* является глобальный контекст, в котором для доступа к данным, а связанные со средой — все сведения, который является глобальным по своей природе, такие как:  
  
-   Состояния среды  
  
-   Текущий уровень среды диагностики  
  
-   Дескрипторы соединений, выделенные в данный момент в среде  
  
-   Текущие параметры всех атрибутов среды  
  
 В это часть кода, который реализует ODBC (диспетчера драйверов или драйвер) дескриптор среды определяет структуры, содержащие эти сведения.  
  
 Дескрипторы среды не часто используются в приложениях ODBC. Всегда используются в вызовах **SQLDataSources** и **SQLDrivers** и иногда используется для вызова **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**, и **SQLGetDiagRec**.  
  
 Каждый фрагмент кода, реализующего ODBC (диспетчера драйверов или драйвер) содержит один или несколько дескрипторов среды. Например диспетчер драйверов сохраняются дескриптор отдельную среду для каждого приложения, подключенные к нему. Дескрипторы среды выделяются с **SQLAllocHandle** и освобождается с помощью **SQLFreeHandle**.
