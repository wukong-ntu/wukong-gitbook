##1.1 How to use this book

This book is designed to walk you through (a) configuring the WuKong middleware and development environment, (b) setting IoT devices for WuKong adoption, and (c) developing new IoT applications on WuKong. The book is organized in six chapters. Chapter 1 is an introduction of the WuKong middleware and the system building environment. Chapters 2 and 3 show the steps for building configuring the software and hardware environment. Chapter 4 gives two simple WuKong execution examples, one without using any actual IoT device and the other using a single IoT device. Chapter 5 go through various WuKong development and management capabilities. In  Chapter 6, we show how to implement and add specific device capabilities (called WuClasses) in your projects. 


### Suggested Chapters


This book is designed for three groups of target readers: *device builders*, *application developers*, and *system installers*. Different chapters may be useful for people with different roles when building WuKong-based IoT systems. 

<!--  
> The WuKong middleware and development environment is designed for device builders, service installers, and application developers. To save your time, you may choose appropriate materials to read based on selected roles. 
-->


Below are the recommended materials for each role. 
  * Device Builder (hardware specific, wuclass programming): Chapters 2, 3 and 6  
  * Service Installers (Master and network setup): Chapters 4.\*.1, 4.\*.2 and 5.1
  * Application Developers: Chapters 4.\*.3, 5.2, and 5.3


### Target Hardware  

WuKong is a distributed middleware consisting of three system components: Master, gateway, and IoT device. Each component can be run independently on specific or shared hardware platforms.  
  
  * Master must be run on Linux-based computers with network connections and Web server capability. It is used to produce target code for specific IoT devices and send executable codes to these devices. A machine with an adequate computing capability is desired for running Master.
  * Gateways are used to connect to IoT devices and forward network packets among devices on different subnets and/or using different networking protocols. They can be run on Linux-based servers or simple gateway machines.
  * IoT devices are designed to provide sensing inputs and actuation controls. They may be run on tiny sensing and control boards, such as those without operating system support. Some IoT boards with sensing and control capabilities may have vendor-supported RTOS or embedded Linux. In addition, WuKong can define virtual devices running on PC or servers to collect user input and to display user interface or media.

Figure 1(a-c) show these possible configurations for WuKong systems. A WuKong-based IoT application can be run using only a Linux-based computer or server, with Master, gateway, and virtual devices all on the same machine (Figure 1a). Some WuKong-based IoT applications may be run on several physical sensing devices and a Linux server running Master and gateway (Figure 1b). A full scale WuKong system may have a dedicated Master running on a (local or cloud) server, several gateway units each managing devices on different subnets or protocols (e.g. WiFi, ZWave, Zigbee), and many IoT devices running on physical boards and/or virtual software modules on servers (Figure 1c). 

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/01-HowToUse/fig1a.png)



![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/01-HowToUse/fig1b.png)

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/01-HowToUse/fig1c.png)

For information on how to run a WuKong-based IoT application using only Linux-based computers, please read Chapters 2, 4.1, 5, and 6.

For information on how to run a WuKong-based IoT application both on Linux-based computers and IoT boards, please read Chapters 2, 3, 4.2, 5, and 6.  