---
title: Настройка подключения к PolyBase - система платформы аналитики | Документы Microsoft
description: В этой статье описывается настройка PolyBase в параллельное хранилище данных для подключения к внешней Hadoop или Microsoft Azure BLOB-объектов источников данных службы хранилища. Для выполнения запросов, объединяющие данные из нескольких источников, включая Hadoop, хранилище больших двоичных объектов и параллельного хранилища данных с помощью PolyBase.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d87ea2b126fde6bf0b18f7a777216f04d45d98f6
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
---
# <a name="configure-polybase-connectivity-to-external-data"></a>Настройка подключения к PolyBase для внешних данных
В этой статье описывается настройка PolyBase в параллельное хранилище данных для подключения к внешней Hadoop или Microsoft Azure BLOB-объектов источников данных службы хранилища. Для выполнения запросов, объединяющие данные из нескольких источников, включая Hadoop, хранилище больших двоичных объектов и параллельного хранилища данных с помощью PolyBase.  
  
### <a name="to-configure-connectivity"></a>Для настройки подключения  
  
1.  Откройте средство формирования запросов, например sqlcmd или SQL Server Data Tools (SSDT) и запустите хранимую процедуру sp_configure, чтобы просмотреть текущие параметры 'hadoop connectivity'.  
  
    ![параметр подключения hadoop](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Решите, какой параметр, нужно ли изменить текущие настройки, а также подключение Hadoop. Этот параметр применяется к всей области SQL Server PDW. Полный список параметров конфигурации и версий см. в разделе [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
3.  Чтобы изменить параметр 'hadoop connectivity', запустите хранимую процедуру sp_configure с RECONFIGURE. Ниже приведены некоторые примеры.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP), HDInsight on Analytics Platform System, or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    Выполнение хранимой процедуры sp_configure RECONFIGURE задает значение параметра конфигурации. Перезапуск области требуется присвоить это значение. Поскольку требуется перезагрузка после остановки Далее также, выполните перезагрузку до и после следующего шага, изменяющий core-site.xml не нужно.  
  
4.  Чтобы включить хранилище больших двоичных объектов Microsoft Azure в качестве внешнего источника данных, добавьте один или несколько ключей доступа Microsoft Azure хранилища учетных записей PDW core-site.xml файл. Чтобы добавить раздел:  
  
    1.  Найти имя учетной записи хранилища Microsoft Azure. Чтобы просмотреть учетные записи хранения, имя входа для[портал Azure](https://portal.azure.com) и нажмите кнопку **учетные записи хранения (классические)**.  
  
        ![Имя учетной записи хранилища Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Найти ключ доступа учетной записи хранилища Azure. Для этого щелкните имя вашей учетной записи хранилища, в колонке параметров щелкните **ключей**. Вы увидите имя и хранилища ключей учетной записи.  
  
        ![Ключи доступа к учетной записи хранилища Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  Открытие удаленного рабочего стола для узла управления PDW.  
  
    4.  Откройте файл C:\Program Files\Microsoft SQL Server параллельных данных Warehouse\100\Hadoop\conf\core-site.xml.  
  
    5.  Добавьте следующее свойство с именем и значением атрибутами core-site.xml.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        В этом примере использует имя и ключ учетной записи доступа показано ранее.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Прежде чем сохранить ключ доступа в core-site.xml примите меры предосторожности. Любой пользователь, имеющий разрешение CONTROL SERVER или ALTER ANY EXTERNAL DATA SOURCE можно создать источник внешних данных, который получает доступ к этой учетной записи. После создания внешнего источника данных SQL Server PDW все пользователи, имеющие разрешения CREATE TABLE можно создать внешнюю таблицу, которая обращается к этой учетной записи хранения. Пользователей можно получить доступ к данным учетной записи и потребляют ресурсы в учетной записи.  
  
    6.  Сохраните изменения core-site.xml.  
  
5.  Добавление в файл yarn-site.xml yarn.application.classpath свойства и значения.  
  
    При подключении внешнего 1.3 Hadoop, пропустите этот шаг.  
  
    Начиная с версии 2.0 Hadoop, yarn-site.xml-файл содержит параметры конфигурации для Hadoop YARN framework. Этот файл находится на узле управления **C:\program files\Microsoft SQL Server параллельных данных Warehouse\100\Hadoop\conf\\**.  
  
    Для выполнения запросов PolyBase внешних кластера Hadoop 2.0 в Windows или Linux, необходимо настроить yarn.application.classpath и значения для согласования с параметрами yarn-site.xml на внешних кластера Hadoop. Эта конфигурация необходима, даже если внешний кластер Hadoop использует параметры по умолчанию.  
  
    Пример настройки по умолчанию.  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    После определения любое свойство в yarn-site.xml PolyBase используются новые значения свойств при выполнении запросов к области HDInsight. Если вы планируете выполнять запросы PolyBase к область HDInsight и внешних кластера Hadoop 2.0 в Windows, должно быть согласованность всех файлов yarn-site.xml, иначе запросы PolyBase завершится ошибкой.  
  
    Чтобы запустить PolyBase область HDInsight и внешних 2.0 кластера Hadoop, используйте параметры по умолчанию yarn-site.xml на внешних кластера Hadoop.  
  
6.  Перезапустите регион PDW. Чтобы сделать это, используйте средство Configuration Manager. В разделе [запустите диспетчер конфигурации &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
7.  Проверьте параметры безопасности для подключений Hadoop. Если **слабая проверка подлинности** в Hadoop стороне включен с помощью `dfs.permission = true`, необходимо создать пользователя Hadoop **pdw_user** и предоставьте полный доступ для чтения и разрешения на запись для этого пользователя. SQL Server PDW и соответствующие вызовы из SQL Server PDW всегда выдается как **pdw_user**.  — Имя основного пользователя и не может изменяться в этой версии подключения к Hadoop и выпуска SQL Server PDW. При отключенной безопасности в Hadoop с помощью `dfs.permission = false`, а затем нужно принимать никаких дальнейших действий.  
  
8.  Решите, какие пользователи могут создавать внешнего источника данных в хранилище больших двоичных объектов Microsoft Azure. Предоставьте каждого пользователя, имя учетной записи хранилища, а также **ALTER ANY EXTERNAL DATA SOURCE** или **CONTROL SERVER** разрешение.  
  
9. Для подключений Hadoop решите, какие пользователи могут создавать внешнего источника данных в Hadoop. Присвойте каждого пользователя IP-адрес и порт номер каждого имени узла Hadoop и дать им **ALTER ANY EXTERNAL DATA SOURCE** или **CONTROL SERVER** разрешение.  
  
10. Также для подключения к WASB требуется пересылки DNS настроены на устройстве. Настройка пересылки DNS, в разделе [использовать DNS-сервер пересылки для разрешения DNS-имена устройств не &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
Авторизованные пользователи теперь можно создать внешние источники данных, внешние форматы файлов и внешних таблиц. Их можно использовать для интеграции данных из нескольких источников, включая Hadoop, хранилище больших двоичных объектов Microsoft Azure и SQL Server PDW.  

## <a name="kerberos-configuration"></a>Конфигурация Kerberos  
Обратите внимание, что при PolyBase проходит проверку подлинности Kerberos защищенного кластера, параметр hadoop.rpc.protection должно быть присвоено проверки подлинности. При этом обмен данными между узлами Hadoop остается в незашифрованном виде. 

 Для подключения к защищенным с помощью Kerberos кластеру [с помощью MIT KDC]:
   
  
1.  Найдите каталог конфигурации Hadoop в каталоге установки на узле управления:  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  Найдите значение конфигурации для ключей конфигурации, перечисленных в таблице, на компьютере с Hadoop. (Найдите файлы в каталоге конфигурации Hadoop на этом же компьютере.)  
  
3.  Скопируйте значения конфигурации в свойство value соответствующих файлов на узел элемента управления.  
  
    |**#**|**Файл конфигурации**|**Ключ конфигурации**|**Действие**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Укажите имя узла KDC. Например, kerberos.your-realm.com|  
    |2|core-site.xml|polybase.kerberos.realm|Укажите область Kerberos. Например, YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|Найдите конфигурацию для Hadoop и скопируйте ее на компьютер с SQL Server. Например, KERBEROS<br></br>**Примечание о безопасности:** слово KERBEROS должно быть написано прописными буквами. При использовании строчных букв функция может не включиться.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Найдите конфигурацию для Hadoop и скопируйте ее на компьютер с SQL Server. Например: hdfs/_HOST@YOUR-REALM.COM.|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Найдите конфигурацию для Hadoop и скопируйте ее на компьютер с SQL Server. Например: mapred/_HOST@YOUR-REALM.COM.|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Найдите конфигурацию для Hadoop и скопируйте ее на компьютер с SQL Server. Например, 10.193.26.174:10020|  
    |7|yarn-site.xml yarn|yarn.resourcemanager.principal|Найдите конфигурацию для Hadoop и скопируйте ее на компьютер с SQL Server. Например: yarn/_HOST@YOUR-REALM.COM.|  
  
4. Создайте объект учетных данных для базы данных, чтобы указать аутентификационные сведения для каждого пользователя Hadoop. См. статью [Объекты T-SQL PolyBase](../relational-databases/polybase/polybase-t-sql-objects.md).  

5. Перезапустите регион PDW. Чтобы сделать это, используйте средство Configuration Manager. В разделе [запустите диспетчер конфигурации &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).
 
## <a name="see-also"></a>См. также  
[Конфигурация устройства &#40;система платформы аналитики&#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
