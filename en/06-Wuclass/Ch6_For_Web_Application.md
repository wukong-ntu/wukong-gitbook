###7.3 Web Server WuClass for UISlider
In this section, we first show how to use UISlider in a WuKong FBP. 
We also present how to use the Twisted Web server to build the UISlider WuClass.  

* ###FBP Using UISlider   
  1. This FBP has three components:  

    * UISlider  
Just as the output of a slide potentiometer has a range from 0 to vcc volt, a UIslider  receives a number from the browser and sends it to the next component. In this FBP, the next component of UISlider is a Threshold.  
    * Threshold  
This component  uses the output  from the upper UISlider as a threshold and compares this value with the output  of another UISlider. The operator is used to decide the comparison rule which can be LT, LTE, GT, and GTE. The default operator is LT. The output property will propagate **True** to the next component.   
    * Number  
The Number component is mainly  for debug purposes. It will display the received value on the console screen.   
![](img/Logic/1.png)  
  
  2. Initial value setting  
  To specify which UISlider is to be used, each UISlider will be given a different pair (device, port) of initial (device, port) values. The values for different components must be different. 
  
![](img/Logic/2.png)
![](img/Logic/3.png)
  
  3. To see how the data flow between components, we add a ShowAll class which, when it receives a request from a browser,  shows all current values of all component on the browser (the left side of the figure below). 
  
![](img/Logic/4.png)   

  4. When a user uses the url to send a request to change the output number of the upper UISlider, we can see the data propagation from the ShowAll request just mentioned. In this case, it sends a request to set the threshold property to 100.  
![](img/Logic/5.png)   
  
  5. Use a request to change the output value of the lower UISlider to 80, we can see the data propagation as above. In this case, it sends a request to set the value property to 80, and the ouput of the Threshold component will become True.   
 ![](img/Logic/8.png)
 

* ####UISlider WuClass   
  
  The Slider WuClass is shown below. The details are explained on certain lines as footnotes at the end of this section.
  ![](img/uislider_wuclass2.png)  
 ![](img/uislider_wuclass3.png)

![](img/no1.png)render_GET is a method to be implemented to support GET requests from clients. And render_GET returns string according to our implementation as a response.  

![](img/no2.png)We can get the values of each http request by parsing the arguments.   

![](img/no3.png)When we use these flags for the addClass function, the class will be used to create new WuObjects. That's why when we add only one UISlider WuClass, we still can have two UISliders in an FBP.    

![](img/no4.png)Since we can have several identical FBP components in one FBP, we must decide which component is requested by the client.      

![](img/no5.png)The device property and port property of UISlider are used to find the requested one. That is why we have to fill the initial values when drawing a FBP.  

![](img/no6.png)putChild can be used to create the URL name for a Resource instance.  
  
![](img/no7.png)Specify the port to serve http get request. In this case, http://localhost:11006/slider is the base to make the http GET request.   

