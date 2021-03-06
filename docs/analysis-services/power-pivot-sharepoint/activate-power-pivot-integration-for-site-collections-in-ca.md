---
title: Активация интеграции PowerPivot для семейств веб-сайтов в ЦС | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77c8cb0d9e9617bfa0560ae1e9bc6389a297a5c2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>Активация интеграции PowerPivot для семейств веб-сайтов в ЦС
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  При использовании параметра установки существующей фермы для установки SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint необходимо включить интеграцию функций [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для определенных семейств веб-сайтов. Если надстройка [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint была установлена с параметром "Новый сервер", эту задачу можно пропустить, так как программа установки SQL Server уже активировала интеграцию компонента [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для корневого семейства веб-сайтов при настройке развертывания.  
  
 Активация компонента на уровне семейств веб-сайтов необходима для того, чтобы сделать страницы и шаблоны приложения доступными для веб-сайтов, в том числе страницы конфигурации для планового обновления данных и страницы приложений для библиотеки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Gallery и библиотек веб-каналов данных.  
  
 Необходимо включить интеграцию [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для всех семейств веб-сайтов, поддерживающих обработку запросов [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="prerequisites"></a>предварительные требования  
 Пользователь должен быть администратором семейства веб-сайтов.  
  
## <a name="activate-power-pivot-features"></a>Включение функций PowerPivot  
  
1.  На сайте SharePoint нажмите кнопку **Действия сайта**.  
  
     По умолчанию доступ к веб-приложениям SharePoint осуществляется через порт 80. Это означает, что часто доступен сайта SharePoint, введя http://\<имя компьютера > Открыть корневой коллекции сайтов.  
  
2.  Щелкните элемент **Настройки сайта**.  
  
3.  В области "Администрирование семейства веб-сайтов" щелкните ссылку **Возможности семейства узлов**.  
  
4.  Прокрутите страницу вниз до пункта **Функция семейства веб-сайтов для интеграции с [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
5.  Нажмите кнопку **Активировать**.  
  
6.  Повторите эти действия для дополнительных семейств веб-сайтов, открыв каждый из сайтов и щелкнув **Действия сайта**.  
  
## <a name="see-also"></a>См. также  
 [Настройка и администрирование сервера Power Pivot в центре администрирования](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Первоначальная настройка (Power Pivot для SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [Установка Power Pivot для SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
