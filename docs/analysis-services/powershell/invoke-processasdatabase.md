---
title: Вызов ProcessASDatabase | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 44a5654207e84f3488c66b3bc9cfab4778b51acb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="invoke-processasdatabase"></a>Invoke-ProcessASDatabase
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Выполняет операцию **Process** для указанной базы данных **Database** с определенным типом **ProcessType** или **RefreshType** , в зависимости от базового типа метаданных.  
  
 Для баз данных с многомерными метаданными используйте **ProcessType** (сюда относятся табличные базы данных с уровнем совместимости 1050, 1100 и 1103).  
  
 Для табличных баз данных с уровнем совместимости 1200 или выше используйте **RefreshType** .  

>[!NOTE] 
>В этой статье может содержать устаревшие сведения и примеры. С помощью командлета Get-Help для последней версии.
  
## <a name="syntax"></a>Синтаксис  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-RefreshType] <RefreshType> {Full | ClearValues | Calculate |     DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-ProcessType] <ProcessType> {ProcessFull | ProcessAdd |     ProcessUpdate | ProcessIndexes | ProcessData | ProcessDefault | ProcessClear | ProcessStructure |     ProcessClearStructureOnly | ProcessScriptCache | ProcessRecalc | ProcessDefrag} [-Server <string>] [-Credential     <pscredential>] [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
## <a name="description"></a>Описание  
 Командлет **Invoke-ProcessASDatabase** обрабатывает базу данных до указанного вами уровня. Например, для табличных баз данных с уровнем совместимости 1200 присвоение значения **Full** параметру **RefreshType** приведет к замене существующих данных на новые.  
  
 Тип обработки (многомерный) или тип обновления (табличный) является обязательным и указывается до или после параметров базы данных и сервера:  
  
-   Дополнительные сведения о многомерных базах данных см. в разделе [Настройка параметров обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
-   Дополнительные сведения о табличных базах данных см. в разделе [Обработка базы данных, таблицы или секции (службы Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="parameters"></a>Параметры  
  
### <a name="-databasename-string"></a>Имя базы данных - \<строка >  
 Указывает тип обрабатываемой базы данных (табличная или многомерная).  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|0|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-Сервер\<Microsoft.AnalysisSevices.Server >  
 Если для своего контекста вы не используете каталог поставщика **SQLAS** , дополнительно указывает экземпляр сервера, к которому нужно подключиться.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?|именованный|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 Указывает тип обработки для табличной базы данных.  Допустимые значения: Full, ClearValues, Calculate, DataOnly, Automatic, Add и Defragment. Описания и инструкции см. в разделе [Обработка базы данных, таблицы или секции (службы Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|1|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>Тип процесса - \<Microsoft.AnalysisServices.ProcessType >  
 Указывает тип обработки для многомерной или табличной базы данных с уровнями совместимости 1050–1103. Допустимые значения: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc и другие. Описания и инструкции см. в разделе [Настройка параметров обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|1|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-credential"></a>-Credential  
 Если этот параметр задан, указанные имя пользователя и пароль будут использоваться для подключения к экземпляру служб Analysis Services. Если учетные данные не будут указаны, будут использованы учетные данные по умолчанию для пользователя Windows, который запускает этот сценарий.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?|именованный|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
## <a name="-whatif"></a>-Whatif  
 Укажите этот параметр, чтобы получить сведения о результатах операции до ее выполнения.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?|именованный|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
## <a name="-confirm"></a>-Confirm  
 Укажите этот параметр, чтобы интерактивно подтвердить выполнение операции (диалоговое окно с кнопками "Да" и "Нет") до ее выполнения.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?||  
|Значение по умолчанию||  
|Принимать входные данные конвейера?||  
|Принимать символы-шаблоны?|false|  
  
## <a name="example-1-sqlas-provider"></a>Пример 1 (поставщик SQLAS)  
 В этом примере с помощью поставщика **SQLAS** задается контекст для списка баз данных в экземпляре по умолчанию.  Сформировав список содержимого каталога баз данных, вы увидите все базы данных вместе с их состоянием обработки и режимами чтения и записи.  
  
 Запустите командлет **Invoke ProcessASDatabase** , указав только имя базы данных.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server > cd sqlas\ssas-srv-01\default\databases  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> dir  
. . . .  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> Invoke-ProcessASDatabase "adventureworks"  
  
```  
  
 В зависимости от типа базы данных вам будет предложено выбрать параметр **RefreshType** или **ProcessType**.  
  
 О завершении обработки свидетельствует наличие объекта влияния в возвращаемом значении: Microsoft.AnalysisServices.Tabular.ObjectImpact.  
  
 Обратите внимание, что иногда сведения о состоянии объекта кэшируются, поэтому если вывести содержимое каталога после успешного завершения обработки, состояние базы данных сохранит исходный дескриптор "не обработано". Это вводит в заблуждение, так как фактически после возврата объекта ObjectImpact база данных является обработанной.  
  
 Чтобы убедиться в успешном завершении обработки, откройте страницу свойств базы данных в среде Management Studio, запустите новый сеанс или верните состояние обработки из объекта базы данных (через [Microsoft.AnalysisServices.ProcessableMajorObject.LastProcessed](https://msdn.microsoft.com/library/microsoft.analysisservices.processablemajorobject.lastprocessed.aspx)).  
  
## <a name="example-2"></a>Пример 2  
 В этом примере показана та же операция, но только с помощью командлета, без поставщика. Чтобы указать сервер и тип обработки, необходимы дополнительные параметры.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server >  Invoke-ProcessASDatabase -databasename "AdventureWorks" -server '\\server-name\instancename' –ProcessType "ProcessFull"  
  
```  
  
  
  
