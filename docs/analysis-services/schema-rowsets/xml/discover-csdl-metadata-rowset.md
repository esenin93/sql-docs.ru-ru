---
title: Набор строк DISCOVER_CSDL_METADATA | Документы Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca80c243a7ee9c001f079f21908f803a99b75e1f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="discovercsdlmetadata-rowset"></a>Набор строк DISCOVER_CSDL_METADATA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Возвращает сведения о модели данных служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] (табличной или многомерной), предоставляя определение модели в формате CSDLBI (язык CSDL с заметками бизнес-аналитики). CSDLBI основан на языке CSDL, схеме XML, используемой платформой Entity Data Framework, необходимой для обеспечения коммуникации между сервером [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] и клиентом [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] . Заметки бизнес-аналитики (BI) предоставляют дополнительные метаданные о табличных моделях и их объектах. Дополнительные сведения о табличных моделях данных см. в разделе [Заметки языка CSDL для бизнес-аналитики (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
 Контекст безопасности команды влияет на возвращаемый набор строк. Для получения определения CSDL с сервера необходимы разрешения на чтение в экземпляре служб Analysis Services.  
  
 Идентификатор языка клиента, который отправляет запрос набора строк, вводится в строку подключения для команды и влияет на язык, который отображается в нескольких свойствах, возвращаемых в составе набора строк.  Сведения о свойствах и описании, которые могут зависеть от идентификатора языка, содержатся в разделе «Замечания».  
  
## <a name="rowset-columns"></a>Столбцы наборов строк  
 Набор строк **DISCOVER_CSDL_METADATA** содержит следующие столбцы.  
  
|**Имя столбца**|**Индикатор типа**|**Ограничение**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Да|Задает имя базы данных, для которой запрошено описание CSDLBI. Если отсутствует, используется текущая база данных.<br /><br /> Это ограничение необходимо для всех типов моделей.|  
|**PERSPECTIVE_ID**|**DBTYPE_WSTR**|Да|Задает идентификатор перспективы, определенной в модели, заданной с помощью CATALOG_NAME.<br /><br /> Необязательное ограничение. Все типы моделей.|  
|**PERSPECTIVE_NAME**|**DBTYPE_WSTR**|Да|Задает имя перспективы, определенной в модели, заданной с помощью CATALOG_NAME.<br /><br /> Это ограничение необходимо, когда табличная модель содержит перспективы или в многомерное решение входит несколько кубов или перспектив.|  
|**МЕТАДАННЫЕ**|**DBTYPE_WSTR**|Нет|Строка, содержащая XML-определение источника данных и его свойств в соответствии со CSDLBI-схемой.|  
|**CUBE_ID**|**DBTYPE_WSTR**|Да|Идентификатор строки.<br /><br /> Это ограничение необязательно для многомерных баз данных. Если доступно несколько кубов и ограничение не указано, то возвращается куб по умолчанию.|  
  
## <a name="remarks"></a>Замечания  
 К DISCOVER_CSDL_METADATA предъявляются следующие требования.  
  
-   Если база данных не указана с использованием ограничения CATALOG_NAME, запрос DISCOVER завершится неудачей.  
  
-   Для табличной модели необходим идентификатор перспективы, если в модели более одной перспективы.  
  
-   Для многомерных моделей необходимы имя каталога и имя куба (перспективы).  
  
-   Если перспектива представлена в качестве ограничения, то возвращается тот же набор строк CSDL, что и для модели. Однако все объекты, которые имеются в модели, но не входят в указанную перспективу, помечаются как **Hidden** = True.  
  
-   Для таблиц и столбцов запрос DISCOVER всегда выдает значение из измерения куба. Если не задано свойство измерения куба, то запрос возвращает значение из этого измерения.  
  
-   Запрос DISCOVER не может возвращать измерения или вычисляемые столбцы, содержащие семантические ошибки.  
  
-   Запрос DISCOVER не возвратит никаких сведений для объектов, которые не имеют значений свойств. Запрос DISCOVER также не возвращает значения для атрибутов, которые используют значение по умолчанию.  
  
 Строка XML, которая возвращается в наборе строк, может включать следующие свойства для конкретного языка или значения. Например, если выполнен запрос набора строк от клиента, имеющего идентификатор LCID 0403 (каталонский испанский), свойство возвратит следующие значения, необходимые для языка «каталонский испанский». Если переводы недоступны на сервере, возвращается строка для языка сервера по умолчанию.  
  
-   Заголовок  
  
-   Квалификатор  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>Пример  
 **Табличные**  
  
 Следующий запрос XMLA для аналитики возвращает представление языка CSDL образца табличной модели AdventureWorks 2012. Каждое табличное решение может содержать только одну модель, поэтому ограничение PERSPECTIVE_NAME можно оставить пустым. Однако эта модель содержит несколько перспектив.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>Пример  
 **Многомерные**  
  
 Следующий запрос XML для аналитики возвращает представления CSDLBI куба операций Contoso. Ограничение VERSION необходимо для запросов к многомерной базе данных. База данных Contoso Retail содержит два куба; таким образом, на куб Operations идет ссылка с помощью ограничения PERSPECTIVE_NAME.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Использование ADOMD.NET для возврата набора строк  
 Если для получения метаданных используется ADOMD.NET и набор строк схемы, то для ссылки на объект набора строк схемы в методе GetSchemaDataSet вы можете использовать идентификатор GUID или строку. Дополнительные сведения см. в статье [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 В следующей таблице указываются значения строки и идентификатора GUID, определяющие этот набор строк.  
  
|Аргумент|Значение|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>См. также:  
 [Службы Analysis Services наборы строк схемы](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Заметки языка CSDL для бизнес-аналитики & #40; CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
