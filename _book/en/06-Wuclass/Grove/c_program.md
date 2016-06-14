## C Program

With the sample code and propagation API in the [last section](../Ch6_Using_C_Programming_Language.md), we can proceed to write WuClasses for each connection type. We will start first on AIO connection type.     

* ###**AIO: Temperature Sensor** ([Hardware Link](http://www.seeedstudio.com/depot/Grove-Temperature-Sensor-p-774.html))    

  Many sensors belong to this connection type, including temperature sensor, light sensor, slide potentiometer, sound sensor and etc. Since the WuClass format of all the AIO sensors are quite similar, only the temperature sensor is presented here.    
  
    ![](temperature_c_wuclass.png)
    
    We have skipped the same comment as in the [last section](../Ch6_Using_C_Programming_Language.md).   
    ![](../../no1.png)Define a global mraa structure variable of AIO connection type, whose name should be unique among all WuClasses.   
    ![](../../no2.png)Line 25 to line 27 refers to the temperature converting formula from [wiki page](http://www.seeedstudio.com/wiki/Grove_-_Temperature_Sensor).    
    
  
* ###**PWM: MOSFET ([Hardware Link](http://www.seeedstudio.com/depot/Grove-MOSFET-p-1594.html)) **  
  
  ![](mosfet_c_wuclass.png)
     We usually use MOSFET to regulate DC voltage supply to LED so that if we change the voltage level, the intensity of LED will also change correspondingly.   
     ![](../../no1.png)This header file is revised from [upm C++ source code](https://github.com/intel-iot-devkit/upm/tree/master/src/cjq4435) to control the PWM period and dutycycle.   
     ![](../../no2.png)Enable a PWM capable pin (pins 3, 5, 6, 9 of Intel Edison) and enter desired PWM period.   
     ![](../../no3.png)The range of dutycycle is 0 to 1, and the range of brightness is 0 to 255. Thus, WuKong can send an analog value to MOSFET to regulate its dutycycle. 
  
  

* ###**I2C: LCD RGB Backlight ([Hardware Link](http://www.seeedstudio.com/depot/Grove-LCD-RGB-Backlight-p-1643.html))**
  
  ![](grove_lcd_c_wuclass.png)
     
     ![](../../no1.png)This header file is revised from [Suli-compatible C++ library](https://github.com/Seeed-Studio/LCD_RGB_Backlight_Suli) to control the LCD; however, its I2C address is wrong and should be replaced with the one in [this liabry](https://github.com/Seeed-Studio/Grove_LCD_RGB_Backlight/blob/master/rgb_lcd.h).   
     ![](../../no2.png)Although Intel Edison mini-breakout board supports six I2C buses, for Intel Edison Arduino extension board, we can only use sixth bus for I2C device as mentioned in the [mraa webpage](http://iotdk.intel.com/docs/master/mraa/edison.html).  
     ![](../../no3.png)There are many useful functions defined in the LCD_RGB_Suli.h file. This function is used to set background light color of LCD.  
     ![](../../no4.png)This function can print out the character at the place of LCD's cursor.  


* ###**UART: Serial MP3 Player ([Hardware Link](http://www.seeedstudio.com/depot/Grove-Serial-MP3-Player-p-1542.html))**  
 ![](mp3_c_wuclass.png)
     ![](../../no1.png)This header file is revised from [upm c++ source code](https://github.com/intel-iot-devkit/upm/tree/master/src/wt5001) to control Grove MP3 player.   
     ![](../../no2.png)The only UART port of Intel Edison is at pin 0.   
     ![](../../no3.png)The default baud rate of Grove MP3 player is 9600.  
     ![](../../no4.png)There are many useful functions defined in MP3_wt5001.h including play, pause, stop, queue, adjusting volume, etc.
