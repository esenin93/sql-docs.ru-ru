---
title: Учебник служб удаленных рабочих СТОЛОВ | Документы Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40ab51d55e33549c2ecc5a615f00f396dd9bb6c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="rds-tutorial"></a>Учебник служб удаленных рабочих СТОЛОВ
Этот учебник демонстрирует использование модели программирования служб удаленных рабочих СТОЛОВ для запроса и обновления источника данных. Во-первых он описывает действия, необходимые для выполнения этой задачи. Затем учебника повторяется в Microsoft® Visual Basic Scripting Edition (с ADO ввода для Windows Foundation Classes (ADO и WFC)).  
  
 Этот учебник, кодируется в различных языках по двум причинам:  
  
-   Документация для служб удаленных рабочих СТОЛОВ предполагает, что коды чтения в Visual Basic. Это делает документации удобным для программистов Visual Basic, но менее полезен для программистов, использовать и другие языки.  
  
-   Если вы не уверены в конкретной функции служб удаленных рабочих СТОЛОВ, и вам известно немного из другого языка, можно попытаться устранить ваш вопрос, поиск одной функции, выраженное в другом языке.  
  
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ больше не включаются в операционной системе Windows (в разделе Windows 8 и [руководство по Windows Server 2012 совместимости](https://www.microsoft.com/en-us/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будут удалены в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ необходимо перенести в [службы данных WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>Способ представления учебника  
 Этот учебник основывается на модели программирования служб удаленных рабочих СТОЛОВ. В нем описывается каждый шаг модели программирования по отдельности. Кроме того он иллюстрирует фрагмент кода Visual Basic по каждому шагу.  
  
 В примере кода повторяется на других языках с минимальными обсуждения. Каждый шаг в учебнике данного языка программирования в модели программирования и описания учебник помечается соответствующего шага. Используйте номер шага, чтобы см. в обсуждении описательные учебника.  
  
 Модель программирования служб удаленных рабочих СТОЛОВ, указанное в следующем разделе. Используйте его в качестве руководства, в процессе работы с учебником.  
  
## <a name="rds-programming-model-with-objects"></a>Модель программирования служб удаленных рабочих СТОЛОВ с объектами  
  
-   Укажите программу для вызова на сервере и получить способом (прокси) для ссылки на него из клиента.  
  
-   Необходимо вызовите программу сервера. Передача параметров серверной программой, которая определяет источник данных и команды для выдачи.  
  
-   Программа сервер получает [записей](../../../ado/reference/ado-api/recordset-object-ado.md) из источника данных, обычно с помощью ADO. При необходимости **записей** объект обрабатывается на сервере.  
  
-   Программа server Возвращает конечное **записей** объекта клиентскому приложению.  
  
-   На стороне клиента **записей** при необходимости помещения объекта в форму, которую можно легко использовать визуальные элементы управления.  
  
-   Изменения **записей** отправляются обратно на сервер и используется для обновления источника данных объекта.  
  
 Этот учебник содержит следующие разделы.  
  
-   [Шаг 1. Укажите программу сервера (учебник по RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Шаг 2. Вызовите программу сервера (учебник по RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Шаг 3. Сервер получает набор записей (учебник по RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Шаг 4. Сервер возвращает набор записей (учебник по RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Шаг 5. DataControl теперь можно использовать (учебник по RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Шаг 6. Изменения отправлены на сервер (учебник по RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Учебник по RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>См. также  
 [Шаг 1: Укажите программу Server (служб удаленных рабочих СТОЛОВ учебник)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Учебник по RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
