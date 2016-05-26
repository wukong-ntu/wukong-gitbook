##5.2 Device Management

In this section, we will show how to use the WuKong Master to manage devices.  

* Click on the **Device Management** top menu  
 
     ![](img/LED_Control_of_Ch4/201.png)
        
*  Adding devices to a WuKong system    

   1.  To add a new device, click the **Add Node** button. This action will put  Master  in the **ADD** mode as the message shows "ready to ADD". 
   
     ![](img/Intel_Sound_of_Ch4/9.png)
   
  2.  Start the device program and let it enter the learning mode.  
  
      ```bash  
      cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/  
      python udpdevice_blink_led.py <IP address of gateway program> \
      <IP address of device program>:<arbitrary port number>  
      #Go to the folder of Python WuClass  
      #Execute Python device to be included to WuKong system   
      ```  
 
  3.  Press **Stop to complete operation** to let Master return to the **STOP** mode.    
 
     ![](img/Intel_Sound_of_Ch4/11.png)

*  Removing devices from a WuKong system    

   1.  To remove a device, click the **Remove Node** button. This action will put the master program in the **DELETE** mode with a message showing "ready to DELETE" 

    ![](img/Intel_Sound_of_Ch4/35.png)
   
  2.  Restart the device program and let it to enter the learning mode. 
  
      ```bash    
      ctrl + c
      python udpdevice_blink_led.py <IP address of gateway program> \
      <IP address of device program>:<use identical port number as adding this device program>  
      ctrl + c
      #Go to the terminal of device program which is going to be removed    
      #Restart Python device program to exclude it from WuKong system  
      #Wait for the message showing "STOP" to terminate the program  
      ```  
      ![](img/Intel_Sound_of_Ch4/36.png)
      
  3.  Click **Stop to complete operation** to let Master go back to the **STOP** mode.    
 
     ![](img/Intel_Sound_of_Ch4/37.png)
    
    
*  How to set location for each device         
  
   Modify the device location and click the Set Location button to save it.
 
 ![](img/LED_Control_of_Ch4/27.png)
 
 
 
*  The **Discover Nodes** button can be used to show the current devices known to Master.   

   ![](img/FBP/21.png)

  

        

*  The **Details** button can be used to  check the sensor profile on each device.

   ![](img/LED_Control_of_Ch4/28.png)
