Прошивка для стика modkam (с кнопкой FLASH и без кнопки FLASH)

## История изменений
1. **jh_2538_router_20200520.hex**
    * Исправлена ошибка с Identify;
    * Разрешен Bootloader. Запуск по низкому уровню на PA7;
    * Отключено постоянное свечение LED4;
    * NWK_MAX_DEVICE_LIST = 100;

2. **jh_2538_router_20200522.hex**
    * Исправлена проблема с переходом в режим bootloader после долгого удерживания кнопки FLASH(PA7). 
    * Добавлена функция сброса устройства на заводские установки путем быстрого нажатия на кнопку RESET 5 раз. Нажатие считается быстрым если произведено до включения светодиода LED1;
    * NWK_MAX_DEVICE_LIST = 40;




## Индикация 

Для индикации используется светодиод **LED1** (синий).
* Мигание с частотой 1 Гц, длительность свечения 500 мс - режим поиска доступной сети;
* Постоянное свечение - устройство в сети;
* Светодиод погас на 1 сек. - подтверждение нажатия на кнопку **FLASH**;
* Мигание с частотой 1 Гц, длительность свечения 100 мс - режим **Identify**;
* Мигание с частотой 5 Гц, длительность свечения 100 мс - для продолжения сброса необходимо отпустить **FLASH(PA7)**; 


## Управление

* Включение питания запускает процесс поиска/присоеденения к сети;
* Удержание кнопки **FLASH** более 5 секунд приводит к сбросу устройства на заводские установки и выполняется программный RESET. Так как низкий уровень на **FLASH(PA7)** - это условие для входа в режим Bootloader после RESET, то быстрое мигание **LED1** (частота 5Гц) указаывает на то что условие для сброса выполнено, но для продолжения необходимо отпустить кнопку;
* Короткое нажатие на кнопку **FLASH** приводит к отправке **ReportAttr** (кластер 0x0 Basic, атрибут 0x5 modelID);

## Simple Descriptor
```
Endpoint: 1
Profile: Home Automation (0x0104)
Application Device: Unknown (0x0100)
Input Cluster Count: 2
Input Cluster List
    Input Cluster: Basic (0x0000)
    
        Attribute: ZCL Version (0x0000)
        Data Type: 8-Bit Unsigned Integer (0x20)
        Uint8: 1 (0x01)
            
        Attribute: HW Version (0x0003)
        Data Type: 8-Bit Unsigned Integer (0x20)
        Uint8: 1 (0x01)
        
        Attribute: Manufacturer Name (0x0004)
        Data Type: Character String (0x42)
        String: jethome
    
        Attribute: Model Identifier (0x0005)
        Data Type: Character String (0x42)
        String: cc2538.router.v1
   
        Attribute: Date Code (0x0006)
        Data Type: Character String (0x42)
        String: 20200520 <- этот параметр зависит от версии прошивки. 

    Input Cluster: Identify (0x0003)
Output Cluster Count: 1
Output Cluster List
    Output Cluster: Basic (0x0000)
```