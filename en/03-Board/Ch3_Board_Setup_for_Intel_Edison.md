##3.1 Board Setup for Intel Edison
<!---- (俊翰-testing, 振豪-format) ---->

There are **four** steps to set up an Intel Edison as a WuKong device. 

**Step 1. Board Hardware Assembly:** To assemble the Intel Edison module on its Arduino extension board.

**Step 2. Board Configuration:** To setup a password on the Intel Edison so that we can use the ssh command to access the board.  

**Step 3. Firmware Update:** To obtain the compatible Yocto image, which is 159.devkit at the time of this writing, to support a larger root partition size and better Python tools.  

**Step 4. Python Tool Installation:** To install the required Python libraries for running WuKong.   

**Step 5. Download WuKong Source Code:** To clone the WuKong source code from GitHub to the Edison board.  

* **  

* **Step 1. Board Hardware Assembly**

 There are two types of extension boards designed for the Intel Edison module: the Arduino extension board, and the mini breakout board. In this chapter, we use the Arduino extension board since it is more convenient to connect sensor kit without soldering. 
 
 Please see the following website on how to assemble an Intel Edison board:  
 https://software.intel.com/en-us/articles/assemble-intel-edison-on-the-arduino-board  
 
 After that, you can see the following website on how to set up a serial terminal to communicate with the board.  
 https://software.intel.com/en-us/get-started-edison-linux-step3
 

* **

* **Step 2. Board Configuration**

  * To configure the board, enter the following command in the serial terminal opened in Step 1:
```bash
configure_edison --setup
```
 
  * When prompted, you must enter a chosen password so that the board can be accessed through the **ssh** command later on.   
  
    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/03-Board/fig3-1-0.png)

  * When prompted, you can enter a name for the board, or the name **"root"** will be given if it is left empty.  
 
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/03-Board/fig3-1-1.png)

  * The next step is the WiFi configuration. Type "Y" to setup WiFi and the board will start to scan network services. Once the board finishes scanning, choose a network SSID and then enter the network password if required. The following screen shows an example setting.

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/03-Board/fig3-1-2.png)
  * If you need to connect to a different network service, you can later use the following command to configure it again:  
```bash
configure_edison --wifi
```

* **

* **Step 3. Firmware Update**

  Make sure the firmware version of your board is the latest one. You can use the following command to check:  
```bash
configure_edison --version
```

  If it shows "159.devkit",  the firmware is a compatible one. If not, please see the following website on how to update its firmware:  
  https://software.intel.com/en-us/iot/hardware/edison/downloads  
  
* **

* **Step 4. Python Tool Installation**
  * Copy the following instructions to `/etc/opkg/base-feeds.conf`
```
src/gz all http://repo.opkg.net/edison/repo/all
src/gz edison http://repo.opkg.net/edison/repo/edison
src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32
```

  * Install **pip** and other tools  
```bash  
opkg update  
opkg install python-pip
opkg install sqlite3 
opkg install git 
pip install twisted 
pip install python-cjson  
pip install gevent  
pip install netifaces  
```

* **

* **Step 5. Download WuKong Source Code**   
  * Clone the source code and download to your preferred working directory on the IoT board.

    ```bash
    git clone -b release0.4 http://github.com/wukong-m2m/wukong-darjeeling
    ```   



