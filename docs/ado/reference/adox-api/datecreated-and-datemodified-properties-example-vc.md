---
title: "DateCreated и DateModified примере свойства (VC ++) | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- DateCreated property [ADOX], VC++ example
- DateModified property [ADOX], VC++ example
ms.assetid: b964beee-83c7-4f91-8255-3ba864c9adfd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 480f6e170c0d2550ebd73925bddcfebf9a7d3126
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="datecreated-and-datemodified-properties-example-vc"></a>DateCreated и DateModified примере свойства (VC ++)
В этом примере демонстрируется [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) и [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) свойства путем добавления нового [столбца](../../../ado/reference/adox-api/column-object-adox.md) к существующему [таблицы](../../../ado/reference/adox-api/table-object-adox.md) и с помощью Создание нового **таблицы**. Процедура DateOutput является обязательным для выполнения этого примера.  
  
```  
// BeginDateCreatedCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void DateCreatedX();  
void DateOutPut(_bstr_t strTemp, _TablePtr tblTemp);  
  
int main() {  
    if ( FAILED(::CoInitialize(NULL) ) )  
        return -1;  
    DateCreatedX();  
    ::CoUninitialize();  
}  
  
void DateCreatedX() {  
    HRESULT hr = S_OK;  
  
    // Define ADOX object pointers, initialize pointers. These are in ADODB  namespace.  
    _CatalogPtr m_pCatalog = NULL;  
    _TablePtr m_pTblEmployees = NULL;  
    _TablePtr m_pTblNew = NULL;  
  
    // Set ActiveConnection of Catalog to this string  
    _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';Data Source= 'c:\\Northwind.mdb';");  
  
    try {  
        TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
  
        // Connect the catalog.  
        m_pCatalog->PutActiveConnection(strCnn);  
        m_pTblEmployees = m_pCatalog->Tables->GetItem("Employees");  
  
        // Print current information about the Employees table.  
        DateOutPut((_bstr_t)"Current properties", m_pTblEmployees);  
  
        // Create and append column to the Employees table.  
        m_pTblEmployees->Columns->Append("NewColumn", adInteger,0);  
        m_pCatalog->Tables->Refresh();  
  
        // Print new information about the Employees table.  
        DateOutPut((_bstr_t)"After creating a new column", m_pTblEmployees);  
  
        // Delete new column because this is a demonstration.  
        m_pTblEmployees->Columns->Delete("NewColumn");  
  
        // Create and append new Table object to the Northwind database.  
        TESTHR(hr = m_pTblNew.CreateInstance(__uuidof(Table)));  
  
        m_pTblNew->Name = "NewTable";  
        m_pTblNew->Columns->Append("NewColumn", adInteger,0);  
        m_pCatalog->Tables->Append(_variant_t((IDispatch*)m_pTblNew));  
        m_pCatalog->Tables->Refresh();  
  
        // Print information about the new Table object.  
        DateOutPut((_bstr_t)"After creating a new table", m_pCatalog->Tables->GetItem("NewTable"));  
  
        // Delete new Table object because this is a demonstration.  
        m_pCatalog->Tables->Delete(m_pTblNew->Name);  
    }  
  
    catch(_com_error &e) {  
        // Notify the user of errors if any.  
        _bstr_t bstrSource(e.Source());  
        _bstr_t bstrDescription(e.Description());  
  
        printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
    }  
  
    catch(...) {  
        cout << "Error occured in include files...." << endl;  
    }  
}  
  
void DateOutPut(_bstr_t strTemp , _TablePtr tblTemp) {  
    // Print DateCreated and DateModified information about specified Table object.  
    cout << strTemp << endl;  
    cout << "    Table: " << tblTemp->GetName() << endl;  
    cout << "        DateCreated = " << (_bstr_t)tblTemp->GetDateCreated() << endl;  
    cout << "        DateModified = " << (_bstr_t)tblTemp->GetDateModified() << endl;  
}  
```  
  
## <a name="see-also"></a>См. также:  
 [Объект столбца (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Свойство DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)   
 [Свойство DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)   
 [Объект таблицы (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)