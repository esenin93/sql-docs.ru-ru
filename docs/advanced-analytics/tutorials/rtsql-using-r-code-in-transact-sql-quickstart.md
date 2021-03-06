---
title: С помощью кода R в Transact-SQL (R в быстрый запуск SQL Server) | Документы Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c11e2bba73cef8a8b6f59d5a92de22cddb19ccd9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>С помощью кода R в Transact-SQL (R в быстрый запуск SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

В этом руководстве описаны основные принципы вызова скрипта R из хранимой процедуры T-SQL.

**Вы узнаете**

+ Как внедрить R в функцию T-SQL.
+ Некоторые советы по работе с SQL и R данных типов и объектов данных
+ Как создать простую модель и сохранить его в SQL Server
+ Создание прогнозов и построения R, с помощью модели

**Предполагаемое время**

На прохождение этого руководства требуется 30 минут, не считая установки.

## <a name="prerequisites"></a>предварительные требования

Необходимо иметь доступ к экземпляру SQL Server с одним из уже установлены следующие компоненты:

+ Службы SQL Server 2017 г машины обучения, с языком R
+ SQL Server 2016 R Services

Экземпляр SQL Server может быть в виртуальной машине Azure или локально. Просто Учтите, что внешние средства написания сценариев отключена по умолчанию, может потребоваться выполнить некоторые дополнительные действия для его запуска.

Для выполнения запросов SQL, включающие скрипты R, можно использовать любое приложение, можно подключиться к базе данных и выполнить код T-SQL. Специалисты SQL можно использовать Visual Studio или SQL Server Management Studio (SSMS).

Для этого учебника, чтобы показать, как просто можно запускать в SQL Server, мы используем новый **mssql расширения для Visual Studio Code**. VS Code является бесплатной среды разработки, можно запустить в Windows, Linux или macOS. **Mssql** расширения представляют собой упрощенные расширение выполнение запросов T-SQL. Инструкции по ее установке см. в статье [Use Visual Studio Code to create and run Transact-SQL scripts for SQL Server](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode) (Использование Visual Studio Code для создания и выполнения скрипта Transact-SQL для SQL Server).

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>Подключение к базе данных и выполнение тестового скрипта Hello World

1. В Visual Studio Code создайте текстовый файл с именем BasicRSQL.sql.
2. В файле нажмите клавиши CTR+SHIFT+P (в операционной системе macOS нажмите COMMAND+P), введите **sql**, чтобы вывести список команд SQL, и выберите **Подключиться**. Код Visual Studio предложит создать профиль для использования при подключении к конкретной базе данных. Это не обязательно, но также облегчает переключение между базами данных и имена входа.
    + Выберите сервер или экземпляр, в которую были установлены R в SQL Server.
    + Используйте учетную запись, имеющую разрешения на создание базы данных, выполнение инструкций SELECT и просмотр определений таблиц.
2. Если подключение успешно установлено, в строке состояния должны отобразиться имена сервера и базы данных, а также текущие учетные данные. В случае сбоя подключения убедитесь, что имена компьютера и сервера заданы правильно.
3. Вставьте и выполните следующую инструкцию:

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    В Visual Studio Code выделите код, который необходимо выполнить, и нажмите клавиши CTRL+SHIFT+E. Если эту комбинацию трудно запомнить, вы можете ее изменить. Сведения см. в статье [Customize Keyboard Shortcuts](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts) (Настройка сочетаний клавиш).

    ![rsql basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**Результаты**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>Устранение неполадок

+ Если возникли ошибки из данного запроса, установки могут быть неполными. После добавления компонента с помощью мастера установки SQL Server необходимо выполнить некоторые дополнительные действия, чтобы включить использование библиотек внешнего кода.  В разделе [установить SQL Server 2017 г машинного самообучения, службы](../install/sql-machine-learning-services-windows-install.md) или [Установка служб R SQL Server 2016](../install/sql-r-services-windows-install.md).

+ Убедитесь, что запущена служба панели запуска. В зависимости от конкретной среды может потребоваться включить рабочие учетные записи R для подключения к SQL Server, установить дополнительные сетевые библиотеки, включить удаленное выполнение кода или перезапустить экземпляр после настройки всех компонентов. См. сведения в статье [Часто задаваемые вопросы по обновлению и установке для служб R SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

+ Чтобы скачать и установить Visual Studio Code, перейдите на [эту страницу](https://code.visualstudio.com/Download).

## <a name="next-lesson"></a>Следующее занятие

Теперь, когда экземпляр готов для работы с языком R, давайте начнем.

Урок 1. [работа с входными и выходными данными](rtsql-working-with-inputs-and-outputs.md)

Занятие 2. [SQL и R данных типов и объектов данных](rtsql-r-and-sql-data-types-and-data-objects.md)

Занятие 3. [использование R функций с данными SQL Server](rtsql-using-r-functions-with-sql-server-data.md)

Урок 4. [создать прогнозную модель](rtsql-create-a-predictive-model-r.md)

Занятие 5. [Predict и построения из модели](rtsql-predict-and-plot-from-model.md)
