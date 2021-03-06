---
title: ALTER TABLE - команда SQL | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 255ce0a4e9e06f2cdd20dd8d1e707b7f7823e6bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - команда SQL
Программно изменяет структуру таблицы.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>Аргументы  
 *TableName1*  
 Указывает имя таблицы, структура которого изменяется.  
  
 Установка [столбец] *FieldName1*  
 Указывает имя поля для добавления.  
  
 ALTER [столбец] *FieldName1*  
 Указывает имя существующего поля для изменения.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Указывает тип поля, ширина поля и поля, точность (число десятичных разрядов) для нового или измененного поля.  
  
 *FieldType* представляет собой одну букву, указывающее поля [тип данных](../../odbc/microsoft/visual-foxpro-field-data-types.md). Некоторые типы полей данных требуется указать *nFieldWidth* или *nPrecision* или оба.  
  
 *nFieldWidth* и *nPrecision* для D, G, I, L, M, P, T и Y игнорируются типов. По умолчанию *nPrecision* является ноль (без десятичных разрядов), если *nPrecision* не включено для типов B "," F "или" N.  
  
 NULL | NOT NULL  
 Разрешает или запрещает значения null в поле.  
  
 Если опустить NULL и NOT NULL, текущее значение параметра SET NULL определяет, допустимы ли значения null в поле. Однако если опустить NULL и NOT NULL и включать первичный ключ или УНИКАЛЬНЫЙ предложения, текущее значение параметра SET NULL игнорируется и поле не является значение NULL по умолчанию.  
  
 ПРОВЕРЬТЕ *lExpression1*  
 Указывает правило проверки для поля. *lExpression1* должно возвращать логическое выражение и может быть определяемой пользователем функции или хранимой процедуры. Каждый раз, когда добавляется пустую запись, проверяется правило проверки. Если правило проверки не допускает значение пустого поля в записи о добавленных возникнет ошибка.  
  
 Ошибка *cMessageText1*  
 Указывает, отображается сообщение об ошибке, если условие поля приводит к ошибке.  
  
 По умолчанию *eExpression1*  
 Задает значение по умолчанию для поля. Тип данных *eExpression1* должны совпадать как тип данных поля.  
  
 PRIMARY KEY  
 Создает тег первичного индекса. Тег индекс имеет то же имя, что и поле.  
  
 UNIQUE  
 Создает тег кандидата индекс с тем же именем, что и поле.  
  
