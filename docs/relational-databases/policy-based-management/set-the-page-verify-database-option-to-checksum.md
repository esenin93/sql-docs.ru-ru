---
title: Задание значения CHECKSUM для параметра базы данных PAGE_VERIFY | Документация Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2bb1bccbb0cebbd6b0373a633e88e871342a2e90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>Задание значения CHECKSUM для параметра базы данных PAGE_VERIFY
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Это правило проверяет, имеет ли параметр базы данных PAGE_VERIFY значение CHECKSUM. Если для параметра базы данных PAGE_VERIFY указано значение CHECKSUM, компонент [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] рассчитывает контрольную сумму для содержимого страницы в целом и сохраняет значение в заголовке страницы при записи страницы на диск. При считывании страницы с диска контрольная сумма вычисляется повторно и сравнивается со значением из заголовка. Это помогает обеспечить высокий уровень целостности данных в файлах.  
  
## <a name="best-practices-recommendations"></a>Рекомендации  
 Присвойте параметру базы данных PAGE_VERIFY значение CHECKSUM  
  
## <a name="for-more-information"></a>Дополнительные сведения см. в разделе  
 [Параметры ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
