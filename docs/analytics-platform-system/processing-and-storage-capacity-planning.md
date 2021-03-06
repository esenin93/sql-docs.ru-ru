---
title: Обработка и емкость - система платформы аналитики | Документы Microsoft
description: Бизнес-требований определите число единиц масштабирования данных и размер дисков узел вычислений, необходимых в устройстве Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f552372ac108d219ad410b88ec9911ecaea63ab3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Мощность обработки и хранения в система платформы аналитики
Бизнес-требований определите число единиц масштабирования данных и размер дисков узел вычислений, необходимых в устройстве Analytics Platform System (APS). Используйте эти вычисления, обработки и хранения емкость приобретение и решения по планированию.  
  
  
## <a name="section1"></a>Планирование производительности обработки  
Производительность запросов для SQL Server Parallel данных хранилища (PDW) сильно зависит от количества ядер ЦП, работа с данными параллельно. В пределах увеличение параллелизма повышает производительность запросов расширенной параллельной обработке (MPP). Даже если размер данных относительно невелико, степень ядро запросов MPP повышается за счет которых больше параллелизма.  
  
Например устройство с 12 вычислительных узлов имеет 192 ядер ЦП, которые обрабатывают данные в параллельном режиме. Это способ 192 параллелизма! Устройства с 56 вычислительных узлов имеет 896 ядер все работают параллельно. Этой величины параллелизма не достижимые без MPP вычислений.  
  
Возрастает количество вычислительных узлов, горизонтальное масштабирование устройства требуется добавление нескольких вычислительных узлов в прошлое и получить заметных преимущества. Поставщики оборудования поддерживает только определенных конфигураций единиц масштабирования данных, чтобы убедиться, что преимущества масштабирования устройства перевешивает стоимость распространение данных через дополнительные вычислительные узлы.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Примеры конфигурации единицы масштабирования данных — HPE  
Ниже приведены примеры поддерживаемых конфигурациях HPE Uunits масштаб данных. Они могут отличаться от последние поддерживаемые конфигурации, но предоставлен в качестве примера того, как увеличить емкость приблизительно 20 процентов.  
  
Uplift является рост емкости процента, увеличив масштаб Uunits данных из одной строки к следующему. Например увеличение единицы масштабирования данных от 6 до 8 дает 33% uplift ядер ЦП и памяти.  Также увеличивает место на диске, который не отображается в этой таблице.  
  
|Единицы масштабирования данных|Вычислительные узлы|Число ядер ЦП|Память (ГБ)|Uplift|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1024|100%|  
|3|6|96|1536|50%|  
|4|8|128|2048|33%|  
|5|10|160|2560|25%|  
|6|12|192|3072|20%|  
|8|16|256|4096|33%|  
|10|20|320|5120|25%|  
|12|24|384|6144|20%|  
|16|32|512|8192|33%|  
|20|40|640|10240|25%|  
|24|48|768|12288|20%|  
|28|56|896|14336|17%|  
  
Описание:  
  
-   **Единицы масштабирования данных** на устройство. Дополнительные сведения о единицах масштабирования данных см. в разделе [компонентов оборудования системы платформы аналитики](hardware-components.md).  
  
-   **Вычислительные узлы** на устройство.  
  
-   **Число ядер ЦП** на устройство. Будет 16 ядер на вычислительном узле, одного ядра в каждом зеркальной пары диска. Структура диска вычислительного узла, в разделе [компонентов оборудования системы платформы аналитики](hardware-components.md).  
  
-   **Память** на устройство. Каждое ядро имеет 256 ГБ памяти.  
  
### <a name="data-scale-unit-configuration-examples--dell-quanta"></a>Масштаб Единица конфигурации примеры данных — Dell, тактов  
Ниже приведены примеры поддерживаемых конфигурациях Dell или Quanta Uunits масштаб данных. Они могут отличаться от последние поддерживаемые конфигурации, но предоставлен в качестве примера того, как увеличить емкость приблизительно 20 процентов.  
  
Uplift является рост емкости процента, увеличив масштаб Uunits данных из одной строки к следующему. Например увеличение единицы масштабирования данных от 6 до 8 дает 33% uplift ядер ЦП и памяти. Также увеличивает место на диске, который не отображается в этой таблице.  
  
|Единицы масштабирования данных|Вычислительные узлы|Число ядер ЦП|Память (ГБ)|Uplift|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2,304|50%|  
|4|12|192|3,072|33%|  
|5|15|240|3,840|25%|  
|6|18|288|4,608|20%|  
|7|21|336|5,376|17%|  
|8|24|384|6,144|14%|  
|9|27|432|6,912|13%|  
|12|36|576|9,216|33%|  
|15|45|720|11,520|25%|  
|18|54|864|13,824|20%|  
  
## <a name="section2"></a>Планирование емкости  
В этой таблице оценивает, что можно загрузить и хранения до 6 петабайт несжатых данных на полностью встроенных устройств Analytics Platform System. 
  
|Поставщика|Размер диска|Узел каждой вычислений физических данных хранилища|Максимальное число вычислительных узлов в стойку|Физического хранения максимального объема данных в стойку|Оценка хранения данных максимальное пользователей на каждую стойку|Максимальное стойки|Оценка хранения данных максимальное пользователя на устройство|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 ТБ|16 ТБ|8|128 TB|320 ТБ|7|2,240 ТБ|  
|HPE|2 ТБ|32 ТБ|8|256 ТБ|640 ТБ|7|4,480 ТБ|  
|HPE|3 ТБ|48 ТБ|8|384 ТБ|960 ТБ|7|6,720 ТБ|  
|DELL|1 ТБ|16 ТБ|9|144 ТБ|360 ТБ|6|2,160 ТБ|  
|DELL|2 ТБ|32 ТБ|9|288 ТБ|720 ТБ|6|4320 ТБ|  
|DELL|3 ТБ|48 ТБ|9|432 ТБ|1080 ТБ|6|6,480 ТБ|  
  
Описание:  
  
-   **Размер диска** — 1, 2 или 3 ТБ для каждого поставщика оборудования.  
  
-   **Хранение физических данных на вычислительном узле** = (размер диска) * (16 дисков на вычислительном узле). Зеркальные диски не включаются, поскольку они предназначены для обеспечения избыточности.  
  
-   **Максимальное вычислительных узлов на каждую стойку** относится к поставщику оборудования.  
  
-   **Физического хранения максимального объема данных на каждую стойку** = (хранилище физических данных на вычислительном узле) * (максимальное вычислительные узлы в стойку).  
  
-   **Оценка хранения данных максимальное пользователей на каждую стойку** = (физического хранения максимального объема данных на каждую стойку) * (5 коэффициента сжатия 5:1) \* (50% для базы данных tempDB и журналы). Это консервативной оценки для несжатые данные загружаются и хранятся на устройстве. Это является приблизительными и не является обязательным для программного обеспечения. Хранение данных пользователя зависит от конфигурации и данных.  
  
-   **Максимальное стойках** индивидуальна для каждого поставщика оборудования.  
  
-   **Оценка хранения максимального объема данных на устройство** = (оценка хранения максимального объема данных на каждую стойку) * (стойки, максимум). Это суммарные общего размера данных пользователя, можно загрузить и хранения на устройстве полностью встроенный консервативной оценки.  
  
