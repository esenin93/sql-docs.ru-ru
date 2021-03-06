---
title: SQL Server Migration Assistant для Access (AccessToSQL) | Документы Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 08/14/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 43b725e800fba4bdb085b03cd0ea183624249b9b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>SQL Server Migration Assistant для Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) для доступа является инструментом для переноса баз данных из [!INCLUDE[msCoName](../../includes/msconame_md.md)] версий 97 — 2010 для доступа к [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2017 г. в Windows и Linux (Предварительная версия) или [!INCLUDE[msCoName](../../includes/msconame_md.md)] базы данных Azure SQL. SSMA для Access преобразует объекты базы данных Access для [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или объекты базы данных Azure SQL, эти объекты на загрузку [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или Azure SQL и затем перемещает данные из доступа к [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или Azure SQL.  
  
Эта документация содержит описание SSMA для Access и приведены пошаговые инструкции по миграции баз данных для доступа к [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или SQL Azure и сведения о проблемах, которые могут возникнуть после миграции.  
  
## <a name="contents"></a>Содержание  
  
|Раздел|Описание|  
|-----------|---------------|  
|[Новые возможности в SSMA для Access](http://msdn.microsoft.com/en-us/a24d3fc0-6911-4bfa-828a-197abf222e02)|Список всех изменений в выпусках SSMA.|  
|[Установка SQL Server Migration Assistant для Access](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)|Предварительные требования для установки SSMA процедуры по установке и лицензирования SSMA и ссылка на последнюю версию.|  
|[Приступая к работе с SQL Server Migration Assistant для Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|Вводит SSMA и пользовательский интерфейс.|  
|[Подготовка к миграции базы данных Access](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)|Описывает подготовку баз данных Access для преобразования в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure.|  
|[Миграция баз данных Access в SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)|Обзор процесса преобразования и подробные сведения о каждом шаге в процесс.|  
|[Связывание приложения Access в SQL Server](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)|Описывает, как использовать существующие приложения Access с [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Справочник по пользовательскому интерфейсу](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)|Содержит документацию по SSMA диалоговым окнам.|  
|[Работа с консолью SSMA для Access](http://msdn.microsoft.com/en-us/ef94e843-9f88-45a2-86c4-a0af268738c4)|Содержит документацию по SSMA консольного приложения|  
|[Получение поддержки по SSMA для Access](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|Сведения о получении дополнительной помощи.|  
  
