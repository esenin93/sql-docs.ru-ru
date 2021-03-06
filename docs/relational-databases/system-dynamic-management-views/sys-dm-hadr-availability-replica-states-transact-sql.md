---
title: sys.dm_hadr_availability_replica_states (Transact-SQL) | Документы Microsoft
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
caps.latest.revision: 65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e04fa466f018e114fe66686b81c5e5899dd2371e
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Возвращает по строке для каждой локальной реплики и одной строке для каждой удаленной реплики в качестве локальной реплики одной группы доступности Always On. Каждая строка содержит сведения о состоянии для данной реплики.  
  
> [!IMPORTANT]  
>  Чтобы получить сведения о каждой реплики в группу доступности, запросите **sys.dm_hadr_availability_replica_states** на экземпляре сервера, на котором размещается первичная реплика. На экземпляре сервера, где размещена вторичная реплика группы доступности, это динамическое административное представление возвращает лишь локальные сведения о группе доступности.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Уникальный идентификатор реплики.|  
|**group_id**|**uniqueidentifier**|Уникальный идентификатор группы доступности.|  
|**is_local**|**бит**|Является ли реплика является локальным, один из:<br /><br /> 0 = указывает удаленную вторичную реплику в группе доступности, первичная реплика которой размещена на локальном экземпляре сервера. Это значение появляется только в расположении первичной реплики.<br /><br /> 1 = обозначает локальную реплику. Во вторичных репликах это единственное доступное значение для группы доступности, к которой принадлежит реплика.|  
|**Роли**|**tinyint**|Текущий [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] роли локальная реплика или подключенной удаленной реплики, одно из:<br /><br /> 0 = разрешается<br /><br /> 1 = первичная<br /><br /> 2 = вторичная<br /><br /> Дополнительные сведения о ролях [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] см. в разделе [Обзор групп доступности AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|**role_desc**|**nvarchar(60)**|Описание **роли**, одно из:<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|Текущее состояние работоспособности реплики может быть одним из:<br /><br /> 0 = ожидание отработки отказа<br /><br /> 1 = ожидает согласования<br /><br /> 2 = в сети<br /><br /> 3 = вне сети<br /><br /> 4 = ошибка<br /><br /> 5 = ошибка, нет кворума<br /><br /> NULL = реплика не является локальной<br /><br /> Дополнительные сведения см. в разделе [роли и состояния работоспособности](#RolesAndOperationalStates)далее в этом разделе.|  
|**оперативной\_состояние\_desc**|**nvarchar(60)**|Описание **operational\_состояние**, одно из:<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**восстановление\_работоспособности**|**tinyint**|Свертку **базы данных\_состояние** столбец [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) динамическое административное представление. Ниже приведены возможные значения и их описания.<br /><br /> 0: в данный момент.  По крайней мере одна присоединенная база данных имеет состояние, отличное от ONLINE (**базы данных\_состояние** — не равно 0).<br /><br /> 1: online. Все присоединенные базы данных имеют состояние базы данных ONLINE (**database_state** равно 0).<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|Описание **recovery_health**, одно из:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**Синхронизация\_работоспособности**|**tinyint**|Отражает свертку состояния синхронизации базы данных (**synchronization_state**) всех присоединенных баз данных доступности (также известный как *реплик*) и режим доступности реплики ( синхронной или асинхронной фиксации режим). Накопительный пакет обновления будут отображены накопительные состояния наименее работоспособных баз данных в реплике. Ниже приведены возможные значения и их описания.<br /><br /> 0: неработоспособны.   Как минимум одна из присоединенных баз данных находится в состоянии NOT SYNCHRONIZING.<br /><br /> 1: частично работоспособна. Некоторые реплики не находятся в целевом состоянии синхронизации: реплики с синхронной фиксацией должны быть синхронизированы, а реплики с асинхронной фиксацией должны синхронизироваться.<br /><br /> 2: исправен. Все реплики находятся в целевом состоянии синхронизации: реплики с синхронной фиксацией синхронизированы, а реплики с асинхронной фиксацией синхронизируются.|  
|**synchronization_health_desc**|**nvarchar(60)**|Описание **synchronization_health**, одно из:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|Используется ли вторичная реплика в настоящее время подключения к первичной реплике. Ниже приведены возможные значения с описаниями.<br /><br /> 0: отключен. Ответ реплики доступности на состояние DISCONNECTED зависит от его роль: в первичной реплике при отключении вторичной реплики баз данных-получателей, помечаются как NOT SYNCHRONIZED в первичной реплике, которая ожидает от вторичной повторное подключение; На вторичной реплике при обнаружении, что она отключена вторичная реплика пытается подключиться к первичной реплике.<br /><br /> 1: подключен.<br /><br /> Каждая первичная реплика отслеживает состояние соединения для всех вторичных реплик в той же группе доступности. Вторичные реплики отслеживают состояние соединения только первичной реплики.|  
|**connected_state_desc**|**nvarchar(60)**|Описание **connection_state**, одно из:<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|Номер последней возникшей ошибки подключения.|  
|**last_connect_error_description**|**nvarchar(1024)**|Текст **last_connect_error_number** сообщения.|  
|**last_connect_error_timestamp**|**datetime**|Отметка даты и времени, указывающее, когда **last_connect_error_number** произошла ошибка.|  
  
##  <a name="RolesAndOperationalStates"></a> Роли и состояния работоспособности  
 Роль, **роли**, отражает состояние определенной реплики доступности и рабочее состояние **operational_state**, описывает ли реплика готова к обработке клиентских запросов для всех База данных реплики доступности. Ниже приводится сводка состояний работоспособности, которые возможны для каждой роли: разрешение, ПЕРВИЧНЫХ и ВТОРИЧНЫХ.  
  
 **СОПОСТАВЛЕНИЕ:** когда реплика доступности находится в роли РАЗРЕШЕНИЯ, возможные состояния работоспособности, как показано в следующей таблице.  
  
|Состояние работоспособности|Описание|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|В группе доступности выполняется команда отработки отказа.|  
|OFFLINE|Все данные конфигурации для реплики доступности были обновлены на кластере WSFC и в локальных метаданных, но в настоящее время в группе доступности отсутствует первичная реплика.|  
|FAILED|При попытке получить информацию из кластера WSFC возникла ошибка чтения.|  
|FAILED_NO_QUORUM|На локальном узле WSFC нет кворума. Это выведенное состояние.|  
  
 **ОСНОВНОЙ:** Если реплика доступности выполняет ПЕРВИЧНУЮ роль, он в настоящее время является первичной репликой. Возможные состояния работоспособности, как показано в следующей таблице.  
  
|Состояние работоспособности|Описание|  
|-----------------------|-----------------|  
|PENDING|Это переходное состояние, но первичная реплика может «застрять» в этом состоянии при отсутствии рабочих потоков для обработки запросов.|  
|ONLINE|Ресурс группы доступности находится в сети, и все рабочие потоки базы данных задействованы.|  
|FAILED|Реплика доступности не может выполнять операции чтения или записи в кластере WSFC.|  
  
 **ПОЛУЧАТЕЛЬ:** при выполнении ВТОРИЧНОЙ роли реплика доступности, в данный момент вторичная реплика. Возможные состояния работоспособности, как показано в следующей таблице.  
  
|Состояние работоспособности|Описание|  
|-----------------------|-----------------|  
|ONLINE|Локальная вторичная реплика подключена к первичной реплике.|  
|FAILED|Локальная вторичная реплика не может выполнять операции чтения или записи в кластере WSFC.|  
|NULL|В первичной реплике это значение возвращается в том случае, когда строка относится к вторичной реплике.|  
  
## <a name="security"></a>безопасность  
  
### <a name="permissions"></a>Разрешения  
 необходимо разрешение VIEW SERVER STATE на сервере.  
  
## <a name="see-also"></a>См. также  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Отслеживание групп доступности (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
