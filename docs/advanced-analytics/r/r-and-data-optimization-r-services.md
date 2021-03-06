---
title: Производительность служб SQL Server R - оптимизация данных | Документы Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5a30ff30651bacde42c60a1e0b265105e3c932e3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2018
ms.locfileid: "34563762"
---
# <a name="performance-for-r-services---data-optimization"></a>Производительность служб R - оптимизация данных
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Эта статья является третий ряда, которое описывает оптимизации производительности для служб R, основанных на два исследований. В этой статье описывается оптимизация производительности для R или Python сценариев, которые выполняются в SQL Server. Он также описывает методы, которые можно использовать для обновления кода R, чтобы избежать известных проблем и для повышения производительности.

## <a name="choosing-a-compute-context"></a>Выбрав контекст вычислений.

В SQL Server 2016 и 2017 г., можно использовать **локального** или **SQL** контекста вычислений при выполнении сценария R или Python.

При использовании **локального** контекст вычислений, анализ выполняется на компьютере, а не на сервере. Таким образом при получении данных из SQL Server для использования в коде, необходимо извлечь данные по сети. Снижение производительности, вызванное такой передачей по сети, зависит от объема передаваемых данных, скорости сети и других передач данных по сети, выполняемых одновременно.

При использовании **контекста вычислений SQL Server**, что код выполняется на сервере. При получении данных из SQL Server, данные должны быть локально на сервере под управлением анализа и поэтому вводится без нагрузки на сеть. Если вам нужно импортировать данные из других источников, следует заранее упорядочение ETL.

При работе с большими наборами данных следует всегда использовать контекст вычислений SQL.

## <a name="factors"></a>Факторы

