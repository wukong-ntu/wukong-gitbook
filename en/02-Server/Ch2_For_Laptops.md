##2.1 Building WuKong Applications Using Computers Only

The instructions below are required to install the toolchains for building WuKong applications on computers and servers. The software to be installed includes Git, Java and Gradle. For running the Python version of WuKong, Python tools are also required. 

* **Install Git**   
```bash
sudo apt-get install git-core
```
  
* **Install Java**  
```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update && sudo apt-get install oracle-java7-installer
```
  
* **Install Gradle**  

  Download gradle 2.4 [HERE](https://services.gradle.org/distributions/gradle-2.4-all.zip) and extract it in a directory, for example, ~/gradle-2.4  
  Append this gradle directory path to environment variable PATH as below.  
  ```bash  
  vim ~/.bashrc  
  ```
  Add 
  ```bash
  export PATH=$PATH:~/gradle-2.4/bin
  ```
  after the last line of bash startup file ~/.bashrc, and then use the source command to execute the script  
```bash  
source ~/.bashrc
``` 

* **Install Python Tools**  
```bash  
sudo apt-get install libevent-dev  
sudo apt-get install python-dev  
sudo apt-get install python-setuptools  
sudo apt-get install libxml2-dev libxslt1-dev zlib1g-dev  
sudo apt-get install python-pip 
sudo pip install configobj simplejson gevent greenlet tornado jinja2 pyserial lxml  
sudo pip install netifaces  
sudo pip install python-cjson  
sudo apt-get install python-pyaudio  
```

<!---
**<font color="red">Note: You can skip Chapter 3 and jump to the Chapter 4.1 if you will not use Intel Edison or Raspberry Pi board. </font>**
--->
