---
title: Оптимизировать динамические свойства (ADO) | Документы Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3512f1a63ae92ce75990f63caabf80a83099c149
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="optimize-property-dynamic-ado"></a>Оптимизировать динамические свойства (ADO)
Указывает, создан ли индекс на [поля](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Параметры и возвращаемые значения  
 Возвращает или задает **логическое** значение, указывающее, должен ли быть создан индекс.  
  
## <a name="remarks"></a>Замечания  
 Индекс может повысить эффективность операций поиска или отсортировать значения в [записей](../../../ado/reference/ado-api/recordset-object-ado.md). Индекс является внутренним для ADO; нельзя явно доступ или использовать его в приложении.  
  
 Чтобы создать указатель на поле, установите **оптимизировать** свойства **True**. Чтобы удалить индекс, присвойте этому свойству значение **False**.  
  
 **Оптимизация** динамическое свойство добавляется к [поле](../../../ado/reference/ado-api/field-object.md) объекта [свойства](../../../ado/reference/ado-api/properties-collection-ado.md) коллекции при [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) свойству **adUseClient**.  
  
## <a name="usage"></a>Использование  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>Объект применения  
 [Объект Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>См. также  
 [Оптимизация примера свойства (Visual Basic)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Оптимизация примера свойства (VC ++)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Свойства фильтра](../../../ado/reference/ado-api/filter-property.md)   
 [Find-метод (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Свойство Sort](../../../ado/reference/ado-api/sort-property.md)