> [!NOTE]  
>  Кандидат индексов (создания, включив параметр УНИКАЛЬНЫМ для совместимости с ANSI в инструкции ALTER TABLE или CREATE TABLE) отличаются от индексов, созданных с помощью параметра УНИКАЛЬНЫЙ индекс команды. Индекс, созданный с помощью UNIQUE в команде индекс допускает повторяющиеся ключи индекса; повторяющиеся ключи индекса не позволяют возможных кандидатур индексов.  
  
 В поле, которое используется для первичные или потенциальные индекса не разрешены значения NULL и повторяющиеся записи.  
  
 При создании нового поля с помощью Добавления СТОЛБЦА Visual FoxPro не приведет к ошибке при создании индекса первичные или потенциальные для поля, которое поддерживает значения null. Однако Visual FoxPro выдаст ошибку при попытке ввести значение null и повторяющихся в поле, которое используется для первичные или потенциальные индекса.  
  
 Если вы изменяете существующее поле, причем первичный или кандидат индексное выражение состоит из полей в таблице, Visual FoxPro проверяет поля содержат ли они значения null или повторяющиеся записи. Если они есть, Visual FoxPro возникает ошибка, и таблица не изменен.  
  
 Ссылки на *TableName2* ТЕГА *TagName1*  
 Указывает родительской таблицы, на который устанавливается постоянное связь. ТЕГ *TagName1* указывает тег индекса родительской таблицы, на котором основывается связь. Имена тегов индекс может содержать до 10 символов.  
  
 NOCPTRANS  
 Предотвращает преобразование в другую кодовую страницу для символьных и memo полей. Если таблица была преобразована в другую кодовую страницу, поля, для которых был указан NOCPTRANS не переводятся. NOCPTRANS можно указать только для полей символов и типа memo.  
  
 В следующем примере создается таблица с именем mytable, содержащий два поля с символьными и два поля типа memo. Второе поле символа, char2 и второе поле примечаний, memo2, включают NOCPTRANS для предотвращения преобразования.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [столбец] *FieldName2*  
 Указывает имя существующего поля для изменения.  
  
 По умолчанию НАБОР *eExpression2*  
 Указывает значение по умолчанию для существующего поля. Тип данных *eExpression2* должны совпадать как тип данных поля.  
  
 Проверка НАБОРА *lExpression2*  
 Указывает новое правило проверки для существующего поля. *lExpression2* должно возвращать логическое выражение и может быть определяемой пользователем функции или хранимой процедуры.  
  
 Ошибка *cMessageText2*  
 Указывает, отображается сообщение об ошибке, если условие поля приводит к ошибке. Сообщение отображается только в том случае, когда данные изменяются в окне просмотра или редактирования.  
  
 DROP DEFAULT  
 Удаляет значение по умолчанию для существующего поля.  
  
 ПРОВЕРКА УДАЛЕНИЯ  
 Удаление правила проверки для существующего поля.  
  
 DROP [столбец] *FieldName3*  
 Указывает поле, чтобы удалить из таблицы. Удаление поля из таблицы также удаляет значение поля по умолчанию и правила проверки поля.  
  
 Если индекс ключа или триггера выражения ссылки на поле, поле удалено выражения становятся недействительными. В этом случае ошибка, создается только в том случае, если поле удаляется, но недопустимый индекс ключа или триггера выражения будет создавать ошибки во время выполнения.  
  
 Проверка НАБОРА *lExpression3*  
 Указывает правило проверки таблицы. *lExpression3* должно возвращать логическое выражение и может быть определяемой пользователем функции или хранимой процедуры.  
  
 Ошибка *cMessageText3*  
 Указывает, отображается сообщение об ошибке, если правило проверки таблицы приводит к ошибке. Сообщение отображается только в том случае, когда данные изменяются в окне просмотра или редактирования.  
  
 ПРОВЕРКА УДАЛЕНИЯ  
 Удаляет правило проверки таблицы.  
  
 Добавить первичный ключ *eExpression3*ТЕГА *TagName2*  
 Добавляет в таблицу первичного индекса. *eExpression3* указывает выражение индекс первичного ключа, и *TagName2* указывает имя тега первичного индекса. Имена тегов индекс может содержать до 10 символов. Если ТЕГ *TagName2* опущен и *eExpression3* состоит из одного поля тег первичного индекса имеет то же имя, как поля, указанного в *eExpression3*.  
  
 УДАЛЕНИЕ ПЕРВИЧНОГО КЛЮЧА  
 Удаление первичного индекса и его тег индекса. Поскольку таблица может иметь только один первичный ключ, не требуется указывать имя первичного ключа. Удаление первичного индекса удаляются любые постоянные связей на основе первичного ключа.  
  
 Добавить UNIQUE *eExpression4*[ТЕГ *TagName3*]  
 Добавляет в таблицу индекса кандидатов. *eExpression4* указывает выражение потенциальных ключей индекса, и *TagName3* указывает имя тега индекс кандидатов. Имена тегов индекс может содержать до 10 символов. Если опустить ТЕГ *TagName3* и, если *eExpression4* состоит из одного поля тег индекс кандидат имеет то же имя, как поля, указанного в *eExpression4*.  
  
 DROP УНИКАЛЬНЫЙ ТЕГ *TagName4*  
 Удаляет кандидата индекса и его тег индекса. Поскольку таблица может иметь несколько потенциальных ключей, необходимо указать имя тега индекс кандидатов.  
  
 Добавить внешний ключ [ *eExpression5*] ТЕГ *TagName4*  
 Добавляет в таблицу внешнего (первичному) индекс. *eExpression5* указывает выражение внешнего индекс ключа, и *TagName4* указывает имя тега внешнего индекса. Имена тегов индекс может содержать до 10 символов.  
  
 Ссылки на *TableName2*[ТЕГ *TagName5*]  
 Указывает родительской таблицы, на который устанавливается постоянное связь. Включить ТЕГ *TagName5* для установления отношения зависимости, тег индекса для родительской таблицы. Имена тегов индекс может содержать до 10 символов. Если опустить ТЕГ *TagName5*, связь устанавливается с помощью тега первичного индекса в родительской таблице.  
  
 DROP ВНЕШНЕГО ключа ТЕГА *TagName6*[Сохранить]  
 Удаляет внешний ключ которого индекс тег *TagName6*. При отсутствии СОХРАНЕНИЯ тег индекс удаляется из структуры индекса. Включить СОХРАНЕНИЕ для предотвращения удаления тега индекса из структуры индекса.  
  
 ПЕРЕИМЕНОВАНИЕ СТОЛБЦА *FieldName4*TO *FieldName5*  
 Можно изменить имя поля в таблице. *FieldName4* указывает имя поля, которое будет переименован. *FieldName5* задает новое имя поля.  
  
> [!CAUTION]  
>  Соблюдайте осторожность при переименовании поля таблицы, так как выражения индекса, правила проверки для полей и таблиц, команд и функций могут ссылаться на исходные имена полей.  
  
 NOVALIDATE  
 Указывает, что Visual FoxPro позволяет вносить изменения в структуру таблицы. Эти изменения могут нарушить целостность данных в таблице. По умолчанию Visual FoxPro предотвращает внесение изменений, которые нарушают целостность данных в таблице ALTER TABLE. Включить NOVALIDATE, чтобы переопределить это поведение по умолчанию.  
  
## <a name="remarks"></a>Замечания  
 ALTER TABLE может использоваться для изменения структуры таблицы, который не был добавлен в базу данных. Однако если включают по умолчанию, FOREIGN KEY, PRIMARY KEY, ссылки или предложений SET при изменении свободного таблицы Visual FoxPro возникает ошибка.  
  
 ALTER TABLE может перестроить таблицу, создав новый заголовок таблицы и добавления записей в заголовке таблицы. Например изменения типа или ширина поля может привести к таблице, чтобы перестроить.  
  
 После перестроения таблицы правила проверки для полей, выполняются для всех полей, тип и ширина изменяется. Если изменить тип или ширина любое поле в таблице, выполняется правило таблицы.  
  
 При изменении поля или таблицы правила проверки для таблицы, которая содержит записи, Visual FoxPro проверяет новые поля или таблицы правила проверки относительно существующих данных и выдает предупреждение при первом возникновении правила поля или таблицы, или о нарушении триггера.  
  
 При изменении таблицы в базе данных, инструкция ALTER TABLE - SQL требует монопольного использования базы данных. Чтобы открыть базу данных для монопольного использования, входят ЭКСКЛЮЗИВНОЕ ОТКРОЙТЕ базы данных.  
  
## <a name="see-also"></a>См. также  
 [Создание таблицы - команда SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Команда INDEX](../../odbc/microsoft/index-command.md)
