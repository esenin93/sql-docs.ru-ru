---
title: "Элемент BackupRemotePartitions (XML для Аналитики) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- BackupRemotePartitions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.backupremotepartitions
- http://schemas.microsoft.com/analysisservices/2003/engine#BackupRemotePartitions
- urn:schemas-microsoft-com:xml-analysis#BackupRemotePartitions
helpviewer_keywords:
- BackupRemotePartitions element
ms.assetid: bd68bcf9-b324-4fa8-b6e5-1f5531f9992c
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 477ecda306edfb1f51befa41ad19ebd1b6382865
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="backupremotepartitions-element-xmla"></a>Элемент BackupRemotePartitions (XML для аналитики)
  Определяет, является ли родительский [резервного копирования](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) команда создает резервную копию удаленных секций, связанных с объектом.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|Boolean|  
|Значение по умолчанию|False|  
|Количество элементов|0—1: необязательный элемент, который может появляться только один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[Резервное копирование](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Замечания  
 Если элемент **BackupRemotePartitions** имеет значение **True**, в команду **Locations** должен включаться элемент **Location** , содержащий один или несколько элементов **Backup** , иначе возникает ошибка. Дополнительные сведения о резервном копировании и восстановлении удаленных секций см. в разделе [резервное копирование, восстановление и синхронизация баз данных &#40; XML для Аналитики &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>См. также:  
 [Элемент Locations &#40; XML для Аналитики &#41;](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)   
 [Элемент Location &#40; XML для Аналитики &#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [Свойства &#40; XML для Аналитики &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  