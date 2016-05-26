###7.1  TCP Server Connection


In this section, we explain how to create a TCP connection between the Intel RealSense SDK and the WuKong FBP components. We also show an FBP application on how to adopt a RealSense camera in an IoT application.  

* ###Connecting Intel RealSense Camera with WuKong 

  1.  The Intel RealSense camera provide many features for facial analysis, hand and finger tracking, sound processing, and augmented reality. In this example, we use only the feature of finger tracking to show how to add a TCP client in WuKong FBPs. Since RealSense has provided its SDK on the website https://software.intel.com/en-us/realsense/home, we simply use its HandsViewer code. The example is under the Intel folder, Intel/RSSDK/sample/FF_HandsViewer/. 

  2.  Our modified HandsViewer example code can be found from 
https://drive.google.com/open?id=0B31WAUDq3a3uZWZzb21iR0NwMDQ where we have included a socketclient file and add a function to define how to send signals. Using this code to replace the original source code under Intel/RSSDK/sample/FF_HandsViewer/src folder, you can use Microsoft Visual Studio to open the solution file called FF_HandsViewer_vs201*. 
When a RealSense camera is plugged in a USB port, an interactive window can be seen as below. This window shows the skeleton of the user's fingers and identify the gesture by showing results on the log output. In this picture, it has identified the gesture as two_fingers_pinch_open.       

![](img/realsense.png)

 In the HandsViewer.cpp file, a socket client is created on line 535 and passed to the DisplayGesture function which is responsible to identify gestures. After getting the gesture, the SendMessage function will send different pre-defined number to there TCP server. In that way, WuKong can respond to each gesture accordingly.  
 
 In WuKong, the TCP server is implemented in the udpdevice_mux_gesture_control.py, under the  RealSenseProtocol class as shown below. This class implements the user-defined network protocol parsing and handling for TCP servers, as an example of explaining how we can support different protocols in WuKong.      
![](img/realsense_protocol2.png)
 ![](img/no1.png) This class inherits basic.LineReceiver which is a protocol that receives lines and/or raw data, depending on the mode. For further information, please refer to https://twistedmatrix.com/documents/9.0.0/api/twisted.protocols.basic.LineReceiver.html   
 ![](img/no2.png) In the lineReceived mode, each line received becomes a callback to lineReceived. In other words, data is the packet received from other TCP client. So data is a message sent by the SendMessage function in the HandsViewer.cpp file.   
 ![](img/no3.png) Once received a message, the code can split and parse the message according to the design. In this WuClass, we define the mode and gesture properties. The meaning of gesture is straightforward, but the meaning of mode requires some explanation. Since RealSense doesn't provide the sample code to identify the number gesture, we cannot change mode simply by using the number gesture. One alternative is using True or False to indicate whether a user wants to change mode or not. The changing mode property corresponds to the "tap" gesture. When a user posts a tap gesture (similar to pressing a virtual button), the mode property will propagate a signal to next component.   
 ![](img/no4.png) Every time we receive new data, we have to reset mode and gesture before calling the setProperty function because WuKong adopts the even-driven model. If we don't reset the property, the same continual mode and gesture signal will be propagated only once.  
 ![](img/no5.png) The previous state of mode property will be stored and compared to the new mode property, or otherwise we will count mode change incorrectly.  
 ![](img/no6.png) Finally, the gesture value is propagated to the next component.    
 
 
* ###FBP Using Intel RealSense Camera     
We now show a simple FBP that uses RealSense Gesture output to control several applications running on a computer. In the following figure, the RealSense WuClass produces two output properties, mode and gesture, that will be linked to a switch component. The switch component then uses the gesture readings to issue control commands to one of the three applications, video player, Hangout communication, and LED light. 

![](img/FBP_RealSense.png)

