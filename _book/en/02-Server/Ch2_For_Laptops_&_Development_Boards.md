##2.2 Tools to Support IoT Devices

If you plan to use physical IoT devices in your application, you still need to complete all instructions in the last section ([Sec 2.1](Ch2_For_Laptops.md)).  After that, you need to install MRAA and OpenSSL as shown below to support Edison, Galileo or Raspberry Pi 2. MRAA (https://github.com/intel-iot-devkit/mraa)  is a low-level skeleton for the I/O communication, so that you do not need to use the GPIOs direct manipulation. This library offers similar methods ike the Arduino methods to control or read from the board pins. OpenSSL is used for connecting to the devices from the Linux computer during WuKong setup. 

* **Install MRAA for Intel Edison, Galileo**

  * **For 32-bit OS**    

    * Install cmake  
```bash
sudo apt-get install cmake  
```

    * Download MRAA source code
```bash
git clone https://github.com/intel-iot-devkit/mraa.git
```
      
    * Build and install MRAA 
```bash
cd mraa && mkdir build && cd build 
cmake ..
make && sudo make install
```

  * **For 64-bit OS**  
    
    * Install 32-bit toolchain
```bash
sudo apt-get install g++-4.8-multilib g++-multilib gcc-4.8-multilib gcc-multilib
sudo apt-get install lib32gcc-4.8-dev cmake
```

    * Download MRAA source code
```bash 
git clone https://github.com/intel-iot-devkit/mraa.git
```
  
    * Build and install MRAA 
```bash
cd mraa && mkdir build && cd build
export CFLAGS=-m32  
export CXXFLAGS=-m32  
cmake .. -DBUILDARCH=i386  
make && sudo make install
```
* **

* **Install OpenSSL on Intel Edison or Galileo**
  
  Go to http://packages.ubuntu.com/trusty/i386/libssl-dev/download  
  Download the latest libssl-dev_X.X.XX-1ubuntuX.XX_i386.deb via "security.ubuntu.com/ubuntu"  
```bash
# (replace <path_of_openssl> with the correct path of libssl-dev package)
dpkg -x libssl-dev_X.X.XX-1ubuntuX.XX_i386.deb libssl-dev
sudo apt-get install libssl-dev  
sudo apt-get install libssl1.0.0:i386  
cd /usr/lib/i386-linux-gnu/  
sudo cp -a <path_of_openssl>/libssl-dev/usr/lib/i386-linux-gnu/* .
cd ../../include/  
sudo cp -a <path_of_openssl>/libssl-dev/usr/include/i386-linux-gnu .
```

* **

* ** Install MRAA for Raspberry Pi**

    * Install cmake 
```bash
sudo apt-get install cmake  
```

    * Download MRAA source code 
```bash
git clone https://github.com/intel-iot-devkit/mraa.git
```

    * Download the toolchain for Raspberry Pi
```bash
git clone https://github.com/raspberrypi/tools
```
  Append the tools directory path to the environment variable PATH as follows.  
  For 32-bit OS, enter 
```bash
export PATH=$PATH:~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin
```
  or, for 64-bit OS, 
```bash
export PATH=$PATH:~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin
```
  as the last line of the bash startup file ~/.bashrc, and then use the source command to execute the script.
  
    * Build and install MRAA
```bash
cd mraa && mkdir build && cd build
CC=arm-linux-gnueabihf-gcc CXX=arm-linux-gnueabihf-g++ cmake .. 
         -DBUILDSWIGNODE=OFF -DBUILDSWIGPYTHON=OFF -DBUILDARCH=arm
CC=arm-linux-gnueabihf-gcc CXX=arm-linux-gnueabihf-g++ make
sudo make install
```

* **

* ** Install OpenSSL for Raspberry Pi**

  Check the version of libssl-dev from the terminal on your Raspberry Pi using the following instruction:
```bash
apt-cache show libssl-dev | grep [Vv]ersion
```

  Then go to http://archive.raspbian.org/raspbian/pool/main/o/openssl/ and download the same version of `libssl-dev_X.X.XX-XXXX_armhf.deb` and `libsslX.X.X_X.X.XX-XXXX_armhf.deb`

  ```bash
  # (replace <path_of_openssl> with the correct path of libssl-dev package)
  dpkg -x libssl-dev_X.X.XX-XXXX_armhf.deb libssl-dev
  sudo cp -a <path_of_openssl>/libssl-dev/usr/lib/arm-linux-gnueabihf /usr/lib/
  sudo cp -a <path_of_openssl>/libssl-dev/usr/include/arm-linux-gnueabihf /usr/include/
  sudo cp -a <path_of_openssl>/libssl-dev/usr/include/openssl /usr/include/arm-linux-gnueabihf

  # (replace <path_of_openssl> with the correct path of libssl package)
  dpkg -x libsslX.X.X_X.X.XX-XXXX_armhf.deb  libssl
  sudo cp -a <path_of_openssl>/libssl/usr/lib/arm-linux-gnueabihf /usr/lib/
  ```
