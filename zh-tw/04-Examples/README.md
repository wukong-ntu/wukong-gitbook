#第4章: 悟空部署範例 

此章節會用兩個範例來說明如何在悟空系統下部署物聯網的環境。第一個範例的應用程式只需使用個人電腦，而不會用到任何開發版。第二個範例則會包含如何在 Intel Edison 及 Raspberry Pi 開發版上建立悟空的應用程式。兩個範例中的應用程式在運行階段皆只需要在區域網路內執行，而不需要連接到網際網路。  

<!--
we will use two examples to show the WuKong programming environment. This demonstration includes how to run WuKong system, manage devices, and deploy application. By finishing this section, you can have a basic idea about how WuKong works.
  
Before diving into the details, we first look at the WuKong programming editor as below. This editor is for creating Flow-Based Program (FBP), an intuitive IoT application flow. In this example, we use two IoT applications to follow two setups as mentioned in the **[Ch2](../Ch2/Ch2_WuKong_Environment_Setup.md)**. In the first FBP, when a UI buttion is clicked, it will send a signal to trigger Intel_sound component, and the the Intel theme will be played.  Similarly, in the second FBP, when the button changes its current value, this value will be propagated through a data link to control light actuator. 

-->

