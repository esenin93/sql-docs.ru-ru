---
title: Добавление подписчика, отличного от подписчика SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97688beba720f9bd99d5b621d0ae5abda70be6c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="add-non-sql-server-subscriber"></a>Добавить подписчик, отличный от подписчика SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Репликация поддерживает принудительные подписки на моментальные снимки и публикации транзакций для подписчиков Oracle и IBM DB2.  
  
## <a name="options"></a>Параметры  
 **Тип добавляемого подписчика:**  
 Выберите подписчик Oracle или подписчик IBM DB2. Дополнительные сведения о поддержке таких подписчиков см. в статье [Подписчики, отличные от подписчиков SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 **Имя источника данных**  
 Данное имя позволяет найти базу данных в сети. Строка соединения с базой данных, формируемая репликацией, содержит имя источника данных, имя входа, пароль и параметры соединения, указанные на странице **Безопасность агента распространителя** данного мастера.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не проверяет имя источника данных и строку подключения, пока агент распространителя не попытается инициализировать подписку.  
  
## <a name="see-also"></a>См. также:  
 [Создание подписки для подписчика, отличного от подписчика SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Подписка на публикации](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
