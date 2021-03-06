---
title: Сопоставление исходной и целевой типы данных (AccessToSQL) | Документы Microsoft
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
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: af10741f0041525b058341f398b86c5e62f7a7e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>Сопоставление исходной и целевой типы данных (AccessToSQL)
Типы доступа к базе данных отличаются от [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] типы базы данных. При преобразовании объекты базы данных Access для [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] объектов, необходимо указать способ сопоставления типов данных доступ к [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Вы можете принять сопоставления типов данных по умолчанию или можно настроить сопоставления, как показано в следующих процедурах.  
  
## <a name="default-mappings"></a>Сопоставления по умолчанию  
SSMA имеет набор по умолчанию сопоставлений типов данных. Список сопоставлений по умолчанию см. в разделе [(сопоставление типов) параметры проекта](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655).  
  
## <a name="customizing-data-type-mappings"></a>Настройка сопоставления типов данных  
С помощью **параметры проекта** диалоговое окно, можно настроить сопоставление типов для всех баз данных и объектов базы данных в проекте. Сопоставления типов для проекта применяются ко всем базам данных и объектов базы данных, у которых нет сопоставления пользовательских типов.  
  
Также можно настроить сопоставление типов данных на уровне базы данных или таблицы.  
  
Ниже показано, как при сопоставлении типов данных на уровне объекта базы данных, базы данных или проекта.  
  
**При сопоставлении типов данных**  
  
1.  Чтобы настроить сопоставление типов данных для всего проекта, откройте **параметры проекта** диалоговое окно:  
  
    1.  На **средства** последовательно выберите пункты **параметры проекта**.  
  
    2.  В левой области выберите **сопоставление типов**.  
  
        Тип диаграммы сопоставления и кнопки отображаются в правой области.  
  
    Или, чтобы настроить сопоставление типов данных на уровне базы данных или таблицы, выберите таблицы или базы данных на панели обозревателя метаданных доступа:  
  
    1.  В панели обозревателя метаданных доступа разверните **доступа к метабазе**и разверните **баз данных**.  
  
    2.  Выберите базы данных или таблицы, для которого требуется настроить сопоставление типов данных.  
  
    3.  В области справа щелкните **сопоставление типов**.  
  
2.  Чтобы добавить новое сопоставление, выполните следующие действия.  
  
    1.  В области типа сопоставления выберите **добавить**.  
  
    2.  В **новое сопоставление типов** диалогового **тип источника**, выберите тип данных Microsoft Access для сопоставления.  
  
    3.  Если тип требует задания длины, укажите длин данных минимальное и максимальное для сопоставления, выбрав **из** и **для** флажки, а затем ввод значения.  
  
        Это позволяет настроить сопоставление данных для небольших и большего значения того же типа данных.  
  
    4.  В разделе **целевой тип**, выберите целевой объект [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] тип данных.  
  
        Некоторые типы требуют длину целевого типа данных. Если это необходимо, введите новую длину данных в **заменить на** , а затем щелкните **ОК**.  
  
3.  Чтобы изменить сопоставление типа данных, выполните следующее:  
  
    1.  В области типа сопоставления выберите **изменить**.  
  
    2.  В **список сопоставления типа** диалогового **тип источника**, выберите тип данных Microsoft Access для сопоставления.  
  
    3.  Если тип требует задания длины, укажите длин данных минимальное и максимальное для сопоставления, выбрав **из** и **для** флажки, а затем ввод значения.  
  
        Это позволяет настроить сопоставление данных для небольших и большего значения того же типа данных.  
  
    4.  В разделе **целевой тип**, выберите целевой объект [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] тип данных.  
  
        Некоторые типы требуют длину целевого типа данных. Если это необходимо, введите новую длину данных в **заменить на** , а затем щелкните **ОК**.  
  
4.  Чтобы удалить сопоставление типов данных, выполните следующие действия.  
  
    1.  В области типа сопоставления выберите строку в список сопоставления типа, который содержит сопоставление типов данных, которые вы хотите удалить.  
  
    2.  Щелкните **Удалить**.  
  
## <a name="next-steps"></a>Следующие шаги  
Следующим шагом в процессе миграции является [преобразования объектов базы данных access объекты SQL Server](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>См. также  
[Миграция баз данных Access в SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
