### 4.1.1 Start the Master and Gateway

1. On your computer, download the source code from github as below:

   ```bash
    git clone -b release0.4 https://github.com/wukong-m2m/wukong-darjeeling.git
   ```

2. Build infuser

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/src/infuser/  
   gradle
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-0.png)

3. Copy the configuration file for Master

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/config/  
   cp master.cfg.dist master.cfg
   ```

4. Run the Master

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/master/   
   python master_server.py
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-1.png)

5. On the computer, open a new terminal to copy the configuration file for gateway program

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/  
   cp gtwconfig.py.dist gtwconfig.py
   ```

6. Configure gtwconfig.py

   ```bash
   # Use ifconfig command to check the network information.   
   ifconfig
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-2.png)

   ```bash
   vim gtwconfig.py 
   # Change MASTER_IP to the IP address of the Master.     
   # Change TRANSPORT_INTERFACE_ADDR according to yout network interface above.
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-3.png)

7. Run the gateway program

   ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/
    python start_gateway.py
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-4.png)



