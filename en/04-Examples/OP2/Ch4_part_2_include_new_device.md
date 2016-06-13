###4.2.2 Include a New Device

1. Use the Chrome browser to open FBP editor: http://localhost:5000  
  <!-- (Currently, only Chrome browser supports FBP editor)  -->
   
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/19.png)

2. Enter the Device Management page to check the initial state  
        
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/20.png)

3. Click the **"Add Nodes"** button to start including the IoT board for Master management. You should see the message stating Master is "ready to ADD". 
    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/201.png)
        
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/21.png)

4. Open another terminal and use SSH command to connect to the IoT board.   
    
	```bash
	ssh root@<IP address of IoT board>
	```

5. After SSH is established, go to the folder of the Python WuClass on the IoT board.
    
	```bash
	cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/   
	```   
        
6. Run the device program udpdevice_blink_led.py. This Python program will start the device to receive a node ID from the WuKong gateway, and then the two WuObjects, Button and Light Actuator, residing on the device.  
  ```bash
  python udpdevice_blink_led.py <IP address of Gateway> \
  <IP address of IoT board>:<arbitrary port number>
  ```
      ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/fig4-2-4.png)

7.  Once Master has found the board (displaying the message as shown), stop the inclusion process.           
     
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/24.png)

8.  Check the device management list again by clicking the Discover Nodes button.  

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/26.png)

9. Modify the device location and press the Set Location button to save it.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/27.png)

10. Press the Details button to check the sensor profile of the Python device.

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/28.png)

