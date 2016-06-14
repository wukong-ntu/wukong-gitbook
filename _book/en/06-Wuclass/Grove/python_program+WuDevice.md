## Python Program
With the template in the [last section](../Ch6_Using_Python_Programming_Language.md), we can create a WuClass by changing its setup function and refresh/update function to control specific hardware interface such as digital GPIO, analog GPIO, PWM, I2C and UART. In this section, we choose one of the sensors or actuators from each hardware interface and explain how its WuClass works. Since there are several authors for these samples, the coding style might be slightly different between each sample; however, the main idea is identical.

* ###**AIO: Temperature Sensor ([Hardware Link](http://www.seeedstudio.com/depot/Grove-Temperature-Sensor-p-774.html)) **    
      
    Since [UPM sensor and actuator](https://github.com/intel-iot-devkit/upm/blob/master/examples/python/grovetemp.py) repository supports python module for this temperature sensor running on the Intel Edison, we integrate its Python module to our temperature sensor WuClass as below.
    
  ![](temp_python_wuclass.png)
      
  ![](../../no1.png)Import the Python library supported by UPM.  
  ![](../../no2.png)Configure which pin will be used to connect to temperature sensor.  
  ![](../../no3.png)This refresh function will repeat every 500 msec according to the value of REFRESH_RATE. Thus, the value function will retrieve temperature value periodically.    
  ![](../../no4.png)Add WuClass to MyDevice and create a instance as described in the last section.  
  ![](../../no5.png)This loop function will repeat every 100 msec. The setProperty function will send celsius value of its WuClass (i.e. cls) from first property (i.e. pID=0).  
  
  
* ###**PWM: MOSFET ([Hardware Link](http://www.seeedstudio.com/depot/Grove-MOSFET-p-1594.html))**  
   

* ###**I2C: LCD RGB Backlight ([Hardware Link](http://www.seeedstudio.com/depot/Grove-LCD-RGB-Backlight-p-1643.html))**  
   We adopt [pyupm_i2clcd library](https://github.com/intel-iot-devkit/upm/blob/master/examples/python/jhd1313m1-lcd.py) to control this LCD RGB Backlight device.    
   
  ![](grove_lcd_python_wuclass.png)  
  
    ![](../../no1.png)This is I2C address for Grove LCD. The I2C addres is unique among all the I2C devices.  


* ###**UART: Serial MP3 Player ([Hardware Link](http://www.seeedstudio.com/depot/Grove-Serial-MP3-Player-p-1542.html))**  
   We adopt [pyupm_wt5001 library](https://github.com/intel-iot-devkit/upm/blob/master/examples/python/wt5001.py) to control this MP3 Player device.  
 
 ![](mp3_python_wuclass.png)  
 
     ![](../../no1.png)The only UART port of Intel Edison is at pin 0.     