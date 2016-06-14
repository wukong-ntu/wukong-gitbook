##7.2 Web Client WuClass for Philip Hue  

In this section, we show how to create and use the Philip Hue WuClass in FBP.

* ###Controlling Philip Hue Light in WuKong##  
   1. To allow users build their own apps, Philip Hue provides the HTTP API to get information and   control Hue systems. Before using HTTP API, we must get the URL address of the Hue hub. Please follow http://www.developers.meethue.com/documentation/getting-started to find the URL address by API Debugger Tool. The URL address will be something like:
```bash
/api/1028d66426293e821ecfd9ef1a0731df/lights  
```
The long number above is the username of the Philip Hue Bridge, which is created if you follow the instructions of the above website.   

   2. Go to the directory of Philip Hue WuClass and change the URL address definition in a Philip Hue utility file according to your bridge.   
```bash
cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/
vim udpdevice_philip_hue_*.py  
# change the user around line34 according to user name of your hue hub.
```
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_user.png)

   3. Add udpdevice_philip_hue_\*.py  to WuKong according to [Section 5.2](../05-Web/Ch5_Device_Management.md).
   
   4. Create the FBP and set the initial value    
       
      An example Philip Hue FBP can be seen as below. Button is used to turn on/off Philip Hue Bulb, and slider is used to adjust the intensity of the red color. The rest of properties can be filled in the left menu, which will pop up once the Philip Hue component is clicked. 
       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_fbp2.png)

       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1_2.png)Currently, WuKong has not supported string type, so we have to convert ip address to integer first. Since the integer length in the WuKong is only 2 bytes, we have to use two properties ip_high and ip_low to indicate the ip address of Philip Hue bridge. Here is an example:
 
       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_ip_example2.png)

       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)index is the id of each Philip Hue lamp, which shows on the Hue app as below.

       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_app2.png)

       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)The range of rgb light intensity is from 0 to 254. The number filled in this blank will be set as the default value for the FBP component.      
   
   5.  Deploy this FBP according to [Section 5.3](../05-Web/Ch5_Application_Management.md)   

* ###Implementing Web Client WuClass      
In the following, we're going to see how web client WuClass is implemented to control the color and on/off state of Philip Hue. Through web client wuclass, we can also connect to other IoT products which provide HTTP API as Philip Hue. Since Hue has a series of products and all of them can be controlled by the same HTTP API, we create an utility file with commonly used classes to avoid repetition codes. This utility file is philip_hue_utils.py as below.      
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_1.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_2.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_3.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_4.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_5.png)

 Note: please refer to Twisted official website for more detailed information about how to use Twisted wevb client. (http://twistedmatrix.com/documents/current/web/howto/client.html)   

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1.png)http_get_path and http_put_path are defined according to HTTP API of Philip Hue.      
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no2.png)put_command is a method used to send HTTP PUT request. The parameters include a request method, a request URI, the request headers, and an object which can produce the request body. The agent is responsible for resolving the hostname into an IP address and connecting to it.    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)get_gamma is used to send HTTP GET request to retrieve gamma value from Hue. Since the gamut of Hue products fall into three different areas and not all of the RGB values can be mapped to those gamuts, we need to calibrate each RGB value with gamma value.      
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)The Response object of HTTP GET request has a deliverBody method which makes the response body available.        
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no5.png)The BeginningPrinter protocol in this example is passed to Response.deliverBody and the response body is then delivered to its dataReceived method as it arrives.  
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no6.png)After the content of HTTP body is parsed, the gamma value can be determined.      
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no7.png)When the body has been completely delivered, the protocol's connectionLost method is called.       

 Next, the WuClass below uses the web client in the utility file to control Philip Hue.  
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_hue_wuclass_1.png)

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_hue_wuclass_2.png) 

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_hue_wuclass_3.png)
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1.png)Import web client from the utility file.    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no2.png)With the property value of Hue bridge ip, username, and index, an object of web client can be created.   
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)Too frequent requests will cause Hue bridge to postpone reponse or drop message, so we have to set a minimum request period to ensure the functionality. In this case, the minimum period is set as 0.55 sec.      
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)Use the method of web client to get gamma value.     
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no5.png)Use gamma value to calibrate the RGB value.      
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no6.png)These two commands will be sent to the Hue bridge as a HTTP body.    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no7.png)FileBodyProducer is responsible to produce a HTTP body object.      
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no8.png)Use put_command to send HTTP request to the Hue bridge.  
