---
title: Контрольные списки настройки - система платформы аналитики | Документы Microsoft
description: Предоставляет контрольные списки для задачи, необходимые для настройки система платформы аналитики по собственной среде. Эти задачи настройки необходимы, прежде чем использовать устройства.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 17099af36994f24d182c7465bcbdc3f82e670328
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2018
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Контрольные списки настройки устройства для система платформы аналитики
Предоставляет контрольные списки для задачи, необходимые для настройки система платформы аналитики по собственной среде. Эти задачи настройки необходимы, прежде чем использовать устройства.  
  
> [!WARNING]  
> Система платформы аналитики с помощью**Configuration Manager** является лучшим способом, и единственный поддерживаемый способ, выполнять задачи, доступные в программе.  
  
## <a name="BeforeTasks"></a>Перед началом  
  
### <a name="prerequisites"></a>предварительные требования  
  
1.  Устройство должно быть установлено в центре обработки данных и включено.  
  
2.  Убедитесь, что у вас есть следующие сведения, предоставляемые к независимому поставщику Оборудования.  
  
    -   Внешний IP-адрес узла управления PDW (*PDW_region -* CTL01)  
  
    -   Доменное имя устройства  
  
    -   Имя пользователя и пароль для администратора домена устройства  
  
3.  Получите доверенный сертификат. Это будет импортирован на более позднем этапе, чтобы разрешить клиентам подключаться к **консоли администрирования** с безопасных соединений. Сохраните файл сертификата на узел элемента управления в PFX-файл защищен паролем.  
  
4.  Запустите **Configuration Manager**, выполнив следующие действия:  
  
    1.  Используйте **удаленного рабочего стола** для подключения к узлу управления PDW (*PDW_region*-CTL01). (Может потребоваться доступ к внешний IP-адрес для CTL01).  
  
    2.  Запустите **Configuration Manager** из **запустить** меню узла управления PDW. Первый экран Configuration Manager отображает топология устройства, который был создан в к независимому поставщику Оборудования. Он представляет собой список оборудования узлов, распознаваемые программным обеспечением SQL Server PDW как часть вашего устройства. Чтобы изменить параметры на экране топология устройства нет необходимости.  
  
## <a name="CMTasks"></a>Выполнять задачи Configuration Manager  
SQL Server PDW**Configuration Manager** (PDWCM) является средством администрирования устройства для системных администраторов SQL Server PDW использовать для выполнения операций на уровне устройства и изменить настройки на уровне устройства. Например можно используйте PDWCM для сброса паролей, задать часовой пояс, изменить IP-адреса, настроить сертификаты SSL, включить удаленный доступ через брандмауэр, запустить или остановить устройства и задать быстрой инициализации файлов.  
  
Используйте **Configuration Manager** для выполнения следующих задач конфигурации.  
  
