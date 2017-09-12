---
title: "Подготовка данных с помощью PowerShell (Пошаговое руководство) | Документы Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1d85684da36ef69caf9dfa39f155a320def37b5
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>Подготовка данных с помощью PowerShell (Пошаговое руководство)

К этому времени должны иметь одно из следующих:

+ SQL Server 2016 R Services
+ Службы SQL Server 2017 г машины обучения, с помощью языка r. включена

На этом занятии вы загрузите данные, пакеты R и R-скриптов, используемые в руководстве из репозитория Github. Вы можете загрузить все содержимое с помощью сценария PowerShell для удобства.

Необходимо также установить некоторых дополнительных пакетов R на рабочей станции R и на сервере. Описаны шаги.

Затем второй сценарий PowerShell, RunSQL_R_Walkthrough.ps1, используется для настройки базы данных, который используется для моделирования и оценки. Что сценарий выполняет массовую загрузку данных в базу данных можно указать, а затем создает некоторые функции SQL и хранимых процедур, которые упрощают задачи обработки и анализа данных.

Давайте начнем!

## <a name="1-download-the-data-and-scripts"></a>1. Загрузка данных и сценариев

Весь необходимый код предоставляется в репозитории GitHub. Скрипт PowerShell можно использовать для создания локальной копии файлов.

1.  На компьютере с клиентом обработки и анализа данных откройте командную строку Windows PowerShell с правами администратора.

2.  Чтобы при выполнении скачанного скрипта не возникали ошибки, выполните приведенную ниже команду. Она временно разрешает выполнять скрипты, не меняя параметры системы по умолчанию.

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  Чтобы скачать файлы скриптов в локальный каталог, выполните приведенную ниже команду Powershell. Если вы не укажете другой каталог, по умолчанию папке `C:\tempR` создается и все файлы сохраняются.
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    Если нужно сохранить файлы в другом каталоге, измените значения параметра *DestDir* и укажите папку на компьютере. Если ввести имя папки, которая не существует, сценарий PowerShell создает папку.
  
4.  Скачивание может занять некоторое время. По завершении скачивания командная консоль Windows PowerShell должна выглядеть следующим образом:
  
    ![После выполнения скрипта PowerShell](media/rsql-e2e-psscriptresults.PNG "После выполнения скрипта PowerShell")
  
