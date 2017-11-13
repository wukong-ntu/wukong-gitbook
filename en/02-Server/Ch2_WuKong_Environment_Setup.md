##Chapter 2: Preparing the Development Environment on Server

<!--- (博文-testing, 振豪-format) --->
<!--
This chapter presents the instructions for preparing the WuKong development environment. To make it easy for readers to learn WuKong without connecting to any IoT device, we show in **[Step 1](Ch2_For_Laptops.md)** how to install WuKong and start WuKong applications using only virtualized devices on computers. In **[Step 2](Ch2_For_Laptops_&_Development_Boards.md)**, we show how to set up IoT devices (such as Intel Edison, Galileo and Raspberry Pi 2) to design applications that can sense and control the physical environment. 
   
In the following discussion, our instructions are specific to computers running **ubuntu 14.04 LTS**. We plan to provide the installation guide for OSX and Windows in the future. Before then, a possible option for laptop users is to install Virtualbox to run ubuntu on laptops.
-->

This chapter presents the instructions for preparing the WuKong development environment on a Linux-based computer. The instructions are tested on computers running **ubuntu 14.04 LTS**. We plan to provide the installation guide for OSX and Windows in the future. Before then, a possible option for PC users is to install Virtualbox to run ubuntu on their PC's. 

Four tools are required to run WuKong. Git is used to get the source code from the WuKong project. Java is necessary to run the Master software. Gradle is used for building the project.
And Python is used for implementing the WuKong Profile Framework. You can skip any step if your server has already installed that specific software.

* **Install Git**   
```bash
sudo apt-get install git-core
```
  
* **Install Java (Updated 2017.11.13)**  
```bash
sudo add-apt-repository ppa:openjdk-r/ppa 
sudo apt-get update && sudo apt-get install openjdk-7-jdk  
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
sudo pip install configobj simplejson gevent greenlet tornado jinja2 pyserial \
lxml  
sudo pip install netifaces  
sudo pip install python-cjson  
sudo apt-get install python-pyaudio  
```

In the next chapter, we will show how to set up IoT devices (such as Intel Edison, Galileo and Raspberry Pi 2) to develop applications that can sense and control the physical environment. But using the toolchains in this chapter, you can already develop a WuKong-based IoT application using just your computer as shown in the Section 4.1.