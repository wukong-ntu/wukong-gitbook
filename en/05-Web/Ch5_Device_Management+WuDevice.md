## Device Management

*  How to Enter Device Management Page  
 
   Click **Device Management** on the top menu  


*  How to Add devices to the WuKong System    

   1.  To add a new device, click **Add Node** button. This action will put the master program in **ADD MODE** as the message shows "ready to ADD" 

    ![](../Ch4/Intel_Sound/9.png)
   
  2.  Start the device program and let it to enter learning mode. This step depends on which type of device program is going to run.   
  
      * For Running Python Script:  
      ```bash  
      cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/  
      python udpdevice_blink_led.py <IP address pf PC> <IP address of Edison>:<any port>  
      #Go to the folder of Python WuClass  
      #Execute Python device to be included to WuKong system   
      ```  
      
      * For Running ELF file: 
      ```bash
      cd <path_of_darjeeling>/darjeeling
      darjeeling.elf -n <network interface> -a  
      ctrl + c
      darjeeling.elf -n <network interface>
      #Go to the folder of darjeeling    
      #Execute darjeeling ELF file with "-a" to enter learning mode   
      #Once get node id, terminate the program and restart without "-a" flag to leave learning mode  
      #The network interface for Intel Edison is wlan0, and for Intel Galielo is wlp1s0  
      ```  
  3.  Press **Stop to complete operation** to let master program back to **STOP MODE**     
 
     ![](../Ch4/Intel_Sound/11.png)

*  How to Remove devices from the WuKong System    

   1.  To remove a device, click **Remove Node** button. This action will put the master program in **DELETE MODE** as the message shows "ready to DELETE" 

    ![](../Ch4/Intel_Sound/35.png)
   
  2.  Restart the device program and let it to enter learning mode. This step depends on which type of device program is going to restart.   
  
      * For Restarting Python Script:  
      ```bash    
      ctrl + c
      python udpdevice_blink_led.py <IP address pf PC> <IP address of Edison>:<any port>  
      ctrl + c
      #Go to the terminal of device program which is going to be removed    
      #Restart Python device program to exclude it from WuKong system  
      #Wait for the message showing "STOP" to terminate the program  
      ```  
      
      * For Restarting ELF file: 
      ```bash
      ctrl + c
      darjeeling.elf -n <network interface> -a  
      ctrl + c
      #Go to the terminal of device program which is going to be removed      
      #Restart darjeeling ELF file with "-a" to exclude it from WuKong system     
      #The network interface for Intel Edison is wlan0, and for Intel Galielo is wlp1s0    
      #Wait for the message showing "STOP" to terminate the program    
      ```  
      ![](../Ch4/Intel_Sound/36.png)
      
  3.  Press **Stop to complete operation** to let master program back to **STOP MODE**     
 
     ![](../Ch4/Intel_Sound/37.png)
    
    
*  How to Set Location for Each Device         
  
   Modify the device location and press Set Location button to restore
 
 ![](../Ch4/LED_Control/27.png)
 
 
 
*  How to Discover Devices   

   ![](../Ch4/LED_Control_C/c_21.png)

  

        

*  How to Check Sensor Profile of Each Device   

   Press **Details** button   

   ![](../Ch4/LED_Control/28.png)
