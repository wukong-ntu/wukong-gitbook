###4.2.3 Build and Deploy an FBP Application


We will now define a LED control application using the FBP editor and deploy this application to the IoT board. 

1.  Click and enter the **Application Management** page.   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/29.png)

2.  Click the **Create New** button and then enter the name for application.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/30.png)

3.  Click on the FBP name to enter the FBP composition canvas.   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/31.png)

4.  Click the **WuClasses** tab.  

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/32.png)

5.  Scroll through the WuClass list to find the Button component. Select it and  click the **Add** button.  A Button component will appear on the composition canvas.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/33.png)

6.   Repeat the last step to add the Light_Actuator component. Please be noted that the new added component will overlap the previous one. You have to draw them apart.     

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/34.png)      

7.  To create a link between two components, first click on the source component. After the source component has been highlighted, select the source property. Then move the cursor and click the  property on the destination component.   
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/35.png)

8.  Check whether the source and destination of the data link is correct. If not, change the property in the dropout menu.   

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/36.png)

9.  Press the **Application** tab and click the **Save** button.  The FBP has now been created.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/38.png)

10.  We will now start the deployment process. First click the **Map** button to start the Master FBP mapping selection process.   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/39.png)

11. After Master has made its selection, the mapping result will be displayed as below.  If the mapping is successful, each FBP component should have a device ID and a port number.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/40.png)

12.  Click the **Deploy** button  to start the FBP execution.

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/41.png)

13.  Master will display some messages and show if the deployment is successful. 

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/42.png)




