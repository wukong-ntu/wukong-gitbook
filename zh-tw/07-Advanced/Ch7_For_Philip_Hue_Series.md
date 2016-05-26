###7.2 Web Client WuClass for Philip Hue  

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
  ![](img/hue_user.png)

   3. Add udpdevice_philip_hue_\*.py  to WuKong according to [Section 5.2](../Ch5/Ch5_Device_Management.md).
   
   4. Create the FBP and set the initial value    
       
      An example Philip Hue FBP can be seen as below. Button is used to turn on/off Philip Hue Bulb, and slider is used to adjust the intensity of the red color. The rest of properties can be filled in the left menu, which will pop up once the Philip Hue component is clicked. 
       ![](img/hue_fbp.png)

       ![](img/no1_2.png)Currently, WuKong has not supported string type, so we have to convert ip address to integer first. Since the integer length in the WuKong is only 2 bytes, we have to use two properties ip_high and ip_low to indicate the ip address of Philip Hue bridge. Here is an example:
 
       ![](img/hue_ip_example2.png)

       ![](img/no3.png)index is the id of each Philip Hue lamp, which shows on the Hue app as below.

       ![](img/hue_app2.png)

       ![](img/no4.png)The range of rgb light intensity is from 0 to 254. The number filled in this blank will be set as the default value for the FBP component.      
   
   5.  Deploy this FBP according to [Section 5.3](../05-Web/Ch5_Application_Management.md)