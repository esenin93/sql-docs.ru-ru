---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 212ce15f0d28b16b81a9c07d785c129b039cdc6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Шифрует данные при помощи асимметричного ключа.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Аргументы  
 *Asym_Key_ID*  
 Идентификатор асимметричного ключа в базе данных. **int**.  
  
 *cleartext*  
 Строка данных, которая будет зашифрована с помощью асимметричного ключа.  
  
 **@plaintext**  
 Переменная типа **nvarchar**, **char**, **varchar**, **binary**, **varbinary** или **nchar**, содержащая данные, которые будут зашифрованы с помощью асимметричного ключа.  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Переменная типа **varbinary** с максимальным размером 8000 байт.  
  
## <a name="remarks"></a>Remarks  
 Шифрование/дешифрование с помощью асимметричного ключа является очень дорогостоящим по сравнению с шифрованием/дешифрованием с помощью симметричного ключа. Рекомендуется не шифровать асимметричным ключом большие наборы данных, например таблицы с пользовательскими данными. Вместо этого данные следует шифровать с помощью сильного симметричного ключа, а симметричный ключ шифровать с помощью асимметричного.  
  
 **EncryptByAsymKey** возвращает значение **NULL**, если ввод превышает определенное число байтов, в зависимости от алгоритма. Ограничения: ключ RSA на 512 бит может шифровать до 53 байт, ключ на 1024 бита может шифровать до 117 байт, ключ на 2048 бит может шифровать до 245 байт. (Обратите внимание, что в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и сертификаты, и асимметричные ключи служат оболочками для ключей RSA.)  
  
## <a name="examples"></a>Примеры  
 В следующем примере текст из переменной `@cleartext` шифруется асимметричным ключом `JanainaAsymKey02`. Зашифрованные данные помещаются в таблицу `ProtectedData04`.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [DECRYPTBYASYMKEY (Transact-SQL)](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Иерархия средств шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
