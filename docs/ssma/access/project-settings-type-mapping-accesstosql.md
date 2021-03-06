---
title: Параметры (сопоставление типов) проекта (AccessToSQL) | Документы Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 072d8aaf4582237cc60a3e3e6d76b02a86dc27c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-type-mapping-accesstosql"></a>Параметры (сопоставление типов) проекта (AccessToSQL)
Параметры сопоставления типов проекта позволяют задать сопоставления типов по умолчанию для проекта SSMA. Можно также указать сопоставления типов для отдельных объектов базы данных. Дополнительные сведения см. в разделе [сопоставление исходной и целевой типы данных](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
Сопоставление типов доступен в **параметры проекта** и **параметры проекта по умолчанию** диалоговые окна:  
  
-   Используйте **параметры проекта** диалоговое окно «», чтобы задать параметры конфигурации для текущего проекта. Чтобы открыть параметры сопоставления типов, в **средства** последовательно выберите пункты **параметры проекта**и нажмите кнопку **сопоставление типов** в левой области.  
  
-   Используйте **параметры проекта по умолчанию** диалоговое окно «», чтобы задать параметры конфигурации для всех проектов. Чтобы открыть параметры сопоставления типов, в **средства** последовательно выберите пункты **параметры проекта по умолчанию**, выберите тип проекта миграции, для которого требуются параметры для просмотра / изменилось с **миграции целевой версии** раскрывающийся список, а затем нажмите кнопку **сопоставление типов** в левой области.  
  
## <a name="options"></a>Параметры  
**Исходный тип**  
Необходимо сопоставить тип данных Access.  
  
**Тип целевого объекта**  
Целевой объект [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или тип данных SQL Azure для указанного типа данных Access.  
  
Следующая таблица показывает сопоставление по умолчанию между исходной и целевой типы данных.  
  
|Тип данных Microsoft Access|Тип данных SQL Server|  
|--------------------|------------------------|  
|**двоичные [\*... \*]**|**varbinary [\*]**|  
|**boolean**|**бит**|  
|**byte**|**tinyint**|  
|**Валюта**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**Идентификатор GUID**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**Long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**MEMO**|**nvarchar(max)**|  
|**MEMO** — для Access 97|**varchar(max)**|  
|**Один**|**real**|  
|**текст [\*... \*]**|**nvarchar [\*]**|  
|**текст [\*... \*]** — для Access 97|**varchar [\*]**|  
  
**Добавить**  
Щелкните, чтобы добавить в список сопоставления типа данных.  
  
**Правка**  
Щелкните, чтобы изменить тип данных в списке сопоставления.  
  
**Удалить**  
Щелкните, чтобы удалить сопоставление типов данных, выбранного из списка сопоставления.  
  
**По умолчанию**  
Щелкните, чтобы сбросить все сопоставления типов данных по умолчанию SSMA.  
  
## <a name="see-also"></a>См. также  
[Сопоставление исходного и целевого типов данных](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[Reference(Access) интерфейса пользователя](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
