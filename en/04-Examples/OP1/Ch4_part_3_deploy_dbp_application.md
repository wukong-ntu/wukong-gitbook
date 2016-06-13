###4.1.3 Build an Application FBP

We are now ready to create an application to play the simple theme music.  

1.  Click and enter the **Application Management** page   

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/19.png)

2.  Clcik the **Create New** button and then enter the name of the application, "app1" in our example. <!--**(The dialog is in Chinese!!)**-->
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/20.png)

3.  Click on the application name just created to open the composition canvas. 

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/21.png)  

4.  Click on the **WuClasses** tab to show all WuClasses available for FBP composition. All existing WuClasses on the Master database will be displayed.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/22.png)  

5.  Scroll through the WuClass list to find the UIButton component. Click its selection button and the **Add** button at the bottom. Repeat this step for the Intel_Sound component.  Two component boxes will be shown on the composition canvas.
    
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/23.png)  

6.  To add a link between the two components, first  click on the source component. After the source component has been highlighted, click on the source property, the "click" property in this example. Then, move the cursor and click on the destination property of the destination component.   
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/24.png)     

7.  Check whether the source and the destination of the data link created are correct. If not, you can change them in the dropout menu.  
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/25.png)   

8.  (Optional) Enter the location for each component using the 5 steps in the following figures. Note that even if the location of each component is left empty, Master can still choose a suitable device for each component according to the device's sensor profile.   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/30.png)

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/31.png)

9.  Click on the **Application** tab and the **Save** button.   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/27.png)

10.  Click on the **Map** button to select the device to run each component.   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/27-1.png)   

11.  After the mapping procedure, the mapping results will be displayed as follows.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/28.png)   

12.  If everything is successful, you can now click on the **Deploy** button to run the application. 

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/27-2.png)   

13.  Messages will be displayed if WuKong is able to deploy the application successfully.  

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/29.png)