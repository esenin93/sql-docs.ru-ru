---
title: 'SQL: Overflow-field (SQLXML 4.0) | Документы Microsoft'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5f4527068d0fd0f83987f5e145226c091a7913c0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="annotation-interpretation---sqloverflow-field"></a>Интерпретация заметки - SQL: Overflow-поле
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  В схеме можно указать столбец как столбец переполнения, чтобы получить все невостребованные данные из XML-документа. Этот столбец указывается в схеме с помощью **SQL: Overflow-поле** заметки. Возможно иметь несколько столбцов переполнения.  
  
 Каждый раз, когда XML-узла (элемент или атрибут), не **SQL: Overflow-поле** определена заметка входит в область, столбец переполнения активируется и получает невостребованные данные. Когда узел выходит за границы области, столбец переполнения перестает быть активным, и процедура массовой загрузки XML делает активным предыдущее поле переполнения (если таковое имеется).  
  
 Сохранения данных в столбце переполнения, Массовая загрузка XML также сохраняет открывающий и закрывающий теги родительского элемента для которой **SQL: Overflow-поле** определен.  
  
 Например, следующая схема описывает  **\<клиентов >** и  **\<CustOrder >** элементов. Каждый из данных элементов определяет столбец переполнения:  
  
```  
<?xml version="1.0" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
 <xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
        parent="Cust"  
        parent-key="CustomerID"  
        child="CustOrder"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
 </xsd:annotation>  
 <xsd:element name="ROOT" sql:is-constant="1">  
  <xsd:complexType>  
    <xsd:sequence>   
      <xsd:element name="Customers"   
                   sql:relation="Cust"  
                   sql:overflow-field="OverflowColumn">  
        <xsd:complexType>  
             <xsd:sequence>   
             <xsd:element name="CustomerID" type="xsd:integer"/>  
             <xsd:element name="CompanyName"  type="xsd:string"/>  
             <xsd:element name="City" type="xsd:string"/>  
             <xsd:element name="Order"  
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder"  
                          sql:overflow-field="OverflowColumn">  
               <xsd:complexType>  
                 <xsd:attribute name="OrderID"/>  
                 <xsd:attribute name="CustomerID"/>  
               </xsd:complexType>  
             </xsd:element>  
          </xsd:sequence>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 В схеме  **\<клиента >** элемент сопоставляется с таблицей Cust и  **\<порядок >** элемент сопоставляется с таблицей CustOrder.  
  
 Оба  **\<клиента >** и  **\<порядок >** элементы определяют столбец переполнения. Таким образом, Массовая загрузка XML сохраняет все невостребованные дочерние элементы и атрибуты  **\<клиента >** элемент в столбец переполнения таблицы Cust и все невостребованные дочерние элементы и атрибуты  **\<Порядок >** элемент в столбец переполнения таблицы CustOrder.  
  
### <a name="to-test-a-working-sample"></a>Проверка рабочего образца  
  
1.  Сохраните схему, приведенную в этом примере, в файле SampleSchema.xml.  
  
2.  Создайте следующие таблицы.  
  
    ```  
    CREATE TABLE Cust (  
              CustomerID     int         PRIMARY KEY,  
              CompanyName    varchar(20) NOT NULL,  
              City           varchar(20) DEFAULT 'Seattle',  
              OverflowColumn nvarchar(200))  
    GO  
    CREATE TABLE CustOrder (  
              OrderID        int         PRIMARY KEY,  
              CustomerID     int         FOREIGN KEY REFERENCES  
                                              Cust(CustomerID),  
              OverflowColumn nvarchar(200))  
    GO  
    ```  
  
3.  Сохраните следующий образец XML-данных в файле SampleXMLData.xml.  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
          <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
     </Customers>  
     <Customers>  
       <CustomerID>1112</CustomerID>  
       <CompanyName>Toms Spezialitten</CompanyName>  
       <City><![CDATA[LA]]> </City>  
       <xyz><address>111 Maple, Seattle</address></xyz>     
       <Order OrderID="3" />  
     </Customers>  
       <Customers>  
       <CustomerID>1113</CustomerID>  
       <CompanyName>Victuailles en stock</CompanyName>  
       <Order OrderID="4" />  
      </Customers>  
    </ROOT>  
    ```  
  
4.  Чтобы выполнить массовую загрузку XML-данных, сохраните этот пример на языке [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) в файле Sample.vbs и выполните его.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
