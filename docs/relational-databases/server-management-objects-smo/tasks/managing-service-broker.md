---
title: Управление компонентом Service Broker | Документы Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Service Broker [SMO]
ms.assetid: b29d7432-d1e5-4bb6-b544-57b3a9430f95
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1d3bb44a64386329570d78e8b3ce436b9573f63f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="managing-service-broker"></a>Управление компонентом Service Broker
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  В SMO [!INCLUDE[ssSB](../../../includes/sssb-md.md)] объекты, включенные в **Microsoft.SqlServer.Management.Smo.Broker** пространства имен, которое требуется ссылка на сборку Microsoft.SqlServer.SMO.dll. Кроме того, необходима ссылка на сборку Microsoft.SqlServer.ServiceBrokerEnum.dll для поддержки сведений о классах.  
  
 SMO предоставляет набор объектов компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)], которые допускают программное управление (DDL) реализацией [!INCLUDE[ssSB](../../../includes/sssb-md.md)]. Оно включает определение типов сообщений, контрактов, очередей и служб. Так как SMO является средством управления, которое не предназначено для работы с данными, SMO не поддерживает отправку и получение сообщений компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)].  
  
 В SMO объект <xref:Microsoft.SqlServer.Management.Smo.Database.ServiceBroker%2A> является классом верхнего уровня, который заключает всю функциональность компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)]. Реализация компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)] необходима для каждой базы данных, которая участвует в работе приложений с распределенным обменом сообщениями. Поэтому объект <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> является потомком объекта <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 Объект <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> содержит коллекции следующих объектов, используемых в определении реализации компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)].  
  
-   Объекты <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageType> представляют типы сообщений, которые определяют содержимое сообщений.  
  
-   Объекты <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageTypeMapping> представляют контракты, которые указывают направление и тип сообщений заданного диалога.  
  
-   Объекты <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceQueue> хранят сообщения до их отправки и после их получения. Они обеспечивают асинхронную связь между службами, а также и другие преимущества, такие как автоматическая блокировка сообщений внутри группы диалога.  
  
-   Объект <xref:Microsoft.SqlServer.Management.Smo.Broker.BrokerService> представляет собой компонент [!INCLUDE[ssSB](../../../includes/sssb-md.md)], которые являются адресуемыми конечными точками для диалогов. Сообщения компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)] отправляются от одной службы к другой. Служба определяет очередь для ожидания сообщений и указывает контракты, для которых служба может быть целью.  
  
-   Объекты <xref:Microsoft.SqlServer.Management.Smo.Broker.RemoteServiceBinding> представляют настройки, которые компонент [!INCLUDE[ssSB](../../../includes/sssb-md.md)] использует для безопасности и проверки подлинности при связи с удаленным сервером.  
  
-   Объекты <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceRoute> представляют маршрут компонента [!INCLUDE[ssSB](../../../includes/sssb-md.md)], который содержит информацию о нахождении службы и базы данных, в которой она определена. Маршрут необходим для доставки сообщения. По умолчанию каждая база данных содержит маршрут, который указывает расположение как текущий экземпляр [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>   
 [SQL Server Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
