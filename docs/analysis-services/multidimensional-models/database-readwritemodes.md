---
title: Режимы ReadWriteModes базы данных | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ec2aebbb202aadf69ccb9ab2c214d878aa0d9d9e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="database-readwritemodes"></a>Режимы ReadWriteModes базы данных
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Часто возникает ситуация, когда администратору базы данных (dba) служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] необходимо переключить базу данных из режима для чтения и записи в режим только для чтения или наоборот. Обычно это продиктовано производственной необходимостью, например, чтобы обеспечить общий доступ нескольким серверам к папке базы данных для масштабирования решения и повышения производительности. В такой ситуации свойство **ReadWriteMode** базы данных позволяет администратору базы данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] легко изменять режим работы базы данных.  
  
## <a name="readwritemode-database-property"></a>Свойство ReadWriteMode базы данных  
 Свойство базы данных **ReadWriteMode** указывает, в каком режиме работает база данных — чтение и запись или только чтение. Эти значения являются единственными допустимыми для данного свойства. Пока база данных находится в режиме только для чтения, к ней не могут применяться операции изменения или обновления. В режиме для чтения и записи в базе данных выполняются операции изменения и обновления. Свойство **ReadWriteMode** базы данных определено как свойство только для чтения. Его можно задать только с помощью команды **Attach** .  
  
 Если база данных находится в режиме только для чтения, определенные ограничения влияют на обычный набор допустимых операций с базой данных. В следующей таблице приведены эти ограниченные операции.  
  
|Режим «только для чтения»|Ограничения на операции|  
|-------------------|---------------------------|  
|Команды XML/A<br /><br /> <br /><br /> Примечание. При выполнении любой из следующих команд возникает ошибка.|**Создание**<br /><br /> **Alter**<br /><br /> **Delete**<br /><br /> **Процесс**<br /><br /> **MergePartitions**<br /><br /> **DesignAggregations**<br /><br /> **CommitTransaction**<br /><br /> **Восстановить**<br /><br /> **Synchronize**<br /><br /> **Insert**<br /><br /> **Update**<br /><br /> **Drop**<br /><br /> <br /><br /> Примечание. Обратная запись в ячейку для базы данных в режиме только для чтения является допустимой, однако нельзя зафиксировать изменения.|  
|Инструкции многомерных выражений<br /><br /> <br /><br /> Примечание. При выполнении любой из следующих инструкций происходит ошибка.|**COMMIT TRAN**<br /><br /> **CREATE SESSION CUBE**<br /><br /> **ALTER CUBE**<br /><br /> **ALTER DIMENSION**<br /><br /> **CREATE DIMENSION MEMBER**<br /><br /> **DROP DIMENSION MEMBER**<br /><br /> **ALTER DIMENSION**<br /><br /> <br /><br /> Примечание. Пользователи Excel не могут использовать функцию группирования в сводных таблицах, так как внутренне эта функция реализована с помощью команд **CREATE SESSION CUBE** .|  
|Инструкции расширений интеллектуального анализа данных<br /><br /> <br /><br /> Примечание. При выполнении любой из следующих инструкций происходит ошибка.|**CREATE [SESSION] MINING STRUCTURE**<br /><br /> **ALTER MINING STRUCTURE**<br /><br /> **DROP MINING STRUCTURE**<br /><br /> **CREATE [SESSION] MINING MODEL**<br /><br /> **DROP MINING MODEL**<br /><br /> **IMPORT**<br /><br /> **SELECT INTO**<br /><br /> **INSERT**<br /><br /> **UPDATE**<br /><br /> **DELETE**|  
|Фоновые операции|Отключены все фоновые операции, которые могут привести к изменению базы данных. В их число входят отложенная обработка и упреждающее кэширование.|  
  
## <a name="readwritemode-usage"></a>Использование свойства ReadWriteMode  
 Свойство **ReadWriteMode** базы данных должно использоваться как часть команды базы данных **Attach** . Команда **Attach** позволяет установить это свойство либо в значение **ReadWrite** , либо в значение **ReadOnly**. Значение свойства **ReadWriteMode** базы данных не может быть изменено напрямую, поскольку оно определено как свойство только для чтения. У вновь создаваемых баз данных свойство **ReadWriteMode** установлено в значение **ReadWrite**. База данных не может быть создана в режиме только для чтения.  
  
 Для переключения свойства базы данных **ReadWriteMode** между значениями **ReadWrite** и **ReadOnly**необходимо использовать последовательность команд **Detach/Attach** .  
  
 Ни одна из операций базы данных, за исключением **Attach**, не изменяет значение свойства базы данных **ReadWriteMode** . В частности, операции типа **Alter**, **Backup**, **Restore**и **Synchronize** не изменяют значение свойства **ReadWriteMode** .  
  
> [!NOTE]  
>  Локальные кубы могут быть созданы только из базы данных, находящейся в режиме только для чтения.  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Присоединение и отсоединение баз данных служб Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Перемещение базы данных служб Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Элемент detach](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Элемент Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  
