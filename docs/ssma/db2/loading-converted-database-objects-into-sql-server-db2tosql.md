---
title: "Загрузка преобразованных объектов базы данных, в SQL Server (DB2ToSQL) | Документы Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f74e15c261041ae0a68152417955a81ed96994f8
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Загрузка преобразованных объектов базы данных, в SQL Server (DB2ToSQL)
После преобразования схемы DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], можно загрузить результирующие объекты базы данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Можно иметь SSMA создания объектов, или можно внести в скрипт объекты и запускать скрипты самостоятельно. Кроме того, SSMA позволяет заменить метаданные целевой фактическое содержимое [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] базы данных.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Выбор между синхронизации и сценарии  
Если вы хотите загрузить объекты преобразованную базу данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] без изменений, может иметь SSMA непосредственного создания или повторного создания объектов базы данных. Этот метод выполняется быстро и просто, но не разрешает настройку [!INCLUDE[tsql](../../includes/tsql_md.md)] код, который определяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] объектов, отличных от хранимых процедур.  
  
Если вы хотите изменить [!INCLUDE[tsql](../../includes/tsql_md.md)] , используемый для создания объектов, или если требуется больший контроль над создания объектов используйте SSMA для создания скриптов. Можно изменить эти сценарии, создайте каждый объект отдельно и даже использовать [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] агента для планирования, создания этих объектов.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>С помощью SSMA для синхронизации объектов с SQL Server  
Использование SSMA для создания [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] объекты базы данных, выберите объекты в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] обозреватель метаданных, а затем синхронизировать объекты с [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], как показано в следующей процедуре. По умолчанию, если объекты, уже существующие в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], и если метаданные SSMA новее, чем объект в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA приведут к изменению определения объектов в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Поведение по умолчанию можно изменить путем редактирования **параметры проекта**.  
  
> [!NOTE]  
> Можно выбрать существующий [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] объекты, которые не были преобразованы из баз данных DB2 базы данных. Тем не менее эти объекты не будет повторно или изменен с SSMA.  
  
**Для синхронизации объектов с SQL Server**  
  
1.  В [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] обозреватель метаданных разверните верхней [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] узел, а затем разверните **баз данных**.  
  
2.  Выберите объекты для обработки:  
  
    -   Чтобы синхронизировать всей базы данных, установите флажок рядом с именем базы данных.  
  
    -   Чтобы синхронизировать или исключить отдельные объекты или категории объектов, установите или снимите флажок рядом с объекту или папке.  
  
3.  После выбора объектов для обработки в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] обозреватель метаданных, щелкните правой кнопкой мыши **баз данных**, а затем нажмите кнопку **синхронизации с базой данных**.  
  
    Вы также можете синхронизировать отдельных объектов и категории объектов, щелкните правой кнопкой мыши объект или ее родительскую папку, выберите команду **синхронизации с базой данных**.  
  
    После этого будет отображаться SSMA **синхронизации с базой данных** диалоговое окно, в котором имеются две группы элементов. На левой стороне SSMA показывает выбранные объекты базы данных представлены в дереве. С правой стороны появится дерево, представляющее те же объекты в метаданных SSMA. Вы можете разверните дерево, щелкнув вправо или влево кнопку «+». Направление синхронизации отображается в столбце действий, который располагается между двумя деревьев.  
  
    Знак действие может находиться в трех состояниях:  
  
    -   Стрелка влево означает, что содержимое метаданные сохраняются в базе данных (по умолчанию).  
  
    -   Стрелка вправо означает, что содержимое базы данных перезапишет SSMA метаданных.  
  
    -   Знак перекрестного означает, что будет выполнено никаких действий.  
  
Щелкните знак «действие» для изменения состояния. Фактический синхронизация будет выполняться при нажатии кнопки **ОК** кнопки **синхронизации с базой данных** диалогового окна.  
  
## <a name="scripting-objects"></a>Создание скриптов для объектов  
Чтобы сохранить [!INCLUDE[tsql](../../includes/tsql_md.md)] определений объектов преобразованную базу данных, или для изменения определения объектов и самостоятельно выполнять скрипты можно сохранить ее определения объектов, [!INCLUDE[tsql](../../includes/tsql_md.md)] сценариев.  
  
**Для сохранения объектов в виде скриптов**  
  
1.  После выбора объектов для сохранения скрипта, щелкните правой кнопкой мыши **баз данных**, а затем нажмите кнопку **Сохранение скрипта**.  
  
    Можно также создать скрипт отдельных объектов и категории объектов, щелкнув правой кнопкой мыши объект или ее родительскую папку, выберите команду **Сохранение скрипта**.  
  
2.  В **Сохранить как** диалогового окна поле, перейдите в папку, в которой вы хотите сохранить скрипт, введите имя файла в **имя файла** поле, а затем [!INCLUDE[clickOK](../../includes/clickok_md.md)]. SSMA добавит .sql расширение имени файла.  
  
### <a name="modifying-scripts"></a>Изменение скриптов  
После сохранения [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] определения объектов, как один или несколько сценариев, можно использовать [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] для просмотра и изменения скриптов.  
  
**Изменение сценария**  
  
1.  На [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **файл** последовательно выберите пункты **откройте**, а затем нажмите кнопку **файл**.  
  
2.  В **откройте** диалоговое окно, выберите файл сценария и нажмите кнопку ОК.
  
3.  Измените файл скрипта с помощью редактора запросов.  
  
    Дополнительные сведения о редакторе запросов см. в разделе «Редактор удобных команд и компоненты» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
4.  Чтобы сохранить скрипт, в меню выберите команду файл **Сохранить**.  
  
### <a name="running-scripts"></a>Выполнение сценариев  
Можно запустить сценарий или отдельные инструкции в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Для выполнения сценария**  
  
1.  На [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **файл** последовательно выберите пункты **откройте**, а затем нажмите кнопку **файл**.  
  
2.  В **откройте** диалоговом окне выберите файл сценария, а затем[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Чтобы выполнить полный сценарий, нажмите клавишу **F5** ключа.  
  
4.  Чтобы выполнить набор инструкций, инструкции select, в окне редактора запросов и нажмите клавишу **F5** ключа.  
  
Дополнительные сведения о том, как использовать редактор запросов для выполнения скриптов см. в разделе «[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] запрос» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
Можно также выполнять скрипты из командной строки с помощью **sqlcmd** программы и от [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] агента. Дополнительные сведения о **sqlcmd**, содержатся в разделе «программа sqlcmd» [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации. Дополнительные сведения о [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] агента, в разделе «Автоматизация административных задач ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] агента)» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
## <a name="securing-objects-in-sql-server"></a>Защита объектов в SQL Server  
После загрузки объектов преобразованную базу данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], можно предоставлять и отменить разрешения на доступ к объектам. Рекомендуется сделать это перед переносом данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Для получения сведений о способах обеспечения безопасности объектов в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], в разделе «Безопасность вопросы для баз данных и базы данных приложений» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
## <a name="next-step"></a>Следующий шаг  
Следующим шагом в процессе миграции должно [переноса данных DB2 в SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>См. также:  
[Перенос данных DB2 в SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
