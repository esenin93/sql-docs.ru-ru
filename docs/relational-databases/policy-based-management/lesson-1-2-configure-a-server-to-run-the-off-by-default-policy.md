---
title: Настройка сервера для выполнения политики "Отключено по умолчанию" | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bd8198d4ab869b38491a58782a03e73d2aaecb5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-2---configure-a-server-to-run-the-off-by-default-policy"></a>Занятие 1.2. Настройка сервера для выполнения политики "Отключено по умолчанию"
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Теперь есть политика с именем «Отключено по умолчанию». В этой задаче производится проверка сервера на соответствие требованиям политики «Отключено по умолчанию».  
  
### <a name="to-run-the-off-by-default-policy"></a>Запуск политики «Отключено по умолчанию»  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], наведите указатель на пункт **Политики**и выберите пункт **Вычислить**.  
  
2.  В диалоговом окне **Выполнить политики** можно выбрать политики из другого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или из файла. На этом шаге оставьте **Источник** , в качестве которого выбран ваш экземпляр [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3.  В разделе **Политики** выберите политику **Отключено по умолчанию** .  
  
4.  Для просмотра соответствия сервера политике нажмите **Вычислить**.  
  
5.  При соответствии компонента **политике в области** Результаты [!INCLUDE[ssDE](../../includes/ssde-md.md)] отобразится зеленый круг с галочкой. Если компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] не соответствует политике, отобразится красный круг со знаком «X».  
  
6.  В области **Данные целевого объекта** при возникновении ошибки дополнительные сведения можно просмотреть в столбце **Сообщение** . Для просмотра отчета, содержащего результаты проверки каждого свойства аспекта, в столбце **Сообщение** нажмите **Просмотреть** .  
  
7.  Описание политики отобразится в нижней части страницы, и в разделе **Дополнительная справка** будет показана гиперссылка, настроенная для политики. Для открытия веб-страницы, указанной при создании политики, щелкните сообщение гиперссылки.  
  
8.  Закройте браузер и диалоговое окно **Подробный просмотр результатов** .  
  
9. Если требуется отключить компонент Database Mail при несоответствии сервера политике, нажмите кнопку **Применить** на странице **Результаты вычислений** .  
  
10. Закройте диалоговые окна **Подробный просмотр результатов** и **Вычисление политик** .  
  
## <a name="next-lesson"></a>Следующее занятие  
[Занятие 2. Создание и применение политики стандартов именования](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
