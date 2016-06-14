#Chapter 1: Introduction

The WuKong project at the [NTU-IoX Center](http://ccc.ntu.edu.tw)  has built an intelligent middleware for IoT systems. The goal of the WuKong project is to help users design and develop hardware-independent IoT applications, so that they can be easily configured and dynamically deployed on vendor-independent IoT platforms. 

The WuKong IoT middleware has the following major features:
* **Virtualized IoT Devices**: Virtualizing IoT devices allows hardware-independent application design and simplifies IoT services migration among devices without redefining applications. Consequently, one can deploy an IoT application on different hardware platforms without using hardware- and/or network-dependent application codes.

* **Flow-Based Programming environment**: WuKong provides a graphical flow-based programming (FBP) tool. In each FBP, a user can define the data and control flow to build an IoT application.  All the user has to do is to select the type of services from a predefined WuKong component library, drag and drop them on the programming canvas, and then connect them with directed links. The application flow diagram will then be used to map logical services onto appropriate physical  devices during application deployment.

* **Heterogeneous and Virtual services**: The WuKong middleware provides virtual machines on heterogeneous platforms to simplify IoT application deployment and migration.  Virtual IoT services can also be implemented (in Python) to support Web-based data services or UI running on servers,  computers and smartphones. In addition, Darjeeling-based Java Virtual Machine is included in the WuKong middleware so that a system can dynamically add bytecodes on each device.

* **Deployment-time Service Mapping**: To support heterogeneous and constant-evolving hardware platforms, WuKong delays the binding between logical IoT services and physical IoT devices until deployment. Consequently, during application development, platform-dependent properties and configurations such as port assignment and pin assignment are minimized. The platform-dependent properties are collected by the WuKong Master when a device registers itself in a WuKong system. The Master will use these properties to produce a proper configuration and generate required executable code for each IoT application.

In this document, we present the instructions and examples on how to set up a WuKong environment and develop WuKong IoT applications. The document includes the description on the required system toolchains, the device hardware and firmware setup,  Master installation and operations, device sensing connections, and advanced IoT device support. All hardware and software used are openly available for access and installation. By making this project open, we hope to make IoT much easier to build and to deploy in the future.

