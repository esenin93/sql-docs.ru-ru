---
title: Редактор разрешения ссылок на столбцы | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3d56af3ba4eb3d8facd0d9f57a01fe36f9cdcbfd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="resolve-column-reference-editor"></a>Редактор разрешения ссылок на столбцы
  Если входной путь отсоединен или если в нем присутствуют несопоставленные столбцы, напротив соответствующего пути данных будет отображен значок ошибки. Чтобы упростить разрешение ошибок ссылок на столбцы, редактор разрешения ссылок позволяет связывать несопоставленные входные и выходные столбцы для всех путей в дереве выполнения. Редактор разрешения ссылок также выделяет пути, чтобы указать, какие из них разрешаются в данный момент.  
  
> [!NOTE]  
>  Можно изменить компонент даже в случае, если путь входа отключен.  
  
 Если после того, как все ссылки на столбцы были разрешены, если ошибок пути данных больше не осталось, значки ошибок не будут отображаться напротив путей данных.  
  
## <a name="options"></a>Параметры  
 **Несопоставленные выходные столбцы (источник)**    
 Столбцы из восходящего пути, которые в данный момент не сопоставлены  
  
**Сопоставленные столбцы (источник)**    
 Столбцы из восходящего пути, которые сопоставлены со столбцами из нисходящего пути  
  
**Сопоставленные столбцы (назначение)**    
 Столбцы из восходящего пути, которые сопоставлены со столбцами из нисходящего пути  
  
**Несопоставленные входные столбцы (назначение)**    
 Столбцы из нисходящего пути, которые в данный момент не сопоставлены  
  
**Удалить несопоставленные входные столбцы**  
 Установите флажок «Удалить несопоставленные входные столбцы», чтобы игнорировать несопоставленные столбцы в назначении пути данных. При нажатии кнопки «Просмотр изменений» будет отображен список изменений, которые будут внесены при нажатии кнопки «ОК».  
  
  
