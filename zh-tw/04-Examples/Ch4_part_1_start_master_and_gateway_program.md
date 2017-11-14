##4.2.1 Start Master and Gateway

The instructions in this section are slightly different from Section 4.1.1 since the gateway software in run on an IoT board (either Edison or Raspberry Pi). Therefore, after starting Master, we will  access the IoT board remotely to start the gateway program.   

<font color="red">**Note:**</font> Before entering this section, if you have run the example in the last section, you need to follow the instructions in the [Section 4.1.5](../discovery_issue.md) to flush the cache files.

1. On the computer, download the source code from github as follows.  

  ```bash
  git clone -b release0.4 https://github.com/wukong-m2m/wukong-darjeeling.git
  ```

2. Build infuser
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/src/infuser/  
  gradle 
      ```      
        
3. Copy the configuration file for Master  
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/wukong/config/  
  cp master.cfg.dist master.cfg  
  ```

4. Start Master    
    ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/master/   
    python master_server.py   
    ```

5. From the computer, open a new terminal and use the SSH command to connect to the IoT board. Although we use Edison in this section, the same operations can be used on Raspberry Pi.    
    ```bash
    ssh root@<IP address of Intel Edison board> 
    ```
    
6. Download the source code to the IoT board after SSH is successful started.
    ```bash
    git clone -b release0.4 http://github.com/wukong-m2m/wukong-darjeeling  
    ```   
    ![](../img/LED_Control/fig4-2-0.png)

7. Copy the configuration file for gateway.  
    ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/  
    cp gtwconfig.py.dist gtwconfig.py
    ```
         
8. Configure gtwconfig.py according to the network information.
   ```bash
   ifconfig 
   # Use this command to check network interface of IoT board. 
   # In this case, the network interface of Edison is wlan0.  
   ```
      ![](../img/LED_Control/fig4-2-1.png)
 
   ```bash
   vim gtwconfig.py 
   # if you cannot use vim, please install it with "opkg install vim"  
   # Change MASTER_IP to IP address of your computer
   # Change TRANSPORT_INTERFACE_ADDR to network interface of IoT board
   ```
      ![](../img/LED_Control/fig4-2-2.png)

9. Start gateway program on the IoT board    
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/
  python start_gateway.py
  ```  
      ![](../img/LED_Control/fig4-2-3.png)

