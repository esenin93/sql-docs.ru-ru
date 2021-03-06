---
title: Ascendants (многомерные Выражения) | Документы Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: df35665a82149bd133e4116d97cb739d70865ac7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="ascendants-mdx"></a>Ascendants (многомерные выражения)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Возвращает набор родителей указанного элемента, включая его самого.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Аргументы  
 *Member_Expression.*  
 Допустимое многомерное выражение, возвращающее элемент.  
  
## <a name="remarks"></a>Замечания  
 **Предки** функция возвращает всех предков элемента из элемента до верхнего элемента в иерархии; в частности, он выполняет обход в обратном порядке иерархии указанного элемента и затем возвращает все родительские элементы связан с элементом, включая его самого, в наборе. Это отличается от [предка](../mdx/ancestor-mdx.md) функции, которая возвращает указанный родительский элемент или предок указанного уровня.  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращается количество заказов посредников для `[Sales Territory].[Northwest]` элемента и всех его предков этого члена из **Adventure Works** куба. **Предки** функция создает набор, который содержит `[Sales Territory].[Northwest]` и всех его предков по оси ROWS.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по функциям многомерных Выражений &#40;Многомерные Выражения&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
