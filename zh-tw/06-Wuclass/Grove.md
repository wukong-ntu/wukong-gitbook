##6.4 悟空類別範例：Grove模組   
<!--##6.4 WuClass Examples for Grove Modules-->   

在悟空類別的實作介紹之後，這章節會繼續了解一些相仿的範例，讓開發者能夠針對個別應用的需要，來實作新的悟空類別。   
<!--Having introduced the template of writing a WuClass in Python, we will show several WuClass examples so that you can use and expand them according to your needs.-->   

我們的範例是使用Grove模組(http://www.seeedstudio.com/wiki/Grove_System), 選擇Grove模組的原因是，這個模組可以透過各家的擴充板，輕易地連接到物聯網開發板(Edison, Galileo and Raspberry Pi)，並且，Grove系列提供了非常豐富的元件與函式庫給物聯網的開發者。   
<!--We use a sensor kit called Grove modules (http://www.seeedstudio.com/wiki/Grove_System). These modules can be assembled easily on Edison, Galileo and Raspberry Pi using individual shields. Also, they provide abundant sensors, actuators and libraries for IoT developers.-->   

關於更多Grove開發模組(Grove Starter Kit)的資訊，請參考以下的網頁：  
使用Intel Edison or Galileo: https://software.intel.com/iot/hardware/devkit   
使用Raspberry Pi: http://www.dexterindustries.com/grovepi/
<!--For more information of Grove starter kit, please refer to the following websites:   
Using Intel Edison or Galileo: https://software.intel.com/iot/hardware/devkit  
Using Raspberry Pi: http://www.dexterindustries.com/grovepi/-->  

####輸入/輸出介面(IO Interface)
<!--####IO Interface-->     
如同上節所述，爲了讓同一個Grove模組的範例能執行在Edison, Galileo和Raspberry Pi，我們新增了這個介面(udpdevice_io_interface.py)來決定如何使用三個不同的GPIO函式庫，對Edison,Galileo來說，所需要匯入的GPIO函式庫爲mraa;對Raspberry Pi來說，所需要匯入的GPIO函式庫爲rpi，若使用Grove Pi擴充板的話，所需要匯入的GPIO函式庫則爲grovepi，因此，在這個介面的一開始(如下圖)，我們定義三種裝置的選項：DEVICE_TYPE_MRAA,DEVICE_TYPE_GPI以及DEVICE_TYPE_RPI，並於第12行決定要使用哪一個選項來執行Grove模組的範例。       
<!--As we mentioned in the last section, in order to be compatible to all libraries of Edison, Galileo and Raspberry Pi, we have added an io interface to bridge individual library. For Edison and Galileo, we have to import mraa library; for Raspberry Pi, we have to import rpi or grovepi library. To achieve this, we add a device_type definition  on line 12 of udpwkpf_io_interface.py. Currently, there are three options: DEVICE_TYPE_MRAA, DEVICE_TYPE_GPI and DEVICE_TYPE_RPI. You need to configure this definition before running a WuClass of Grove modules on the IoT board.-->          

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/io_interface_type3.png)

####GPIO使用方式
<!--####GPIO USAGE-->    
除了用這個介面決定使用哪一種裝置外，這個介面也定義了如何在裝置上使用GPIO，目前爲止，我們在這個介面中定義了6個使用GPIO的共同方式，如下所示：
<!--After specifying which library we want to import for the WuClass, we also use this type definition to manage how the code uses the gpio function. For the time being, we have defined six common functions for gpio usage. These functions are as follows.-->     
```
pin_mode(pin, pin_type, pin_mode, **kwargs)  
# 這個函式是用來初始化GPIO腳位(pin)的設定，包括型態(pin_type)是數位或類比(digital/analog)，
# 或者模式(pin_mode)是輸入或輸出。

digital_read(pin_obj)   
# 若腳位的型態設定爲數位，模式設定爲輸入，我們可以用這個函式來讀取GPIO的值，
# pin_obj是pin_mode的回傳物件。  

digital_write(pin_obj, val)   
# 若腳位的型態設定爲數位，模式設定爲輸出，我們可以用這個函式來寫入GPIO，
# pin_obj是pin_mode的回傳物件,val是要寫入GPIO的值。  

analog_read(pin_obj)  
# 若腳位的型態設定爲類比，模式設定爲輸入，我們可以用這個函式來讀取GPIO，  
# pin_obj是pin_mode的回傳物件。
# 但由於Raspberry Pi本身不支援類比輸入，
# 所以此函式只適合用在Edison,Galileo以及使用grovepi擴充板的Raspberry Pi。 

analog_write(pin_obj, val)
# 若腳位的型態設定爲類比，模式設定爲輸出，我們可以用這個函式來寫入GPIO，
# pin_obj是pin_mode的回傳物件,val是要寫入GPIO的值。 
# 但目前只有使用grovepi擴充板的Raspberry Pi支援類比輸出。

temp_read(pin_obj)
# 這是針對Grove模組中的溫度感測器所定的介面函式，
# pin_obj是pin_mode的回傳物件。
# 但由於Raspberry Pi本身不支援類比輸入，
# 所以此函式只適合用在Edison,Galileo以及使用grovepi擴充板的Raspberry Pi。  
```  

目前關於Grove開發模組的悟空裝置程式，大都是使用以上的介面函式來讀取或寫入開發板的GPIO，然而，這個介面目前只限於使用數位和類比GPIO，尚未支援共同的PWM,I2C,SPI,以及UART介面，主要的原因是，各個GPIO函式庫在處理數位和類比GPIO的方式較爲接近，所以容易定義一個共同的介面，但其餘的傳輸方式就有許多差異，因此，目前若需使用PWM,I2C,SPI,以及UART傳輸的Grove模組時，就不會使用這個介面，而是針對各個開發板獨自開發，比方說蜂鳴器(Buzzer)，mraa函式庫是用PWM來控制蜂鳴器，但grovepi函式庫只支援用類比輸出(analog write)來控制蜂鳴器，於是蜂鳴器的範例就沒有使用這個介面。   
<!--We have used the above functions throughout the WuClasses for the Grove kit. However, before you use these functions, you need to check updwkpf_io_interface.py to see whether it supports the "device type" you have selected.-->   

####Grove開發模組範例(Grove Starter Kit)
<!--####Examples-->  
以下列出使用各個GPIO介面函式的範例：
<!--According to the connection types of Grove modules, we can divide them into following categories: Digital IO, Analog IO, PWM, I2C, SPI, and UART. Sometimes, one device handles certain connection type using individual library which is quite different than others. In this case, the function of io interface could be difficult to be defined. Therefore, for the time being, we only apply io interface to WuClass of Grove starter kit.-->        

* **使用數位輸入GPIO的按鈕(Button)**
<!--* **Sensor with digital input**-->   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_digital_input.png)  