Язык R использует концепцию «факторов», которые являются специальная переменная для категориальных данных. Специалисты по анализу данных часто коэффициент переменные используются в формуле их, так как обработка категориальные переменные как факторы, гарантирует, что данные обрабатываются правильно машины обучения функции. Дополнительные сведения см. в разделе [R для «чайников»: переменные коэффициент](http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

Разработчиками предусмотрено коэффициент переменные можно преобразовать из строк целых чисел и обратно снова для хранения и обработки. R `data.frame` функция обрабатывает все строки как переменные коэффициент, если аргумент *stringsAsFactors* равно **False**. Это означает, что строки автоматически преобразуется в целое число для обработки и затем сопоставляются с исходной строки.

Если исходные данные для факторы хранится как целое число, производительность может снизиться, так как R преобразует коэффициент целых чисел в строки во время выполнения, а затем выполняет собственную внутреннее преобразование строки в целое число.

Чтобы избежать таких преобразований во время выполнения, рассмотрите возможность хранения значения как целочисленные значения в таблице SQL Server и с помощью _colInfo_ аргумент для указания уровней для столбца, используемого в качестве фактора. Большинство объектов источника данных в RevoScaleR принимать параметр _colInfo_. Используйте этот параметр для имен переменных, используемых в источнике данных, укажите их тип, а также определить уровни переменные или преобразований для значений столбца.

Например следующий вызов функции R возвращает целые числа 1, 2 и 3 из таблицы, но сопоставляет значения коэффициента с уровнями «apple», «orange» и «banana».

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Если исходный столбец содержит строки, это всегда более эффективно для определения уровней, опережает время с помощью _colInfo_ параметра. Например следующий код R обрабатывает строки как факторы, как во время чтения.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Если нет никаких семантических различий в создании модели, последний подход может привести к более высокую производительность.

## <a name="data-transformations"></a>Преобразования данных

Специалисты по анализу и обработке данных часто используют функции преобразования, написанные на языке R, в процессе анализа. Функция преобразования применяется к каждой строке, полученных из таблицы. В SQL Server для всех строк, которые получены в пакете, в которой требуется связь между интерпретатора R и подсистема аналитики применяются такие преобразования. Чтобы выполнить преобразование, данные перемещаются из SQL в подсистему аналитики, а затем в процесс интерпретатора R и обратно.

По этой причине использование преобразований в рамках кода R может иметь значительное отрицательное влияние на производительность алгоритма, в зависимости от объема тестовых данных.

Это более эффективно будет иметь все необходимые столбцы в таблице или представлении перед выполнением анализа и избежать преобразования во время вычисления. Если вы не можете добавить дополнительные столбцы к существующим таблицам, создайте другую таблицу или представление с преобразованными столбцами и используйте соответствующий запрос для получения данных.

## <a name="batch-row-reads"></a>Считывает строки пакета

При использовании источника данных SQL Server (`RxSqlServerData`) в коде, рекомендуется сначала ознакомиться с помощью параметра _rowsPerRead_ для указания размера пакета. Этот параметр определяет количество строк, запрос и отправлено внешних скриптов для обработки. Во время выполнения алгоритма видит только указанное количество строк в каждом пакете.

Возможность контролировать объем данных, обрабатываемых одновременно может помочь решить или устранения неполадок. Например, если входной набор данных очень широка (содержит много столбцов), или если набор данных содержит несколько больших столбцов (например, произвольный текст), можно уменьшить размер пакета, чтобы избежать разбиения на страницы данных не хватает памяти.

По умолчанию значение этого параметра имеет значение 50000, чтобы обеспечить корректную производительность даже на компьютерах с недостаточным объемом памяти. Если на сервере недостаточно памяти, увеличение этого значения 500 000 или даже миллионы могут помочь повысить производительность, особенно для больших таблиц.

Увеличение размера пакета преимущества очевидны на большой набор данных, а в задачу, которая может работать на нескольких процессов. Однако увеличение этого значения не всегда дают наилучшие результаты. Рекомендуется поэкспериментировать с данными и алгоритм, чтобы определить оптимальное значение.

## <a name="parallel-processing"></a>Параллельная обработка

Чтобы повысить производительность **rx** аналитические функции можно использовать возможность выполнения задач в параллельном режиме, используя доступные ядра на компьютере сервера SQL Server.

Существует два способа для достижения параллелизма с помощью R в SQL Server:

-   **Используйте \@parallel.** При использовании хранимой процедуры `sp_execute_external_script` для выполнения скрипта R установите для параметра `@parallel` значение `1`. Это является лучшим методом, если R-скриптов не **не** использовать функции RevoScaleR, имеющих другие механизмы для обработки. Если скрипт использует функции RevoScaleR (обычно префикс «rx»), параллельная обработка выполняется автоматически и не нужно явно задавать `@parallel` для `1`.

    Если скрипт R может выполняться параллельно, и SQL-запрос может выполняться параллелизация, компонент database engine создает несколько параллельных процессов. Максимальное число процессов, которые могут быть созданы равен **максимальная степень параллелизма** параметр (MAXDOP) для экземпляра. Затем все процессы запустите тот же сценарий, но получать только часть данных.
    
    Таким образом, этот метод не является полезным для скриптов, которые должен видеть все данные, например, при обучении модели. Тем не менее это пригодится при выполнении задач, таких как пакетное прогнозирование в параллельном режиме. Дополнительные сведения об использовании параллелизм с `sp_execute_external_script`, в разделе **Дополнительные советы: параллельная обработка** раздел [с помощью кода R в Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Использовать numTasks = 1.** При использовании **rx** функции в контексте вычислений SQL Server, установите для параметра _numTasks_ параметр число процессов, которые вы хотите создать. Количество процессов, созданных никогда не может быть более **MAXDOP**; тем не менее фактическое количество процессов, созданных определяется компонентом database engine и может быть меньше, чем вы запрошена.

    Если скрипт R может выполняться параллельно, и SQL-запрос может выполняться параллелизация, SQL Server создает несколько параллельных процессов при выполнении функций rx. Фактическое число процессов, которые создаются зависит от множества факторов, таких как управление ресурсами, текущее использование ресурсов, другие сеансы и план выполнения запроса для запроса, используемого с R-скрипта.

## <a name="query-parallelization"></a>Параллелизация запросов

В Microsoft R может работать с источниками данных SQL Server, определяя данные как RxSqlServerData объект источника данных.

Создает источник данных на основе всей таблицы или представления:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Создает источник данных на основе SQL-запроса:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Если таблицы в источнике данных, а не запрос, R Services используется эвристическими для определения необходимых столбцов для выборки из таблицы; Однако такой подход вряд ли приведет параллельного выполнения.

Чтобы убедиться, что данные можно проанализировать в параллельном режиме, следует заключить запрос, используемый для извлечения данных таким образом, что компонент database engine можно создать план параллельных запросов. Если код или алгоритм использует больших объемов данных, убедитесь, что запрос, присвоенное `RxSqlServerData` оптимизирован для параллельного выполнения. Запрос, который не выполняется в рамках плана параллельного выполнения, может выполниться в одном процессе для вычисления.

Если необходимо работать с большими наборами данных, используйте среду Management Studio или другим анализатор запросов SQL, прежде чем выполнять код R, для анализа плана выполнения. Выполните все рекомендуемые действия для улучшения производительности запроса. Например, отсутствующий индекс таблицы может повлиять на время, затраченное на выполнение запроса. Дополнительные сведения см. в разделе [наблюдение и настройка производительности](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Другой распространенная ошибка, может повлиять на производительность заключается в том, что запрос получает больше столбцов, чем необходимо. Например если формула зависит только три столбца, но в исходной таблице есть столбцы, 30, перемещаются данные без необходимости.

 + Старайтесь не использовать `SELECT *`!
 + Внимательно просмотрите столбцы в наборе данных и выберите только те, необходимые для анализа
 + Удалить из запросов все столбцы, которые содержат типы данных, которые несовместимы с кода R, например идентификаторы GUID и идентификаторами rowguids
 + Проверьте форматы неподдерживаемые даты и времени
 + Вместо загрузки таблицы, создайте представление, которое выбирает определенные значения или приводит столбцы, чтобы избежать ошибок преобразования

## <a name="optimizing-the-machine-learning-algorithm"></a>Оптимизация алгоритм машинного обучения

Этот раздел содержит прочие советы и ресурсы, относящиеся к RevoScaleR и другие параметры в Microsoft R.

> [!TIP]
> Общие сведения об оптимизации R выходит за рамки данной статьи. Тем не менее, если вам нужно сделать код быстрее, мы рекомендуем популярные статьи [Inferno R](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Он охватывает программных конструкций в R и слабых местах в виде наглядных языка и подробных сведений и множество примеров конкретных методах программирования R.

### <a name="optimizations-for-revoscaler"></a>Оптимизация для RevoScaleR

Многие алгоритмы RevoScaleR поддерживает параметры для управления созданием обученной модели. Хотя важна точность и правильность модели производительности алгоритма могут оказаться менее важно. Чтобы обеспечить баланс между точностью и время обучения, можно изменить параметры для повышения скорости вычислений, а также во многих случаях, повысить производительность, не снижая точность и правильность.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` поддерживает `maxDepth` параметр, который управляет глубину дерева принятия решений. Как `maxDepth` является увеличение производительности может привести к снижению, поэтому важно проанализировать преимущества увеличении глубины и что приводит к падению производительности.

    Можно также управлять баланс между времени точность сложности и прогноза путем настройки параметров, таких как `maxNumBins`, `maxDepth`, `maxComplete`, и `maxSurrogate`. Если увеличить глубину до 10 или 15, стоимость вычислений сильно увеличится.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Попробуйте использовать `cube` аргумент, если в формуле первой зависимой переменной является переменной коэффициент.
    
    Когда `cube` равно `TRUE`, регрессии выполняется с использованием секционированных обратное, которой может быстрее и использует меньше памяти, чем стандартная регрессии вычисления. Если в формуле используется много переменных, производительность может существенно повыситься.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Используйте `cube` аргумент, если первый зависимой переменной является переменной коэффициент.
    
    Когда `cube` равно `TRUE`, алгоритм использует секционированную обратное, которого может выполняться быстрее и использовать меньше памяти. Если в формуле используется много переменных, производительность может существенно повыситься.

Дополнительные рекомендации по оптимизации RevoScaleR см. в следующих статьях:

+ Статья службы поддержки: [производительности, помощник по настройке параметров rxDForest и rxDTree](https://support.microsoft.com/kb/3104235)

+ Методы управления модели помещается в модель повышенного дерева принятия решений: [оценка моделей с помощью вероятностный градиентный Бустинг](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Общие сведения о том, как RevoScaleR перемещает и обрабатывает данные: [написать пользовательские алгоритмы фрагментации в ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Модель программирования для RevoScaleR: [управляет потоками в RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Функция справочник для [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Функция справочник для [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Использовать MicrosoftML

Кроме того, рекомендуется ознакомиться в новый **MicrosoftML** пакет, который предоставляет масштабируемые алгоритмы обучения, можно использовать контексты вычислений и RevoScaleR, предоставляемые преобразования.

+ [Приступая к работе с MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Выбор алгоритма MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Решения с использованием Microsoft R Server ввода в эксплуатацию

Если ваш сценарий включает в себя быстрого прогноза с помощью хранимых моделей или интеграции машинного обучения в приложении, можно использовать [ввода в эксплуатацию](https://docs.microsoft.com/r-server/what-is-operationalization) возможности Microsoft R Server (прежнее название — DeployR).

+ Как **специалист по анализу данных**, используйте [пакета mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) для совместного использования кода R с другими компьютерами и интеграция R аналитика в приложениях web, рабочий стол, мобильных устройств и панели мониторинга: [публикация и управление веб-службами R в R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Как **администратора**, как управлять пакетами, мониторинг веб-узлов и вычислительных узлов и управления безопасностью в заданиях R: [взаимодействовать и использовать веб-службы в R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Статьи в этой серии

[Производительность помощник по настройке для R — введение](sql-server-r-services-performance-tuning.md)

[Настройка производительности для R - конфигурации SQL Server](sql-server-configuration-r-services.md)

[Настройка производительности для R - R оптимизации кода и данных](r-and-data-optimization-r-services.md)

[Помощник по настройке производительности - пример использования результатов](performance-case-study-r-services.md)
