##3.2 Board Setup for Intel Galileo Gen 2

<!---- (俊翰-testing, 振豪-format) ---->

This section shows **four** steps to set up an Intel Galileo Gen2 for running WuKong.     

**Step 1. Linux Image Preparation:** To prepare a bootable microSD card with the Linux environment. 

**Step 2. Board Assembly:** To assemble the Intel Galileo board.

**Step 3. Board Configuration:** To setup a password for Intel Edison so that we can use ssh command to access Intel Edison.  

**Step 4. Python Tool Installation:** To install required Python libraries for WuKong.   

**Step 5. Download WuKong Source Code:** To clone the WuKong source code from GitHub to the Galileo board.  


* **  

* **Step 1. Linux Image Preparation**  
 
  Unlike Edison, Galileo Gen2 doesn't have a built-in flash memory so that we need to prepare a bootable microSD card. 
  
  Please see the following website to make a bootable microSD card:  
  https://software.intel.com/en-us/get-started-galileo-linux-step1   
  
* ** 
  
* **Step 2. Board Assembly**

  According to the Intel official IoT website, the required hardware includes:
  * Intel Galileo Gen 2,
  * A SD card (>2GB),
  * 6 pin Serial to Type A USB cable (e.g. FTDI cable # TTL-232R-3V3)
  * a 7-15V DC power supply rated at least 1500mA.
  * (Optional) WiFi adaptor (e.g. Intel® Centrino® Wireless-N 135 or Intel® Centrino® Advanced –N 6205).

  Once the hardware is prepared, please follow the lower part of the following website to assemble an Intel Galileo Gen 2 board:  
  https://software.intel.com/en-us/get-started-galileo-linux-step2  
  
  After assembling the Intel Galileo Gen2 board, please see the following website to set up the serial communication with the board:  
  https://software.intel.com/en-us/get-started-galileo-linux-step3  
  
* **

* **Step 3. Board Configuration**  
  If you have a recommended WiFi module as mentioned in Step 2, see the following website on how to install the WiFi adapter and to configure the WiFi setting.  
  https://software.intel.com/en-us/get-started-galileo-linux-step4  
    
  If not, see the following website to set up an ethernet connection. Instead of using a serial terminal, it uses Arduino IDE to communicate with board.  
  https://software.intel.com/en-us/articles/intel-galileo-getting-started-ethernet  
  
* **

* **Step 4. Python Tool Installation**
  * Copy the following instructions to `/etc/opkg/base-feeds.conf`
```
src/gz all http://repo.opkg.net/edison/repo/all
src/gz edison http://repo.opkg.net/edison/repo/edison (?edison?)
src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32
```

  * Install **pip** and other tools
```bash
opkg update  
opkg install python-pip   
pip install twisted  
pip install python-cjson  
pip install gevent  
opkg install sqlite3   
pip install netifaces  
opkg install git  
```

* **

* **Step 5. Download WuKong Source Code (Updated 2017.11.14)**   
  * Clone the source code and download to your preferred working directory on the IoT board.

    ```bash
    git clone -b release0.4 https://github.com/wukong-m2m/wukong-darjeeling.git 
    ```  