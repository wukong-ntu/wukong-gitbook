## Implement a WuClass from Definition


In this section, we take previous LED-controlled FBP as an example to explain the basic template of the WuClass. We will start from WuClass [using Python Programming Language](Ch6_Using_Python_Programming_Language.md) and then move to WuClass [using C Programming Language](Ch6_Using_C_Programming_Language.md).

Currently, WuKong has been ported to several platforms including Intel Edison, Intel Galileo, and Raspberry Pi. Although they share the same WuClass definition of WuKongStandardLibrary.xml as mentioned in the last page, their implementation is platform-dependent and language-dependent. Therefore, before implementing a WuClass, you have to choose one of the platforms and one of the programming languages supported in WuKong. After choosing platform and programming language, find the WuClass sample files and create your WuClass in the same folder according to the table below.
       

| WuClass File Path | Python language | C language |
| -- | -- | -- |
| Intel Edison | <*path_of_source_code*>/wukong-darjeeling/wukong/gateway/udpwkpf/ | <*path_of_source_code*>/wukong-darjeeling/src/lib/wkpf/c/posix.mraa/native_wuclasses/  |
| Intel Galileo | <*path_of_source_code*>/wukong-darjeeling/wukong/gateway/udpwkpf/ | <*path_of_source_code*>/wukong-darjeeling/src/lib/wkpf/c/posix.mraa/native_wuclasses/ |
| Raspberry Pi | <*path_of_source_code*>/wukong-darjeeling/wukong/gateway/udpwkpf/ | <*path_of_source_code*>/wukong-darjeeling/src/lib/wkpf/c/posix.mraa.raspberrypi/native_wuclasses/ |  
   
   
Once the WuClass has been implemented in the corresponding path, we can modify the enable_wuclasses.xml file and build the darjeeling ELF file again. With this new ELF file, the device will have a capability of the new WuClass so that a new application of this new WuClass can be deployed to the device just as we have done in the [chapter 4](../04-Examples/Ch4_The_First_Example.md).




