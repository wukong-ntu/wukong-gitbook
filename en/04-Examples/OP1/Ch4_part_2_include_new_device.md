##4.1.2 Include a New Device

Before we can deploy any IoT application on WuKong, Master must find the devices available to run it. In this section, we show how to use the device management capability in WuKong Master.

1.  Use the Chrome browser to open the Master interface: http://localhost:5000  
   <!--- (Currently, only the Chrome browser supports FBP editor)   --->
 
 ![](../img/LED_Control/19.png)

2.  Click on the **Device Management** tab and the **Discover Node** button to check the initial state.  
     ![](../img/Intel_Sound/8_0.png)

3.  Click the **Add Node** button to include a new device in Master.   
    
 ![](../img/Intel_Sound/8.png)

    Note: If the message shown is not <font color="red">ready to ADD</font>, press the <font color="red">Stop to complete operation</font> button and try the step again.  
    
  ![](../img/Intel_Sound/9.png)

4.  Open a terminal and go to the folder where the device program is stored.  

    ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/   
    ```
        
5.  Run the device program udpdevice_intel_sound.py. This Python program will start the device to receive a node ID from the WuKong gateway, and then the Intel_Sound WuClass on the device.  
      
    ```bash
    python udpdevice_intel_sound.py <IP address of gateway> \
    <IP address of device program>:<arbitrary port number>
    ```
    
    <font color="red">Note: When the device program is started, this device will get a Node ID assigned by the Master.</font>
    ![](../img/Intel_Sound/fig4-1-5.png)  
    
6.  Click on the <font color="red">Stop to complete operation</font> button.

   ![](../img/Intel_Sound/11.png)

7.  Click the <font color="red">Discover Nodes</font> button to refresh the device list. 
  
    ![](../img/Intel_Sound/13.png)

8.  The sensor profile of this device can be seen by clicking the <font color="red">Details</font> button.    
  
    ![](../img/Intel_Sound/14.png)  

9.  The location of the device can be changed as follows.  
 
   ![](../img/Intel_Sound/Intel_Sound_15.png)
   
10.  Add another device program called udpdevice_logic.py by repeating Step 3 to Step 9. After that, the device management list should be as follows.   

  ![](../img/Intel_Sound/18.png)
