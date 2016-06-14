##6.4 WuClass Examples for Grove Modules

Having introduced the template of writing a WuClass in Python, we will show several WuClass examples so that you can use and expand them according to your needs. 

We use a sensor kit called Grove modules (http://www.seeedstudio.com/wiki/Grove_System). These modules can be assembled easily on Edison, Galileo and Raspberry Pi using individual shields. Also, they provide abundant sensors, actuators and libraries for IoT developers. 

For more information of Grove starter kit, please refer to the following websites:   
Using Intel Edison or Galileo: https://software.intel.com/iot/hardware/devkit  
Using Raspberry Pi: http://www.dexterindustries.com/grovepi/

####IO Interface   

As we mentioned in the last section, in order to be compatible to all libraries of Edison, Galileo and Raspberry Pi, we have added an io interface to bridge individual library. For Edison and Galileo, we have to import mraa library; for Raspberry Pi, we have to import rpi or grovepi library. To achieve this, we add a device_type definition  on line 12 of udpwkpf_io_interface.py. Currently, there are three options: DEVICE_TYPE_MRAA, DEVICE_TYPE_GPI and DEVICE_TYPE_RPI. You need to configure this definition before running a WuClass of Grove modules on the IoT board.        

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/io_interface_type3.png)

####GPIO USAGE  

After specifying which library we want to import for the WuClass, we also use this type definition to manage how the code uses the gpio function. For the time being, we have defined six common functions for gpio usage. These functions are as follows.  
```
pin_mode(pin, pin_type, pin_mode, **kwargs)  
# this function declares whether the pin is digital/analog, input/output, etc.

digital_read(pin_obj)   
# if  pin_obj is digital and input,  we can use this to retrieve data from gpio

digital_write(pin_obj, val)   
# the usage is opposite to digital_read. 

analog_read(pin_obj)  
# since rpi library doesn't support anaglog reading, 
# we can only use this function when we import mraa or grovepi library. 

analog_write(pin_obj, val)
# only grovepi supports analog writing, 
# so we cannot use this function when we import mraa or rpi library. 

temp_read(pin_obj)  
# this function is specific for reading value from temperature sensor 
# of Grove starter kit.  
```  

We have used the above functions throughout the WuClasses for the Grove kit. However, before you use these functions, you need to check updwkpf_io_interface.py to see whether it supports the "device type" you have selected. 

####Examples  
According to the connection types of Grove modules, we can divide them into following categories: Digital IO, Analog IO, PWM, I2C, SPI, and UART. Sometimes, one device handles certain connection type using individual library which is quite different than others. In this case, the function of io interface could be difficult to be defined. Therefore, for the time being, we only apply io interface to WuClass of Grove starter kit.     

* **Sensor with digital input**   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_digital_input.png)  

* **Actuator with digital output**  
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_digital_output.png)

* **Sensor with Analog input**   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_analog_input.png)

* **Sensor with individual library**   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/6_4_example_specific_library.png)   

All of these WuClasses for Grove starter kit can be found in  
```
https://github.com/wukong-m2m/wukong-darjeeling/tree/release0.4/wukong/gateway/udpwkpf
```

####Pin Numbering  

While selecting a device type, we have to define the pin numbering for each sensor and actuator. The following figures are the pin assignments for grove starter kit on Edison base board, Raspberry Pi and GrovePi shield. In our code, the pin number used in each WuClass is defined at the beginning of the code so that you can change it easily.     
  

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