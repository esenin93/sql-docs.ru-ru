---
title: ИМПОРТ (ДАННЫХ DMX) | Документы Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ae93e70bb0e5672ada244064feb12750a96d4ffd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="import-dmx"></a>IMPORT (расширения интеллектуального анализа данных)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Загружает модель или структуру интеллектуального анализа данных из файла резервной копии служб Analysis Services (ABF) на сервер.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Аргументы  
 *Имя файла*  
 Строка с именем и расположением файла для импорта.  
  
## <a name="remarks"></a>Замечания  
 Если объекты не указаны, то загружается все содержимое DMB-файла. Если в DMB-файле содержится ссылка на несуществующую на сервере базу данных, то указанная база данных будет создана.  
  
 Только администратор базы данных или сервера имеет право экспортировать и импортировать объекты.  
  
## <a name="import-from-file-example"></a>Импорт из образца файла  
 В следующем примере выполняется импорт всего содержимого файла с моделью взаимосвязей и структурой на текущий сервер.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>См. также  
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции определения данных](../dmx/dmx-statements-data-definition.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции управления данными](../dmx/dmx-statements-data-manipulation.md)   
 [Расширения интеллектуального анализа данных & #40; расширений интеллектуального анализа данных & #41; Справка по инструкции](../dmx/data-mining-extensions-dmx-statements.md)   
 [ЭКСПОРТ &AMP;#40;РАСШИРЕНИЙ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ&AMP;#41;](../dmx/export-dmx.md)   
 [Экспорт и импорт объектов интеллектуального анализа данных](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