5.  В консоли PowerShell выполните команду `ls` , чтобы просмотреть список файлов, скачанных в каталог *DestDir*.  Описание файлов см. в разделе [содержимое](#What-the-Download-Includes).

## <a name="2-install-required-r-packages"></a>2. Установить необходимые пакеты R

Для работы с этим пошаговым руководством требуется ряд библиотек R, которые по умолчанию не устанавливаются вместе с [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Необходимо установить оба пакетов на стороне клиента которой разработки решения, а также на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] компьютере, где вы развертываете решение.

### <a name="install-required-packages-on-the-client"></a>Установка необходимых пакетов на клиентском компьютере

Скачанный скрипт R содержит команды для скачивания и установки этих пакетов.

1. В среде R откройте файл скрипта RSQL_R_Walkthrough.R.

2. Выделите и выполните следующие строки:
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    Некоторые пакеты также установить необходимые пакеты. Всего требуется около 32 пакетов.

### <a name="install-required-packages-on-the-server"></a>Установка необходимых пакетов на сервере

Существует множество различных способов, необходимо установить пакеты на сервере SQL Server. Например, SQL Server предоставляет [пакета управления](../r/installing-and-managing-r-packages.md) функция, которая позволяет администраторам баз данных создайте репозитория пакетов и назначьте пользователя прав для установки собственных пакетов. Тем не менее если вы являетесь администратором на компьютере, можно установить новые пакеты, с помощью R, при условии, что установка в правильную библиотеку.

> [!NOTE]
> На сервере **не** установить библиотеку пользователя даже при появлении соответствующего запроса. При установке в библиотеке пользователя экземпляра SQL Server не удается найти или запускать пакеты. Дополнительные сведения см. в статье [Installing New R Packages on SQL Server](../r/install-additional-r-packages-on-sql-server.md)(Установка новых пакетов R в SQL Server).

1. На компьютере [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] откройте программу RGui.exe **от имени администратора**.  Если вы установили службы SQL Server R Services с настройками по умолчанию, программу RGui.exe можно найти в папке C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64.

2.  В командной строке R выполните следующие команды R:
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - В этом примере используется функция R grep для поиска вектора доступных путей и нахождения пути в каталоге Program files. Дополнительные сведения см. на странице [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep).

    - Если вы считаете, что пакеты уже установлены, проверьте список установленных пакетов с `installed.packages()`.

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3. Подготовка среды с помощью RunSQL_R_Walkthrough.ps1

И файлы данных, R-скриптов и скриптов T-SQL, загружаемый файл содержит скрипт PowerShell `RunSQL_R_Walkthrough.ps1`. Скрипт выполняет следующие действия:

- проверяет установлен ли клиент SQL Native Client и программы командной строки для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; Программы командной строки необходимы для запуска [служебной программы bcp](../../tools/bcp-utility.md), которая служит для быстрой массовой загрузки данных в таблицы SQL;

- подключается к указанному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и выполняет ряд скриптов [!INCLUDE[tsql](../../includes/tsql-md.md)] , которые настраивают базу данных и создают таблицы для модели и данных;

- выполняет скрипт SQL для создания нескольких хранимых процедур;

- загружает данные, которые вы скачали ранее, в таблицу с именем `nyctaxi_sample`;

- перезаписывает аргументы в файле скрипта R так, чтобы использовалось указанное имя базы данных.

Необходимо запустить этот сценарий на компьютере, где построения решения: например, ноутбуке, где разработки и тестирования кода R. Компьютер с клиентом обработки и анализа данных должен подключаться к компьютеру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью протокола именованных каналов.

1. Откройте командную строку PowerShell **администратор**.
  
2.  Перейдите в папку, в которую вы скачали скрипты, и введите имя скрипта, как показано ниже. Нажмите клавишу ВВОД.

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3.  Появится для каждого из следующих параметров:
  
    **Имя сервера базы данных**: имя экземпляра SQL Server, установленным машинного обучения, служб или служб R.

    В зависимости от требований сети для имени экземпляра может требоваться одно или несколько имен подсетей в качестве квалификатора.  Например, если MYSERVER не подходит, попробуйте myserver.subnet.mycompany.com.
    
    **Имя базы данных, которую вы хотите создать.** Например, вы можете ввести **Tutorial** или **Taxi**.

    **Имя пользователя.** Укажите учетную запись с правами доступа к базам данных. Имеются две возможности:
    
    + Введите имя входа SQL с правами CREATE DATABASE и введите пароль SQL при последующем запросе.
    + Нажмите клавишу ВВОД, но не вводите имя, чтобы использовалось ваше собственное удостоверение Windows, а в защищенной строке введите пароль Windows. В PowerShell не поддерживается ввод другого имени пользователя Windows.
    + Если не указать допустимого пользователя, сценарий по умолчанию использует встроенную проверку подлинности Windows.
    
      > [!WARNING]
      > При использовании строки в сценарии PowerShell для предоставления учетных данных пароля записывается в файл обновленный скрипт в виде обычного текста. Удалите учетные данные из файла сразу же после создания необходимых объектов R.
      
    **Путь к CSV-файлу.** Укажите полный путь к файлу данных. По умолчанию путь и имя файла — `C:\tempR\nyctaxi1pct.csv1`.
  
4.  Чтобы запустить скрипт, нажмите клавишу ВВОД.

    Скрипт должен автоматически скачать файл и загрузить данные в базу данных. Это может занять некоторое время. Следите за сообщениями о состоянии в окне PowerShell.
      
    При массовом импорте данных или других происходит сбой шаг, можно загрузить данные вручную, как описано в [Устранение неполадок](#bkmk_Troubleshooting) раздела.

**Результаты (успешное завершение)**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

Щелкните эту ссылку, чтобы перейти к следующему занятию: [представление и просматривать данные, используя SQL](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>Устранение неполадок

Если у вас возникнут проблемы с помощью скрипта PowerShell, можно выполнить все или любые действия вручную, нажав строк сценария PowerShell в качестве примеров. В этом разделе перечислены некоторые распространенные проблемы и обходные пути.

### <a name="powershell-script-didnt-download-the-data"></a>Скрипт PowerShell не скачал данные

Чтобы скачать данные вручную, щелкните приведенную ниже ссылку правой кнопкой мыши и выберите пункт **Сохранить объект как**.

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

Запомните путь к скачанному файлу данных и его имя. Требуется полный путь для загрузки данных в таблицу с помощью **bcp**.

### <a name="unable-to-download-the-data"></a>Не удалось скачать данные

Файл данных имеет большой размер. Необходимо использовать компьютер, который имеет довольно хорошо подключение к Интернету или загрузки время ожидания может истечь.

### <a name="could-not-connect-or-script-failed"></a>Не удалось подключиться, или выполнение скрипта завершается сбоем

При выполнении одного из скриптов может появиться следующая ошибка: *При установлении соединения с сервером SQL Server произошла ошибка, связанная с сетью или с определенным экземпляром*.

+ Проверьте правильность написания имени экземпляра.
+ Проверьте всю строку подключения.
+ В зависимости от требований сети для имени экземпляра может требоваться одно или несколько имен подсетей в качестве квалификатора.  Например, если MYSERVER не подходит, попробуйте myserver.subnet.mycompany.com.
+ Проверьте, разрешает ли брандмауэр Windows подключения от SQL Server.
+ Зарегистрируйте сервер и настройте разрешение удаленных подключений.
+ Если вы используете именованный экземпляр, включите обозреватель SQL, чтобы упростить подключения.

### <a name="network-error-or-protocol-not-found"></a>Ошибка сети, или не найден протокол

+ Проверьте, поддерживает ли экземпляр удаленные подключения.
+ Проверьте, может ли указанный пользователь SQL удаленно подключиться к базе данных.
+ Включите именованные каналы в экземпляре.
+ Проверьте разрешения, назначенные учетной записи. Указанная учетная запись может не иметь разрешений на создание базы данных и отправку данных.

### <a name="bcp-did-not-run"></a>Не удалось запустить bcp

+ Проверьте, есть ли на компьютере [служебная программа bcp](../../tools/bcp-utility.md) . Вы можете запустить программу **bcp** из окна PowerShell или командной строки Windows.
+ Если произошла ошибка, добавьте расположение служебной программы **bcp** в системную переменную среды PATH и повторите попытку.

### <a name="the-table-schema-was-created-but-the-table-has-no-data"></a>Схема таблицы создана, но в таблице нет данных

Если остальная часть скрипта выполнена без проблем, можно отправить данные в таблицу вручную, вызвав программу **bcp** из командной строки следующим образом:

#### <a name="using-a-sql-login"></a>Использование имени входа SQL

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password>
~~~~

#### <a name="using-windows-authentication"></a>Использование проверки подлинности Windows

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T
~~~~

+ `in` Ключевое слово указывает направление перемещения данных.
+ Для аргумента  **-f** необходимо указать полный путь к файлу форматирования. Файл форматирования необходим при использовании параметра **in** .
+ Используйте аргументы **-u** и **-p** при запуске служебной программы bcp с именем входа SQL.
+ Если используется встроенная проверка подлинности Windows, используйте аргумент **-t** .

Если данные с помощью скрипта не загружаются, проверьте синтаксис. Также проверьте, верно ли указано имя сервера для сети. Например, не забудьте указать необходимые подсети, а также имя компьютера в случае подключения к именованному экземпляру. Убедитесь, что имя входа имеет возможность выполнения массовой передачи.

### <a name="i-want-to-run-the-script-without-prompts"></a>Скрипт должен выполняться без вывода запросов

Вы можете указать все параметры в одной командной строке, используя шаблон ниже, со значениями, принятыми в вашей среде.

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

В примере ниже скрипт запускается с помощью имени входа SQL.

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   подключается к указанным экземпляру и базе данных с использованием учетных данных пользователя *SqlUserName*;
-   получает данные из файла *C:\temp\nyctaxi1pct.csv*;
-   скачивает данные в таблицу *dbo.nyctaxi_sample*базы данных *MyDB* в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с именем *MyServer*.

### <a name="the-data-loaded-but-it-contains-duplicates"></a>Данные скачаны, но содержат повторяющиеся элементы

Если в базе данных в существующую таблицу с одинаковым именем и той же схеме, **bcp** вставляет новую копию данных, а не перезаписывают существующие данные.

Чтобы избежать повторяющихся данных, необходимо усечь все имеющиеся таблицы перед повторным запуском скрипта.

## <a name="whats-included-in-the-sample"></a>Что входит в образце

При загрузке файлов из репозитория GitHub, вы получите следующие:

+ Данные в формате CSV. в разделе [обучения и оценки данных](#bkmk_data) подробные сведения
+ скрипт PowerShell для подготовки среды;
+ XML-файл форматирования для импорта данных в SQL Server с помощью программы bcp;
+ несколько скриптов T-SQL;
+ весь код R, необходимый для выполнения действий, описанных в этом пошаговом руководстве.

### <a name="bkmk_data"></a>Обучение и оценки данных

Данные представляют собой представительную выборку из набора данных по работе такси в Нью-Йорке, который содержит записи о более чем 173 миллионах отдельных поездок в 2013 году, включая сведения о размере оплаты и чаевых за каждую поездку. Чтобы с этими данными было проще работать, команда Майкрософт по обработке и анализу данных произвела выборку приблизительно 1 % из всего набора.  Эти данные были помещены в общедоступный контейнер хранилища BLOB-объектов в Azure в формате CSV. Исходные данные представляют собой несжатый файл размером немного менее 350 МБ.

+ Открытый набор данных: [такси NYC и Limousine Commission] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [Построение моделей машинного Обучения Azure в наборе данных такси NYC] (https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/.

### <a name="powershell-and-r-script-files"></a>Файлы скриптов PowerShell и R

+ **RunSQL_R_Walkthrough.ps1** запуска этого сценария сначала с помощью PowerShell. Он вызывает скрипты SQL для загрузки данных в базу данных.

+ **taxiimportfmt.xml** — файл определения формата, который используется служебной программой bcp для загрузки данных в базу данных.

+ **RSQL_R_Walkthrough.R** это основной R сценарий, который используется в остальной части занятия для выполнения данных для анализа и моделирования. Он предоставляет весь необходимый код R для изучения данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , создания модели классификации и построения графиков.

### <a name="t-sql-script-files"></a>Файлы скриптов T-SQL

При выполнении сценария PowerShell несколько [!INCLUDE[tsql](../../includes/tsql-md.md)] сценариев на экземпляре SQL Server. В следующей таблице перечислены [!INCLUDE[tsql](../../includes/tsql-md.md)] сценариев и их функции.

|Имя файла скрипта SQL|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|Создает базу данных и две таблицы:<br /><br /> *nyctaxi_sample:*таблица, в которой хранятся данные для обучения — выборка из набора данных по работе такси в Нью-Йорке. К таблице добавляется кластеризованный индекс columnstore для оптимизации хранения данных и производительности запросов.<br /><br /> *nyc_taxi_models:*пустая таблица, которая будет использоваться в дальнейшем для сохранения обученной модели классификации.|
|PredictTipBatchMode.sql|Создает хранимую процедуру, которая вызывает обученную модель с целью прогнозирования меток для новых наблюдений. В качестве входного параметра она принимает запрос.|
|PredictTipSingleMode.sql|Создает хранимую процедуру, которая вызывает обученную модель классификации с целью прогнозирования меток для новых наблюдений. Переменные новых наблюдений передаются в процедуру в виде встроенных параметров.|
|PersistModel.sql|Создает хранимую процедуру, которая позволяет сохранять двоичное представление модели классификации в таблице базы данных.|
|fnCalculateDistance.sql|Создает скалярную функцию SQL, которая вычисляет прямое расстояние между местами посадки и высадки.|
|fnEngineerFeatures.sql|Создает функцию SQL с табличным значением, которая создает функции для обучения модели классификации.|

Запросов T-SQL, используемых в этом пошаговом руководстве были протестированы и могут выполняться как-находится в коде R. Однако если вы хотите дополнительно поэкспериментировать с ними или разработать собственное решение, мы рекомендуем использовать выделенную среду разработки SQL для предварительного тестирования и настройки запросов перед их добавлением в код R.

+ [Расширение mssql](https://code.visualstudio.com/docs/languages/tsql) для [кода Visual Studio](https://code.visualstudio.com/) является бесплатной упрощенной средой для выполнения запросов, поддерживающей большинство задач разработки базы данных.
+ [Среда SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) — это мощное бесплатное средство для разработки баз данных SQL Server и управления ими.

## <a name="next-lesson"></a>Следующее занятие

[Просмотр и изучение данных с помощью SQL и R](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>Предыдущее занятие

[Пошаговое руководство обработки и анализа данных с начала до конца R и SQL Server](/walkthrough-data-science-end-to-end-walkthrough.md)

[Предварительные требования для данного пошагового руководства обработки и анализа данных](walkthrough-prerequisites-for-data-science-walkthroughs.md)
