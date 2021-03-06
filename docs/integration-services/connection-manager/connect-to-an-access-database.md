---
title: Соединение с базой данных Access | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Access [Integration Services]
- Access databases [Integration Services]
ms.assetid: 229fbd46-ef6a-4609-a4cc-d80d52c33cf1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c8e0811b894e96c4ac7b11ef377765aa6b56cdbf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-an-access-database"></a>Подключение к базе данных Access
  Чтобы привязать пакет служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] к источнику данных Microsoft Office Access, нужны диспетчер соединений OLE DB и поставщик данных. Выбор поставщика данных зависит от версии Access, в которой был создан источник данных.  
  
-   Для файлов в формате Access 2003 и более ранних версий пакету требуется поставщик [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB.  
  
-   Для формата Access 2007 пакету требуется поставщик данных OLE DB для компонента Microsoft Office 12.0 Access Database Engine.  
  
 Создать диспетчер соединений OLE DB и выбрать соответствующий поставщик данных можно либо из области «Диспетчеры соединений» в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , либо с помощью мастера импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  На 64-разрядном компьютере пакеты, которые соединяются с источниками данных [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access, должны запускаться в 32-разрядном режиме. Поставщик [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB для Jet и поставщик OLE DB для ядра СУБД Microsoft Office 12.0 Access доступны только в 32-разрядных версиях.  

## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Компоненты подключения для файлов Microsoft Excel и Access
  
Если компоненты подключения для файлов Microsoft Office еще не установлены, может потребоваться скачать их. Скачать последнюю версию компонентов подключения для файлов Access и Excel можно на следующей странице: [Распространяемый компонент ядра СУБД Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=54920).
  
Последняя версия компонентов позволяет открывать файлы, созданные в более ранних версиях Access.

Если на компьютере установлена 32-разрядная версия Office, нужно установить 32-разрядную версию компонентов, а также убедиться в том, что пакет запускается в 32-разрядном режиме.

Если у вас есть подписка на Office 365, нужно скачать распространяемый компонент ядра СУБД Access 2016, а не среду выполнения Microsoft Access 2016. При запуске установщика может появиться сообщение о том, что невозможно установить скачанные компоненты вместе с компонентами Office, полученными с помощью технологии "нажми и работай". Чтобы обойти это сообщение, запустите установку в тихом режиме. Для этого откройте окно командной строки и запустите скачанный EXE-файл с параметром `/quiet`. Пример:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="connecting-to-a-data-source-in-access-2003-or-earlier-format"></a>Соединение с источником данных в формате Access 2003 или более ранней версии  
  
### <a name="to-create-an-access-connection-manager-from-the-connection-managers-area"></a>Создание диспетчера соединений Access из области «Диспетчеры соединений»  
  
1.  Откройте пакет в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Щелкните правой кнопкой мыши в области **Диспетчеры соединений** , а затем выберите команду **Создать соединение OLE DB**.  
  
3.  В диалоговом окне **Настройка диспетчера соединений OLE DB** нажмите кнопку **Создать**.  
  
     Дополнительные сведения см. в разделе [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  В диалоговом окне **Диспетчер соединений** в поле **Поставщик**выберите поставщик **Microsoft Jet 4.0 OLE DB**, а затем настройте диспетчер соединений.  
  
### <a name="to-create-an-access-connection-from-the-sql-server-import-and-export-wizard"></a>Создание соединения Access с помощью мастера импорта и экспорта SQL Server  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]запустите мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  На странице **Выбор источника данных** выберите в поле **Источник данных**значение **Microsoft Access**, а затем настройте соединение Access.  
  
     При выборе в поле **Источник данных** значения **Microsoft Access**мастер автоматически создаст диспетчер соединений OLE DB с нужным поставщиком данных. Дополнительные сведения см. в разделе [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="connecting-to-a-data-source-in-access-2007-format"></a>Соединение с источником данных в формате Access 2007  
 Для доступа к источнику данных в формате Access 2007 диспетчеру соединений OLE DB требуется поставщик данных OLE DB для компонента Microsoft Office 12.0 Access Database Engine. Этот поставщик устанавливается автоматически вместе с системой [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007. Если система Office 2007 не установлена на компьютере, где работают службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , необходимо отдельно установить поставщик. Чтобы установить поставщик OLE DB для ядра СУБД Microsoft Office 12.0 Access, скачайте и установите компоненты, расположенные на веб-странице [2007 Office System Driver: Data Connectivity Components](http://go.microsoft.com/fwlink/?LinkId=98155)(Системный драйвер Office 2007: компоненты связи с данными)  
  
### <a name="to-create-an-ole-db-connection-manager-from-the-connection-managers-area"></a>Создание диспетчера соединений OLE DB из области «Диспетчеры соединений»  
  
1.  Откройте пакет в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Щелкните правой кнопкой мыши в области **Диспетчеры соединений** , а затем выберите команду **Создать соединение OLE DB**.  
  
3.  В диалоговом окне **Настройка диспетчера соединений OLE DB** нажмите кнопку **Создать**.  
  
     Дополнительные сведения см. в разделе [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  В диалоговом окне **Диспетчер соединений** в поле **Поставщик**выберите поставщик **OLE DB для СУБД Microsoft Office 12.0 Access**, а затем настройте диспетчер соединений.  
  
    > [!NOTE]  
    >  Для соединения с источником данных, который использует Access 2007, выбирать в поле **Источник данных** значение **Поставщик Microsoft OLE DB для Jet 4.0**нельзя.  
  
### <a name="to-create-an-ole-db-connection-from-the-sql-server-import-and-export-wizard"></a>Создание соединения OLE DB из мастера импорта и экспорта SQL Server  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]запустите мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  В диалоговом окне **Выбор источника данных** в поле **Источник данных**выберите поставщик **OLE DB для СУБД Microsoft Office 12.0 Access**, а затем настройте соединение.  
  
    > [!NOTE]  
    >  Для соединения с источником данных, который использует Access 2007, выбирать в поле **Источник данных** значение **Поставщик Microsoft OLE DB для Jet 4.0**нельзя.  
  
     При выборе в поле **Источник данных** значения **поставщик OLE DB для СУБД Microsoft Office 12.0 Access**мастер автоматически создаст диспетчер соединения OLE DB с нужным поставщиком данных. Дополнительные сведения см. в разделе [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="see-also"></a>См. также:  
 [Подключение к книге Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
