---
title: 'Коллекции (Visual C++ синтаксис индекс с #import) | Документы Microsoft'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92ffc11b2011ff5f37aee25266d0f229b1dfd617
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="collections-visual-c-syntax-index-with-import"></a>Коллекции (Visual C++ синтаксис индекс с #import)
Полезно знать, что коллекции наследуют некоторые общие методы и свойства.  
  
 Наследовать все коллекции **число** свойство и **обновление** добавить метод и все коллекции **элемент** свойство. **Ошибки** добавляет в коллекцию **снимите** метод. **Параметры** наследует коллекции **Append** и **удалить** методы, пока **поля** коллекции добавляет **Append**, **удаление**, и **обновление** методы.  
  
## <a name="properties-collection"></a>Коллекция Properties  
  
### <a name="methods"></a>Методы  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Свойства  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>Коллекция ошибок  
  
### <a name="methods"></a>Методы  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Свойства  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Коллекция Parameters  
  
### <a name="methods"></a>Методы  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Свойства  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Коллекция Fields  
  
### <a name="methods"></a>Методы  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>Свойства  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>См. также  
 [Коллекция ошибок (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Коллекция Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Коллекция параметров (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Коллекция Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
