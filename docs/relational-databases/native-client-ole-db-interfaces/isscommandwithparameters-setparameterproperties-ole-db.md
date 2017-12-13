---
title: "ISSCommandWithParameters::SetParameterProperties (OLE DB) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords: SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 458b169c41ebf5e209e178bd9db67b9e04503ff7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Задает свойства каждого параметра по порядковому номеру или задает массовые свойства параметра, указывая массив структур SSPARAMPROPS.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Аргументы  
 *cParams*[in]  
 Количество структур SSPARAMPROPS в *rgParamProperties* массива. Если это число равно нулю, **ISSCommandWithParameters::SetParameterProperties** приведет к удалению всех свойств, которые могли быть указаны для всех параметров в команде.  
  
 *rgParamProperties*[in]  
 Массив задаваемых структур SSPARAMPROPS.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **ISSCommandWithParameters::SetParameterProperties** метод возвращает те же коды ошибок, что и метод ядра OLE DB **ICommandProperties::SetProperties** метод.  
  
## <a name="remarks"></a>Замечания  
 Настройка свойств параметров с помощью этого метода разрешена для каждого параметра в отдельности по порядковому номеру или с помощью одного **ISSCommandWithParameters::SetParameterProperties** вызвать после структура SSPARAMPROPS строится из массива свойств.  
  
 **SetParameterInfo** метод должен вызываться перед вызовом метода **ISSCommandWithParameters::SetParameterProperties** метод. Вызов метода `SetParameterProperties(0, NULL)` очищает все указанные свойства параметра, тогда как вызов метода `SetParameterInfo(0,NULL,NULL)` очищает все сведения о параметре, в том числе все свойства, которые могут быть связаны с параметром.  
  
 Вызов **ISSCommandWithParameters::SetParameterProperties** для задания свойств для параметра, который не относится к типу DBTYPE_XML и DBTYPE_UDT, возвратит DB_E_ERRORSOCCURRED или DB_S_ERRORSOCCURRED и пометит  *dwStatus* все DBPROPs, содержащихся в структурах SSPARAMPROPS для этого параметра с DBPROPSTATUS_NOTSET поле. Чтобы обнаружить, к какому параметру относится DB_E_ERRORSOCCURRED или DB_S_ERRORSOCCURRED, необходимо пройти по массиву DBPROP каждого набора DBPROPSET, содержащегося в структуре SSPARAMPROPS.  
  
 Если **ISSCommandWithParameters::SetParameterProperties** вызывается, чтобы указать свойства параметров, сведения о которых имеют еще не был установлен с **SetParameterInfo**, поставщик возвращает E_ НЕПРЕДВИДЕННОЕ с следующее сообщение об ошибке:  
  
 Невозможно вызвать метод SetParameterProperties для указанных параметров, не вызывая предварительно метод SetParameterInfo. До задания свойств параметров необходимо задать сведения о параметрах.  
  
 Если вызов **ISSCommandWithParameters::SetParameterProperties** содержит некоторые параметры, когда сведения о параметре был набор и некоторые параметры, когда сведения о параметре не указан, то свойства dwStatus в DBPROPSET набора свойств SSPARAMPROPS вернутся со значением DBSTATUS_NOTSET.  
  
 Структура SSPARAMPROPS определена следующим образом.  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Усовершенствования в компоненте database engine, начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] разрешить ISSCommandWithParameters::SetParameterProperties получать более точные описания ожидаемых результатов. Эти более точные результаты могут отличаться от значения, возвращаемые методом ISSCommandWithParameters::SetParameterProperties в предыдущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в разделе [обнаружение метаданных](../../relational-databases/native-client/features/metadata-discovery.md).  
  
|Член|Description|  
|------------|-----------------|  
|*iOrdinal*|Порядковый номер переданного параметра.|  
|*cPropertySets*|Количество структур DBPROPSET в *rgPropertySets*.|  
|*rgPropertySets*|Указатель на буфер, в который будет возвращен массив структур DBPROPSET.|  
  
## <a name="see-also"></a>См. также:  
 [ISSCommandWithParameters &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  