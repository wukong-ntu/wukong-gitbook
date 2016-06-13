## WuClass Examples for Grove Modules

Having introduced the template of writing a WuClass both in Python and C, we are going to explain several WuClass samples within the WuClass list of the FBP editor so that you can use them and expand them according to your design. 

* ###**Grove Module List**   

  Since the sensor list provided in the Intel IoT official website https://software.intel.com/en-us/iot/hardware/sensors is focus on Grove modules, in this section, we also start on WuClass samples for Grove modules. Although there are countless Grove modules in the list, we can filter the list by component type or connection type. According to the connection types of Grove modules as shown below, there are AIO, GPIO, I2C, PWM, SPI, and UART. With this category, we can categorize WuClass samples for Grove modules into different groups as well. In each group, we will take a WuClass as an example and give an explaination.    

 ![](intel_iot_sensor.png)

* ###**mraa API for Grove Modules**   

 To control Grove modules, we have to find a way to interface with each connection type of Grove modules on the Intel Edison and Intel Galileo. Fortunately, mraa library provides an array of C/C++ API with binding to Python. Therefore, we can use the mraa API to alleviate large efforts of the hardware configuration. Here are the [LINK for mraa C LIBRARY](http://iotdk.intel.com/docs/master/mraa/), and the [LINK for mraa Python LIBRARY](http://iotdk.intel.com/docs/master/mraa/python/index.html). In fact, we have already used the mraa API for a button and a light actuator WuClass in the last section. The connection type of button and light actuator is GPIO. For other connection types, please move on to the next page [Using C Programming Language](../Ch6/Grove/c_program.md) or [Using Python Programming Language](../Ch6/Grove/python_program.md)          
