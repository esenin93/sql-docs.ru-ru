---
title: Принципы работы ADO | Документы Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da11650be6a1188933909fc49a1c06c8b4d61fb4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="ado-fundamentals"></a>Принципы работы ADO
ADO предоставляет разработчикам мощные, логические объектную модель для программного доступа к, изменение и обновление данных из разнообразных источников данных, через интерфейсы OLE DB системы. Наиболее распространенное использование ADO является запрос таблицы или таблиц в реляционной базе данных, получения и отображения результатов в приложении и возможно позволяют внести и сохранить изменения в данных. Ниже приведены другие задачи:  
  
-   Запросы к базе данных с помощью SQL и отображения результатов.  
  
-   Доступ к сведениям в хранилище файлов в Интернете.  
  
-   Обработка сообщений и папок в системе электронной почты.  
  
-   Сохранение данных из базы данных в XML-файл.  
  
-   Выполнение команд, описанных с XML и получение XML-потока.  
  
-   Сохранение данных в двоичный файл или поток XML.  
  
-   Дает пользователям возможность просматривать и изменять данные в таблицах базы данных.  
  
-   Создание и повторное использование параметризованных команд базы данных.  
  
-   Выполнение хранимых процедур.  
  
-   Динамическое создание гибкую структуру, которая называется **записей**, для хранения, перейдите и работы с данными.  
  
-   Выполнение операций транзакций базы данных.  
  
-   Фильтрация и сортировка локальные копии сведений из базы данных на основе условий во время выполнения.  
  
-   Создание и управление ими иерархические результаты из баз данных.  
  
-   Привязка полей базы данных для компонентов, привязанных данных.  
  
-   Создание удаленного, отключен **наборы записей**.  
  
 ADO предоставляет разнообразные параметры и настройки для обеспечения такой гибкости. Таким образом важно методический подхода в том, как использовать в приложениях, неудачного завершения каждого из ваших целей на управляемые отрезки ADO.  
  
 В большинстве приложений, использующие ADO участвуют четыре основных операций: получение данных, проверка данных, изменения данных и обновление данных. Эти операции проверяются более подробно далее в этом разделе.  
  
 Тем не менее прежде чем рассмотреть эти сведения, мы представим обзор объектная модель ADO и простого приложения ADO, который записывается в Microsoft® Visual Basic® и выполняет каждый из четырех основных операций ADO:  
  
-   [Объекты и коллекции ADO](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: простое приложение ADO](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [Поставщики OLE DB](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [ошибки](../../../ado/guide/data/errors-ado.md)
