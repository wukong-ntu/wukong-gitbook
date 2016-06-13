# Using Python programming language

* ###**Python WuClass Template**  

  All the Python WuClass samples can be found in the   <*path_of_source_code*>/wukong/gateway/udpwkpf/udpdevice\*.py and all of them are developed from a same template as shown below:  

 ![](required_python_wuclass_template.png)

* ###**LED-controlled sample code**  

  Based on this template, we have added two WuClasses to realize a LED-controlled application as the following sample code. If you have deployed that application to your device according to [chapter 4](../Ch4/Ch4_The_First_Example.md), this sample code will become more readable to you because these WuClasses are designed according to the application at chapter 4.  
  
  ![](python_wuclass_led_blink.png)

 ![](../no1.png)In addition to required libraries as shown in the template, mraa library is imported to control GPIO of Intel Edison board or Intel Galileo board.  

 ![](../no2.png)self.ID is an identifier of WuClass defined in the WuKongStandardLibrary.xml  

  ![](../no3.png)Use mraa library to specify which GPIO pin will be used and which direction will be set.  
  
  ![](../no4.png)This update function is called whenever there is a new data propagated to the light actuator just as button sends current value to light actuator through data link in the LED-controlled FBP.  
  
   **pID** is property identifier, the sequence number (starts from 0) in WuKongStandardLibrary.xml. For example, the on_off's pID of light actuator is 0; the curren_value's pID of button is 0; the refresh_rate's pID of button is 1.   
   
   **val** is a boolean value recevied from its data link.  
   
  ![](../no5.png)This **callLater** function will call self.refresh function after 0.1 sec.
    
  ![](../no6.png)As a source of data, the **setProperty** function of button will send value to data link according to its arguments. The first argument of setProperty function is pID. In this case, pID=0 indicates that the first property of button (current_value) is going to send data. And this data is the second argument.  
  
  ![](../no7.png)Add WuClass to MyDevice and create a instance. Use this instance to define which GPIO pin will be used. The second argument of addClass function is similar to virtual attribute of WuClass definition. 0 in addClass means native; 1 in addClass means virtual. However, this has not been implemented yet.  
  
  cls represents WuClass.  
  
  ![](../no8.png)Don't forget to add **reactor.run()** or else the value of button will neither be refreshed periodically nor be propagated to light actuator through data link.  


* ###**Summary**  
To summarize this section, here are several steps to write a Python Wuclass:
  * Copy the template to a new file at  <*path_of_source_code*>/wukong/gateway/udpwkpf/udpdevice_XXX.py  
  * Write a class for your sensor according to the pattern of Button, or write it for actuator according to the pattern of Light_Actuator.  
  * Add WuClass to MyDevice and configure its instance.