|Задача конфигурации|Описание|  
|----------------------|---------------|  
|Ознакомьтесь с имена физических компонентов|[PDW Appliance структуры физические компоненты и &#40;система платформы аналитики&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Запустите диспетчер конфигурации SQL Server PDW|[Запустите диспетчер конфигурации &#40;система платформы аналитики&#41;](launch-the-configuration-manager.md)|  
|Изменение пароля администратора домена|Устройство имеет закрытый Windows доменных служб Active Directory, используемый для проверки подлинности узлов в устройстве.<br /><br />К независимому поставщику Оборудования, настроить устройство с паролем администратора домена по умолчанию. Это необходимо изменить пароль, который является безопасным.<br /><br />**Configuration Manager** единственный поддерживаемый способ изменения пароля администратора домена.<br /><br />Дополнительные сведения см. в разделе [сброса пароля &#40;Analytics Platform System&#41;](password-reset.md).|  
|Изменение пароля для **sa** входа в систему|SQL Server PDW имеет имя входа администратора системы **sa**. **Sa** входа имеет все права доступа. Его можно предоставить, запретить или право отзывать любое разрешение. Также можно увидеть все системные представления.<br /><br />Дополнительные сведения см. в разделе [сброса пароля &#40;Analytics Platform System&#41;](password-reset.md).|  
|Задайте часовой пояс устройства|Укажите время (локального или нужное время), все узлы устройств.<br /><br />Дополнительные сведения см. в разделе [конфигурация часового пояса устройства &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Укажите внешний параметры сети для SQL Server PDW appliance|[Сетевая конфигурация устройства &#40;система платформы аналитики&#41;](appliance-network-configuration.md)|  
|Импортировать сертификат безопасности для консоли администрирования|Сертификат может поддерживать подключения Secure Sockets Layer (SSL) по протоколу HTTPS для [отслеживать устройства с помощью консоли администрирования &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). По умолчанию **консоли администрирования** включает самозаверяющий сертификат, который обеспечивает конфиденциальность, но не проверки подлинности сервера. Этот сертификат также возвращает сообщение об ошибке в Internet Explorer сообщением: «Имеется проблема с сертификатом безопасности этого веб-сайта» при подключении пользователя. Несмотря на то, что это подключение шифрует обрабатываемых данных между клиентом и сервером, подключение осуществляется по-прежнему риску злоумышленниками.<br /><br />Администраторы SQL Server PDW следует немедленно получить сертификат, связанный доверенным центром сертификации распознается клиентами, для безопасного подключения и устранить эту ошибку, которая сообщает Internet Explorer. Это требует полного доменного имени, которая сопоставляет виртуальный IP-адрес узла управления (рекомендуется) или имя сертификата, соответствующий значению, вводимых пользователями в их адрес обозревателя столбцов, которые необходимо получить доступ к консоли администрирования.<br /><br />Используйте **Configuration Manager** Добавление и удаление доверенных сертификатов. Непосредственно с помощью средства конфигурации сертификата службы Microsoft Windows HTTP (`winHttpCertCfg.exe`) для управления сертификатами не поддерживается.<br /><br />Дополнительные сведения см. в разделе [Подготовка сертификата PDW &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Переключение функции|Отображает сведения о параметрах функции, представленные в AU7 системы платформы аналитики. Эта страница служит для обновления или включение или отключение компонентов и параметров в Analytics Platform System. Для изменения значения компонента коммутатора требуется перезапуск службы.<br /><br />Дополнительные сведения см. в разделе [переключение функции PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Включение и отключение правила брандмауэра Windows, которые разрешают или запрещают доступ к конкретным портам на SQL Server PDW appliance.|К независимому поставщику Оборудования будут настраивать и включить правила брандмауэра, которые необходимы для правильной работы устройства. В большинстве случаев не будет включить или отключить правила брандмауэра.<br /><br />Дополнительные сведения см. в разделе [конфигурации брандмауэра PDW &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Запуск и остановка SQL Server PDW appliance|Останавливает или запускает SQL Server PDW appliance. Дополнительные сведения см. в разделе [состояние служб PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Просмотр параметров быстрой инициализации файлов с помощью **права** диалоговое окно|Мгновенная инициализация файлов является компонентом SQL Server, который обеспечивает более быстрое выполнение операций файла данных. Это свойство включено в SQL Server PDW только в том случае, если учетной записи сетевой службы было предоставлено право SE_MANAGE_VOLUME_NAME. По умолчанию она отключена.<br /><br />Дополнительные сведения см. в разделе [мгновенных файл инициализации настройки &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md).|  
|Восстановить базу данных master из резервной копии|Удаляет текущий **master** базы данных и заменяет его с помощью резервной копии. Дополнительные сведения см. в разделе [восстановление базы данных Master &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Выполнить дополнительные задачи по настройке  
После выполнения **Configuration Manager** задачи, выполните описанные ниже дополнительные задачи по настройке. Некоторые из этих задач являются необязательными.  
  
|Задача конфигурации|Описание|  
|----------------------|---------------|  
|Антивирусное программное обеспечение сторонних разработчиков, которые могут быть установлены и настроены на устройстве для общедоступный узлов SQL Server PDW.<br /><br />(необязательно)|Дополнительные сведения см. в разделе [антивирусные программы &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|Можно изменить пароль DSRM.<br /><br />(необязательно)|Дополнительные сведения см. в разделе [задать пароль администратора для входа в систему узлов AD в режиме восстановления служб каталогов &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Настроить устройство для получения обновлений программного обеспечения<br /><br />(Рекомендовано)|Устройства должна быть настроена на получение обновлений для SQL Server PDW и базового программного обеспечения.<br /><br />Дополнительные сведения см. в разделе [настройки Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Сведения о службах WSUS см. в разделе [обслуживания программного обеспечения &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Настройка подключения к внешним данным, таких как хранилище больших двоичных объектов Azure или Hadoop.<br /><br />(необязательно)|Дополнительные сведения см. в разделе [Настройка PolyBase подключения к внешним данным &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Настройка антивирусного программного обеспечения<br /><br />(необязательно)|Антивирусные решения сторонних разработчиков могут использоваться для защиты внешний узлов, но не является обязательным. Следуйте инструкциям из раздела.|  
|Настройте InfiniBand сетевые адаптеры на резервное копирование и загрузки серверов<br /><br />(необязательно)|Настройка резервного копирования и загрузки серверов, для подключения к SQL Server PDW по сети InfiniBand, необходимо настроить сетевые адаптеры, чтобы разрешить DNS для разрешения соединения InfiniBand активного сети InfiniBand устройства.|  
|Настройка отправлять данные телеметрии в корпорацию Майкрософт<br /><br />(необязательно)|Чтобы настроить Analytics Platform System отправлять данные телеметрии в корпорацию Майкрософт, необходимо запустить сценарий PowerShell на узел элемента управления. Дополнительные инструкции в разделе [телеметрии отзывы в корпорацию Майкрософт &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>См. также  
[Антивирусная программа &#40;система платформы аналитики&#41;](antivirus-software.md)  
[Настройка сети InfiniBand адаптеров &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
