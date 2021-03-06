---
title: Добавление, изменение или удаление допустимых значений параметра отчета | Документы Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4d3466964e2b2550e5b0dd6b90cbaac3a063e68e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter"></a>добавить, изменить или удалить допустимые значения параметра отчета
  После создания параметра отчета можно указать список допустимых значений, которые будут выведены для пользователя. Список допустимых значений ограничивает значения, которые может выбрать пользователь, набором допустимых значений.  
  
 Допустимые значения выводятся в раскрывающемся списке рядом с параметром отчета на панели инструментов при выполнении отчета. Параметры отчета могут представлять одно или несколько значений. В случае нескольких значений в верхней позиции списка будет расположено значение **Выделить все** , предоставляя пользователю возможность выбрать или очистить все значения одним щелчком.  
  
 Можно предоставить статический список значений или список из набора данных отчета. Дополнительно значениям можно присвоить понятные имена, указав значение в поле метки. Например, для параметра на основе поля `ProductID` можно вывести в метке параметра поле `ProductName` . При работе отчета пользователь сможет выбирать названия продуктов, но на самом деле выбранное значение будет соответствовать полю `ProductID`.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 После публикации отчета можно изменить доступные значения, определяемые в отчете с помощью средства разработки отчетов, задавая значения свойств параметров на сервере отчетов. Дополнительные сведения см. в разделе [Параметры отчета (построитель отчетов и конструктор отчетов)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>Добавление или изменение допустимых значений параметра отчета  
  
1.  В области данных отчета разверните узел «Параметры». Щелкните правой кнопкой мыши параметр и выберите пункт **Свойства параметра**. Откроется диалоговое окно **Свойства параметра отчета** .  
  
    > [!NOTE]  
    >  Если область данных отчета не появилась, в меню **Вид** выберите команду **Данные отчета**.  
  
2.  Нажмите кнопку **Допустимые значения**. Выберите параметр допустимых значений.  
  
    -   Нажмите кнопку **Указать значения** , чтобы вручную ввести список значений, и, по желанию, понятные имена (метки) для значений.  
  
         Нажмите кнопку **Добавить** и введите значение в текстовое поле **Значение** и, по желанию, метку в текстовое поле **Метка** . Если не указать метку, будет использовано значение. Для значения можно записать выражение. Тип данных должен соответствовать типу данных параметра. Нельзя задавать параметры в выражении с помощью имен полей. Примеры см. в разделе [Часто используемые фильтры (построитель отчетов и службы SSRS)](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md).  
  
         Повторите этот шаг для всех значений, которые нужно указать. Порядок, в котором значения отображаются в данном списке, определяет порядок, в котором пользователь увидит их в раскрывающемся списке. Чтобы изменить порядок элементов списка, щелкните текстовое поле **Значение** или **Метка** , чтобы выбрать элемент, а потом с помощью кнопок со стрелками вверх и вниз переместите выбранный элемент вверх или вниз по списку.  
  
    -   Чтобы ввести имя существующего набора данных, который получает значения и, по желанию, понятные имена для данного параметра, щелкните **Получать значения из запроса** .  
  
        > [!IMPORTANT]  
        >  Если один и тот же набор данных содержит параметр запроса, соответствующий параметру отчета, то отчет отобразит сообщение об ошибке при попытке запустить его. Эту ошибку можно устранить, использовав другой набор данных для получения значений.  
  
         В поле **Набор данных**введите имя набора данных.  
  
         В поле **Поле значения**выберите имя поля, которое предоставляет значения параметра.  
  
         В поле **Поле метки**выберите имя поля, предоставляющего понятные имена для параметра. Если для понятных имен нет отдельного поля, выберите поле, которое было выбрано для поля **Значение** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     При предварительном просмотре отчета можно увидеть раскрывающийся список допустимых значений параметра.  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>Удаление допустимых значений параметра отчета  
  
1.  В области данных отчета разверните узел «Параметры». Щелкните правой кнопкой мыши параметр и выберите пункт **Свойства параметра**. Откроется диалоговое окно **Параметры отчета** .  
  
2.  Нажмите кнопку **Допустимые значения**.  
  
3.  В поле **Выберите один из следующих параметров**укажите значение **Нет**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     При предварительном просмотре отчета можно увидеть, что для данного параметра раскрывающийся список допустимых значений больше не появляется.  
  
## <a name="see-also"></a>См. также:  
 [Изменение порядка параметров отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Добавление, изменение или удаление параметра отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Добавление каскадных параметров в отчет (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Добавление, изменение или удаление значения по умолчанию для параметра отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Ссылки на коллекцию параметров (построитель отчетов и службы SSRS)](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Учебник. Добавление параметра к отчету (построитель отчетов)](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Выражения (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
