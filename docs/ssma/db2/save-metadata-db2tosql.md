---
title: Сохранение метаданных (DB2ToSQL) | Документы Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9a76083e-4902-449e-b125-7e9259fc37f7
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9563eee331be3a1b091bc2fb1dda55492256a53d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="save-metadata-db2tosql"></a>Сохранение метаданных (DB2ToSQL)
**Сохранить метаданные** диалоговом окне будет предложено загрузить метаданные в проект SSMA перед сохранением. Это позволяет иметь полный файл проекта, который можно использовать в автономном режиме и отправить другим пользователям, например, сотрудники службы технической поддержки.  
  
Чтобы получить доступ к **сохранить метаданные** диалоговое окно, сохраните проект. Если отсутствуют какие-либо метаданные, будет отображаться SSMA **сохранить метаданные** диалоговое окно.  
  
## <a name="options"></a>Параметры  
**Название**  
Имя каждой базы данных в проекте.  
  
**Состояние**  
Указывает метаданные, загруженный в проект SSMA или отсутствуют метаданные.  
  
SSMA загружает метаданные в проект при необходимости. Метаданные автоматически загружаются после просмотра метаданных и преобразования схемы.  
  
**Выделить все**  
Выбирает все перечисленные базы данных.  
  
**Clear**  
Снимает флажок для всех баз данных с отсутствующими метаданными. Не удается снимите флажок, если для загрузки метаданных.  
  
**Сохранить**  
Сохраняет проект, загрузка метаданных для выбранных баз данных, имеющих отсутствующие метаданные.  
  
**Отмена**  
Отменяет сохранения операции. Отсутствующие метаданные не загружается в проект.  
  
