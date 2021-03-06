---
title: Конфигурации SQL Server для служб R | Документация Майкрософт
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 382b39a7209480f7f02b0cee5d91eb6cbd662cd9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-configuration-for-use-with-r"></a>Конфигурация SQL Server для использования с помощью R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Эта статья является второго ряда, которое описывает оптимизации производительности для служб R, основанных на два исследований.  В этой статье приведены рекомендации по конфигурации оборудования и сети компьютера, который используется для запуска SQL Server R Services. Он также содержит сведения о способах настройки экземпляра SQL Server, базы данных или таблиц, используемых в решении. Так как использование NUMA в SQL Server размывает линии между оптимизации оборудования и базы данных, третий раздел описывает ЦП сопоставить и управление ресурсами подробно.

> [!TIP]
> Если вы не знакомы с SQL Server, настоятельно рекомендуется также изучить руководство по настройке производительности SQL Server: [монитора и настройки производительности](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Оптимизация оборудования

Оптимизации работы сервера важно убедиться, что имеются ресурсы для выполнения внешних скриптов. При ограниченности ресурсов, возможны проблемы такие:

- Выполнение задания отложенного или отменено для приоритетов операций базы данных
- Ошибка «превышено допустимое значение» может вызвать сценарий R завершение без завершения
- Данные загружаются в память R усечен для неполных результатов

### <a name="memory"></a>Память

Объем доступной памяти может иметь значительное влияние на производительность расширенных аналитических алгоритмов. Недостаточно памяти могут повлиять на степень параллелизма, при использовании контекста вычислений SQL. Это также может повлиять на размер фрагмента данных (строк на каждую операцию чтения), который можно обработать, и поддерживаемое число одновременных сеансов.

Настоятельно рекомендуется не менее 32 ГБ. При наличии более чем 32 ГБ, можно настроить источник данных SQL для использования нескольких строк в каждой операции чтения для повышения производительности.

Можно также управлять памяти, используемых экземпляром. По умолчанию SQL Server имеет приоритет над процессы внешнего скрипта при выделении памяти. При установке служб R по умолчанию выделяется только 20% доступной памяти для R.

Обычно это не достаточно для выполнения задач обработки и анализа данных, но ни вы хотите создать препятствия в работе SQL server памяти. Следует поэкспериментировать и оптимизировать выделения памяти между СУБД, связанных служб и внешние сценарии, с учетом, изменяющийся случая оптимальной конфигурации.

Для модели сопоставления resume использования внешнего скрипта было активно и возникли другие базы данных службы ядра СУБД запущен; Таким образом ресурсы, выделенные для внешних скриптов были увеличивается до 70%, который был оптимальные для производительности сценария.

### <a name="power-options"></a>Параметры электропитания

В операционной системе Windows **высокая производительность** питания следует использовать. С помощью параметра различных режима приводит к снижению или нестабильной производительности при использовании SQL Server.

### <a name="disk-io"></a>Дисковые операции ввода-вывода

Обучения и прогнозирования, что задания с помощью служб R по своей природе являются операции ввода-ВЫВОДА привязан и зависят от скорости работы этих дисков, хранящихся на базе данных. Может помочь быстрее дисках, например твердотельных накопителей (SSD).

На дисковые операции ввода-вывода также оказывают влияние и другие приложения, у которых есть доступ к диску, например операции чтения базы данных, выполняемые другими клиентами. На производительность дисковых операций ввода-вывода могут влиять параметры текущей файловой системы, например размер блока, используемый этой системой.

При наличии нескольких дисков баз данных на диске, отличном от SQL Server, который запрашивает для компонента database engine не предназначаются на том же диске, что хранилище запросов для данных, хранящихся в базе данных.

Дисковые операции ввода-вывода могут оказывать значительное влияние на производительность при выполнении аналитических функций RevoScaleR, использующих несколько итераций во время обучения. Например `rxLogit`, `rxDTree`, `rxDForest`, и `rxBTrees` используют несколько итераций. Если источником данных является SQL Server, эти алгоритмы используют временные файлы, которые оптимизированы для сбора данных. Эти файлы автоматически удаляются после завершения сеанса. Наличие на диск высокой производительности для операций чтения и записи может значительно повысить общее прошедшее время для этих алгоритмов.

> [!NOTE]
> Ранние версии служб R требуется 8.3 поддержки filename в операционных системах Windows. Это ограничение была снята после пакета обновления 1. Тем не менее можно использовать fsutil.exe, чтобы определить, поддерживает ли диск 8.3 имена файлов, или для включения поддержки, если это не.

### <a name="paging-file"></a>Файл подкачки

Операционная система Windows использует файл подкачки для управления аварийными дампами и хранения страниц виртуальной памяти. Если обнаружена излишняя подкачка, необходимо увеличить физическую память компьютера. Несмотря на то что больший объем физической памяти не устранит подкачку, это значительно уменьшит потребность в ней.

Скорость диска, на котором хранится файл подкачки, также влияет на производительность. Вы можете улучшить ее, если сохраните файл подкачки на диске SSD или если будете использовать файлы подкачки на нескольких дисках SSD.

Сведения об изменении размера файла подкачки см. в разделе [способ определения соответствующего файла подкачки для 64-разрядных версий Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Оптимизация на уровне экземпляра или базы данных

Оптимизация экземпляра SQL Server является ключом для эффективного выполнения внешних скриптов.

> [!NOTE]
> Оптимальные параметры различаются в зависимости от размера и типа данных, количество столбцов, используемых для оценки или обучения модели.
> 
> Можно просмотреть результаты определенные оптимизации в последней статье: [производительности - пример внедрения результаты настройки](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Образцы скриптов см. в разделе отдельной [репозитории GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Сжатие таблицы

Часто производительность операции ввода-ВЫВОДА можно повысить с помощью сжатия или хранилища данных в один столбец. Как правило часто повторяются данные в несколько столбцов в таблице, поэтому с помощью кластеризованного индекса columnstore использует эти повторов при сжатии данных.

Columnstore не может быть столь же эффективна, если существует множество операций вставки в таблицу, но является хорошим выбором, если статические данные или только редко изменяются. Если хранилище столбцов нельзя использовать по каким-либо причинам, чтобы улучшить операции ввода-вывода, можно включить сжатие для основной таблицы строк.

Дополнительные сведения см. в следующих статьях:

+ [Сжатие данных](../../relational-databases/data-compression/data-compression.md)

+ [Включить сжатие таблицы или индекса](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Руководство по индексам columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Таблицы, оптимизированные для памяти

В настоящее время памяти больше не является проблемой для современных компьютеров. Как характеристики оборудования постоянно совершенствуются, относительно легко получить ОЗУ рекомендуется задать. Тем не менее в то же время данные быстрее, чем раньше создаются и данные должны быть обработаны с низкой задержкой.

Оптимизированные для памяти таблицы представляют одно из решений, в том, что они используют большим объемом памяти, доступное на дополнительных компьютерах решение этой задачи большие наборы данных. Оптимизированные для памяти таблицы находятся в памяти, главным образом, чтобы данные считываются из и записываются в память. Для обеспечения надежности вторая копия таблицы сохраняется на диске и данных только для чтения с диска во время восстановления базы данных.

Если требуется для чтения и записи в таблицы, часто, оптимизированные для памяти таблицы могут помочь с высокой масштабируемостью и малой задержкой.  В случае соответствия возобновить использование таблиц, оптимизированных для памяти, можем считать все возможности возобновления из базы данных и сохранить их в оперативной памяти, в соответствии с новой вакансии. Это значительно уменьшается дисковый ввод-ВЫВОД.

Повышение производительности были реализованы с использованием оптимизированной для памяти таблицы в процессе записи прогнозов обратно в базу данных из нескольких параллельных пакетов. Использование таблиц, оптимизированных для памяти, на сервере SQL Server с поддержкой низкой задержкой в таблице операций чтения и записи.

Процесс был также прозрачную во время разработки. В то же время создания базы данных были созданы устойчивых таблиц, оптимизированных для памяти. Таким образом разработка используется тот же рабочий процесс, независимо от хранения данных.

### <a name="processor"></a>Процессор

SQL Server может выполнять задачи в параллельном режиме с помощью доступных ядер на компьютере; больше ядер, которые доступны, тем выше производительность. При увеличении числа ядер не могут помочь для операций ввода-ВЫВОДА привязаны, ЦП привязан алгоритмы преимущество от более быстрых процессоров с большим количеством ядер.

Так как сервер обычно используется несколькими пользователями одновременно, администратор базы данных необходимо определить оптимальное количество ядер, которые необходимы для поддержки вычисления пиковой рабочей нагрузки.

### <a name="resource-governance"></a>Управление ресурсами

Пулы ресурсов можно использовать в выпусках, поддерживающих регулятор ресурсов, чтобы указать, что некоторых рабочих нагрузок выделение некоторое количество процессоров. Можно также управлять объем памяти, выделенной для конкретных рабочих нагрузок.

Управление ресурсами в SQL Server позволяет централизовать мониторинга и контроля различных ресурсов, используемых SQL Server и R. Например может выделить половина доступной памяти для ядра СУБД, чтобы убедиться, что основные службы всегда могут работать несмотря на временных рабочих нагрузок более сложной.

Значение по умолчанию для внешних скриптов потребление памяти ограничено до 20% от общего объема памяти, доступной для SQL Server. Это ограничение применяется по умолчанию, чтобы убедиться, что все задачи, которые зависят от сервера базы данных, не подвержены важности длительных заданий R. Однако администратор базы данных может изменить эти ограничения. Во многих случаях ограничение 20% недостаточна для поддержки серьезные машинного обучения рабочих нагрузок.

Параметры конфигурации, поддерживаемые являются **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, и **MAX_PROCESSES**. Чтобы просмотреть текущие параметры, используйте эту инструкцию: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Если сервер в основном используется для служб R, рекомендуется увеличить MAX_CPU_PERCENT до 40% или 60%.

-  Если несколько сеансов R должен использовать тот же сервер, в то же время, все три параметра должно быть увеличено.

Чтобы изменить параметры выделенных ресурсов, используйте инструкции T-SQL.

+ Эта инструкция задает использование памяти на 40%: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Эта инструкция задает все три настраиваемых значений: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Если изменить память, ЦП или параметр max процесс и затем следует немедленно применить параметры, выполните следующую инструкцию: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Соответствие программной архитектуры NUMA, оборудования NUMA и Процессора

При использовании SQL Server в контексте, иногда можно улучшить производительность путем настройки параметров, относящихся к NUMA и соответствие процессора. 

В системах с _оборудования NUMA_ имеют несколько системных шин, каждая из которых обслуживает небольшую группу процессоров. Каждый ЦП может обращаться к памяти, связанной с другими группами согласованным образом. Каждая группа называется узлом NUMA. Если имеется оборудование NUMA, оно может быть настроено так, что вместо NUMA используется чередующаяся память. В этом случае Windows и, следовательно, SQL Server не распознает его как NUMA. 

Можно выполнить следующий запрос, чтобы найти количество узлов памяти, доступной для SQL Server:

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Если запрос возвращает один узел памяти (узел 0), либо не имеет оборудования NUMA, либо оборудование настроено как с чередованием (не NUMA). SQL Server также игнорирует оборудования NUMA при существует четыре или меньшее число процессоров или если по крайней мере на одном узле находится только один ЦП.

Если на компьютере установлено несколько процессоров, но не имеет оборудования NUMA, можно также использовать [программной архитектуры NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) для разделения процессоров на более мелкие группы.  В SQL Server 2016 и 2017 г. SQL Server компонент программной архитектуры NUMA включается автоматически при запуске службы SQL Server.

При программной архитектуры NUMA включена, SQL Server автоматически управляет узлов Тем не менее, чтобы оптимизировать для конкретных рабочих нагрузок, можно отключить _нежесткой привязке_ и вручную настроить сходство ЦП в узлы NUMA мягкой. Это поможет вам больше возможностей управления, по которому рабочих нагрузок назначены какие узлы, особенно в том случае, если используется выпуск SQL Server, который поддерживает управление ресурсами. Задание соответствия Процессоров и выравнивание пулов ресурсов с группами процессоров, можно уменьшить задержку и убедитесь, что связанные процессы выполняются в том же узле NUMA.

Общий процесс настройки программной архитектуры NUMA и процессоров для поддержки рабочих нагрузок R выглядит следующим образом:

1. Включить программной архитектуры NUMA, если он доступен
2. Определить соответствие процессоров
3. Создание пулов ресурсов для внешних процессов, с помощью [регулятора ресурсов](../r/resource-governance-for-r-services.md)
4. Назначьте [группы рабочей нагрузки](../../relational-databases/resource-governor/resource-governor-workload-group.md) для конкретных Территориальные группы

Сведения, включая пример кода см. в этом учебнике: [SQL оптимизации советы и рекомендации (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Другие ресурсы:**

+ [Программная архитектура NUMA в SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Как соответствия программной архитектуры NUMA нескольким процессорам

+ [Автоматический режим программной NUMA: он просто выполняется быстрее (Bob Ворд)](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   Описывает журнал и сведения о реализации, с производительностью на более новых серверах для многоядерных процессоров.

## <a name="task-specific-optimizations"></a>Оптимизация для конкретных задач

В этом разделе приведена сводка методов, что существует в эти примеры, а также в других тестах по оптимизации конкретных машинного обучения рабочих нагрузок. Общие рабочие нагрузки включают обучение модели, возможность извлечения и конструируются и различные сценарии для оценки: одной строки, небольшой пакет и большого пакета.

### <a name="feature-engineering"></a>Формирование признаков

Один усложняют с помощью R — обычно обработки на один ЦП. Это является узким местом производительности основных для многих задач, особенно компонентов техническим специалистам. В решении соответствия resume только задачи разработки компонента создан 2500 перекрестного произведения функции, которые пришлось вместе со средствами исходного 100. Эта задача может потребоваться значительное время, если все, что было выполнено на один ЦП.

Для повышения производительности конструируются несколькими способами. Можно оптимизировать код R и сохранить возможность извлечения внутри процесса моделирования или переместите процессом разработки компонентов в SQL.

- С помощью языка R. Определить функцию и передайте его в качестве аргумента для [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) во время обучения. Если модель поддерживает параллельную обработку, задачи разработки компонента могут быть обработаны с помощью нескольких процессоров. При таком подходе команды обработки и анализа данных наблюдается повышение производительности 16% с точки зрения времени оценки. Однако этот подход требует модель, которая поддерживает параллелизации, а также запрос, могут выполняться с использованием параллельных планов.

- Использование R с помощью SQL контекста вычислений. В многопроцессорной среде с изолированной ресурсы, доступные для выполнения отдельных пакетов можно добиться большей эффективности, изолируя запросов SQL, используемых для каждого пакета для извлечения данных из таблиц и ограничения данных в одной группе рабочей нагрузки. Методы, используемые для изоляции пакетов включить секционирование и используется PowerShell для параллельного выполнения отдельных запросов.

- Ad hoc параллельного выполнения: контекст вычислений в SQL Server, вы можете использовать ядро СУБД SQL для обеспечения возможности параллельного выполнения, и если найден соответствующий параметр для повышения эффективности.

- Используйте T-SQL в процессе, отдельном featurization. Precomputing данные с помощью SQL обычно используется быстрее.

### <a name="prediction-scoring-in-parallel"></a>Прогноз (оценки), в параллельном режиме

Одно из преимуществ использования SQL Server является возможность обрабатывать большое количество строк в параллельном режиме. Ничто это преимущество соответствующим образом отмечены как оценки. Обычно модели не требуется доступ ко всем данным для оценки, так можно секционировать с каждой группой рабочей нагрузки, одна задача обработки входных данных.

Можно также отправлять входные данные как отдельный запрос, и SQL Server затем анализирует запрос. При параллельном плане запроса могут быть созданы для входных данных, он автоматически секции данных, назначенные узлов и параллельно также выполняет необходимые соединения и статистические вычисления.

Если вы заинтересованы в сведениях о определения хранимой процедуры для использования при оценке, см. раздел примера проекта на [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) и найдите файл «step5_score_for_matching.sql». Образец также отслеживает Начало запроса и время окончания и скрипта записывает время консоль SQL, чтобы можно было оценить производительность.

### <a name="concurrent-scoring-using-resource-groups"></a>Параллельные оценки с помощью групп ресурсов

Позволяет масштабировать оценки проблему, рекомендуется применять MAP-Reduce подход, в котором миллионы элементов разделяются на несколько пакетов. Затем несколько оценки заданий выполняются одновременно. В этой платформе пакеты, обрабатываются на разных наборах ЦП, и результаты собираются и записываются в базу данных.

Этот подход используется в сценарии resume сопоставления; Тем не менее управление ресурсами в SQL Server необходима для реализации этого метода. С помощью настройки группы рабочей нагрузки для внешних скриптов с заданиями, можно направлять оценок для разных процессоров заданий R и добиться более высокую пропускную способность.

Управление ресурсами также может помочь выделить разделить доступные ресурсы на сервере (ЦП и память), чтобы свести к минимуму конкуренции рабочей нагрузки. Можно настроить функции-классификаторы, чтобы отличать различные типы заданий R: например, можно решить, оценки, вызываемой из приложения всегда имеет приоритет, пока цикл задания имеют низкий приоритет. Эта изоляция ресурсов потенциально можно сократить время выполнения и обеспечить более предсказуемую производительность.

### <a name="concurrent-scoring-using-powershell"></a>Параллельные вычисления с помощью PowerShell

Если вы решили самостоятельно секционировать данные, выполнять несколько параллельных задач оценки можно использовать скрипты PowerShell. Чтобы сделать это, используйте командлет Invoke-SqlCmd и инициировать задач оценки в параллельном режиме.

В случае соответствия resume параллелизма была разработана следующим образом:

- 20 процессоров разделяются на четыре группы пять ЦП. Каждой группе процессоров находится на том же узле NUMA.

- Максимальное количество параллельных пакетов было задано значение 8.

- Каждая группа рабочей нагрузки необходимо выполнять задачи оценки. Как только одна задача завершения чтения данных и оценки начинается другая задача можно запустить, чтение данных из базы данных.

Для просмотра скриптов PowerShell для этого сценария, откройте experiment.ps1 файл в [Github проекта](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Сохранение модели для прогнозирования

После обучения и оценки завершается и выбраны лучшую модель, рекомендуется хранить модели в базе данных, чтобы он был доступен для прогнозов. Загрузка предварительно вычисленных модели из базы данных для прогноза эффективна, так как SQL Server машинного обучения использует алгоритмы специальные сериализации для сохранения и загрузки модели при перемещении между R и базы данных.

> [!TIP]
> В SQL Server 2017 г можно использовать функцию ПРОГНОЗИРОВАНИЯ для выполнения оценки, даже если R не установлен на сервере. Поддерживаются только модели типов из пакета RevoScaleR.

Тем не менее в зависимости от алгоритма, используемого, некоторые модели может быть достаточно большим, особенно в том случае, если обучена на большой набор данных. Например, алгоритмы, такие как **lm** или **glm** создавать большое число сводных данных вместе с правилами. Существуют ограничения на размер модели, которые могут храниться в столбце varbinary, поэтому рекомендуется исключить ненужные артефакты из модели перед сохранением в базе данных для производства модели.

## <a name="articles-in-this-series"></a>Статьи в этой серии

[Производительность помощник по настройке для R — введение](../r/sql-server-r-services-performance-tuning.md)

[Настройка производительности для R - конфигурации SQL Server](../r/sql-server-configuration-r-services.md)

[Настройка производительности для R - R оптимизации кода и данных](../r/r-and-data-optimization-r-services.md)

[Помощник по настройке производительности - пример использования результатов](../r/performance-case-study-r-services.md)
