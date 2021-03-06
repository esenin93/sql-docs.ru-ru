---
title: Аргументы для внешних средств | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64ce1d99c60eb8863c0e149b8560d99d5d16ffeb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="arguments-for-external-tools"></a>Аргументы для внешних средств
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Аргументы — это переменные, с помощью которых среда Studio передает параметры внешним средствам, запускаемым через меню **Сервис** . Внешние средства, например «Блокнот», можно добавить в меню **Сервис** с помощью диалогового окна **Внешние средства** .  
  
В следующей таблице приведены возможные аргументы для внешних программ.  
  
|Имя|Аргумент|Description|  
|--------|------------|---------------|  
|**Путь элемента**|$(ItemPath)|Полное имя файла текущего источника (определяемое как диск + путь + имя файла); пусто, если окно источника не активно.|  
|**Каталог элемента**|$(ItemDir)|Каталог текущего источника (определяемое как диск + путь); пусто, если окно источника не активно.|  
|**Имя файла элемента**|$(ItemFilename)|Имя текущего файла источника (определяемое как имя файла); пусто, если окно источника не активно.|  
|**Расширение элемента**|$(ItemExt)|Расширение имени текущего файла источника.|  
|**Текущая строка***|$(CurLine)|Строка текущего положения курсора в окне редактора.|  
|**Текущий столбец***|$(CurCol)|Столбец текущего положения курсора в окне редактора.|  
|**Текущий текст***|$(CurText)|Текущий текст (слово под курсором или выбранная область, расположенная на одной строке, если она выбрана).|  
|**Путь цели**|$(TargetPath)|Полное имя целевого файла (определяется как диск + путь + имя файла).|  
|**Целевой каталог**|$(TargetDir)|Каталог целевого объекта.|  
|**Имя цели**|$(TargetName)|Имя целевого файла.|  
|**Расширение цели**|$(TargetExt)|Расширение имени целевого файла.|  
|**Каталог проекта**|$(ProjDir)|Каталог текущего проекта (определяется как диск + путь).|  
|**Имя файла проекта**|$(ProjFileName)|Полное имя файла текущего проекта (определяется как диск + путь + имя файла).|  
|**Каталог решения**|$(SolutionDir)|Каталог текущего решения (определяется как диск + путь).|  
|**Имя файла решения**|$(SolutionFileName)|Имя файла текущего решения (определяется как диск + путь + имя файла).|  
  
* Текущая строка, текущий столбец или текущий текст определяются по положению курсора в редакторе текста, которое отображается в строке состояния.  
  
## <a name="see-also"></a>См. также:  
[Диалоговое окно «Внешние средства»](../ssms/external-tools-dialog-box.md)  
[Общие элементы интерфейса пользователя](../ssms/general-user-interface-elements.md)  
  