* **使用數位輸出GPIO的繼電器(Relay)**
<!--* **Actuator with digital output**-->     
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_digital_output.png)

* **使用類比輸入的旋轉電位器(Slider)**
<!--* **Sensor with Analog input**-->   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_analog_input.png)

* **使用特定函式的溫度感測器(Temperature Sensor) **
<!--* **Sensor with individual library**-->   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_specific_library.png)   

這些範例程式均存放於：
```
https://github.com/wukong-m2m/wukong-darjeeling/tree/release0.4/wukong/gateway/udpwkpf
```

####開發板的腳位編號
<!--####Pin Numbering-->     
在選擇使用哪一個裝置執行Grove開發模組的範例後，我們需要確認範例程式中所定義的腳位編號，並將Grove開發模組連接到合適的位置，以下分別是Edison的Grove擴充板,Raspberry Pi與其GrovePi擴充板的腳位定義，這些腳位編號通常定義在每個悟空裝置程式的最前面。   
<!--While selecting a device type, we have to define the pin numbering for each sensor and actuator. The following figures are the pin assignments for grove starter kit on Edison base board, Raspberry Pi and GrovePi shield. In our code, the pin number used in each WuClass is defined at the beginning of the code so that you can change it easily.-->        
  

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/edison_pin_assignment.png)

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/rpi_pin_assignment.png)   

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/grovepi_pin_assignment.png)  



<!--
  Since the sensor list provided in the Intel IoT official website https://software.intel.com/en-us/iot/hardware/sensors is focus on Grove modules, in this section, we also start on WuClass samples for Grove modules. Although there are countless Grove modules in the list, we can filter the list by component type or connection type. According to the connection types of Grove modules as shown below, there are AIO, GPIO, I2C, PWM, SPI, and UART. With this category, we can categorize WuClass samples for Grove modules into different groups as well. In each group, we will take a WuClass as an example and give an explaination.   
-->

<!-- ![](intel_iot_sensor.png)-->

<!--
* ###**mraa API for Grove Modules**   

 To control Grove modules, we have to find a way to interface with each connection type of Grove modules on the Intel Edison and Intel Galileo. Fortunately, mraa library provides an array of C/C++ API with binding to Python. Therefore, we can use the mraa API to alleviate large efforts of the hardware configuration. Here is the [LINK for mraa Python LIBRARY](http://iotdk.intel.com/docs/master/mraa/python/index.html). In fact, we have already used the mraa API for a button and a light actuator WuClass in the last section. The connection type of button and light actuator is GPIO. The following part is going to explain more about other connection types.  
-->

<!--According to the connection types of Grove modules, we can divide them into following categories: AIO, GPIO, I2C, PWM, SPI, and UART. We will take a WuClass from each category as an example in the following pages. -->  