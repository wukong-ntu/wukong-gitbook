## 3.3 Board Setup for Raspberry Pi Board

This section shows the **four** steps to set up an Raspberry Pi for running WuKong.

**Step 1. Raspbian Linux Image Preparation:** To prepare a bootable microSD card with the Linux environment.

**Step 2. Board Hardware Assembly:** To assemble the Raspberry Pi hardware and its accessories.

**Step 3. Board Configuration:** To setup a password for Raspberry Pi.

**Step 4. Python Tool Installation:** To install required Python libraries for running WuKong.

**Step 5. Download WuKong Source Code:** To clone the WuKong source code from GitHub to the Raspberry Pi board.

* \*\*

* **Step 1. Raspbian Linux Image Preparation**

  You can install with NOOBS as introduced in the following website:  
  [https://www.raspberrypi.org/help/noobs-setup/](https://www.raspberrypi.org/help/noobs-setup/)

  We also recommend to download the image and write it to the SD Card by instructions in the official website.  
  [https://www.raspberrypi.org/documentation/installation/installing-images/README.md](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)

  The image by default fills only 4 GB of the SD card. If you need more space, please refer to the solution in the official website.  
  [https://www.raspberrypi.org/documentation/configuration/raspi-config.md](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)

* \*\*

* **Step 2. Board Hardware Assembly**

  The required hardware materials include:

  * Raspberry Pi Board,
  * A SD card \(&gt;4GB\),
  * HDMI cable
  * a 7-15V DC power supply rated at least 1500mA.
  * Optional USB WiFi adaptor.
  * Optional Grove Pi extension board

  You can watch video such as [https://www.youtube.com/watch?v=JiTNdwD1fS0](https://www.youtube.com/watch?v=JiTNdwD1fS0) for the instructions to set up the Raspberry Pi hardware.

* \*\*

* **Step 3. Board Configuration**  
  Once powering on the RPi, You can either use GUI or login via SSH with account **pi** and password **raspberry**.

  * Change the keyboard layout by typing commands in a terminal.

    ```
    sudo nano /etc/default/keyboard
    ```

    Then find the following line:

    ```
    XKBLAYOUT=”gb”
    ```

    and change the "gb" to the two letter code for your country, say "us". Enter Ctrl+X to save the file and leave.

    Here \([https://en.wikipedia.org/wiki/ISO\_3166-1\#Current\_codes](https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes)\) is the list of current country codes from Wikipedia if you don't know your country code \(use the codes in the column labeled alpha-2\).

  * Change the update mirror site of Raspbian repository

    ```
    sudo nano /etc/apt/sources.list
    ```

    Replace the link "[http://mirrordirector.raspbian.org/raspbian](http://mirrordirector.raspbian.org/raspbian)" with the closest server from the official list. [https://www.raspbian.org/RaspbianMirrors](https://www.raspbian.org/RaspbianMirrors)

    ```
    deb http://mirrordirector.raspbian.org/raspbian jessie ...
    ```

* \*\*

* **Step 4. Toolchain Installation**  
  &lt;!--

  * Install MRAA and OpenSSL on RPi\*\*

    ```
    sudo apt-get update
    sudo apt-get install libssl-dev cmake
    git clone https://github.com/intel-iot-devkit/mraa.git
    cd mraa
    mkdir build
    cd build
    cmake .. -DBUILDSWIGNODE=OFF -DBUILDSWIGPYTHON=OFF
    make
    sudo make install
    sudo ldconfig
    ```

    --&gt;

  * Python Tool Installation  
    Install **pip** and other tools

    ```
    sudo apt-get update  
    sudo apt-get install python-twisted python-cjson python-gevent  
    sudo apt-get install sqlite3 python-netifaces
    ```

  * Optionally, install grovepi library and enable the I2C interface for the Grove Pi extension board in the terminal.

    ```
    sudo apt-get install python-smbus i2c-tools
    sudo raspi-config
    ```

    Once the menu shows up, select the **Advanced Options** and then **I2C** by Arrow and Enter keys. Select **Yes** to enable I2C interface and **Yes** to load the module by default. Finally, reboot the RPi.

    ```
    sudo reboot
    ```

    Check if the I2C is enabled by entering command in the terminal after reboot. If you have a Pi Model A, B+ or 2 B \(512MB memory\).

    ```
    sudo i2cdetect -y 1
    ```

    Otherwise, for Pi 1 B \(256MB memory\), run

    ```
    sudo i2cdetect -y 0
    ```

    It should show some address\(es\) like 20, 40, or 70 within the table.

    ```
    git clone https://github.com/DexterInd/GrovePi.git  
    cd <source code>/GrovePi/Software/Python  
    sudo python setup.py install
    ```

* \*\*

* **Step 5. Download WuKong Source Code \(Updated 2017.11.14\)**

  * Clone the source code and download to your preferred working directory on the IoT board.

    ```bash
    git clone -b release0.4 https://github.com/wukong-m2m/wukong-darjeeling.git
    ```



