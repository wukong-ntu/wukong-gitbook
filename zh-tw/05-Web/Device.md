##5.2 裝置管理(Device Management)

在此章節，我們將會解解如何使用悟空主控台去管理裝置。

* 點選**裝置管理(Device Management)** 
 
     ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/LED_Control_of_Ch4/201.png)
        
*  將裝置加入悟空系統

   1.  點選**加入裝置(Add Node)** 按鈕，主控台會進入**加入(ADD)**模式，並提示"準備好加入裝置(ready to ADD)" 
   
     ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/Intel_Sound_of_Ch4/9.png)
   
  2.  啟動裝置程式，並令其進入**認知模式(learing mode)**  
  
      ```bash  
      cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/  
      python udpdevice_blink_led.py <此網域的通訊閘的IP> \
      <此裝置使用的網路介面的 IP>:<任意的通訊埠>  
      
      #到Python悟空類別的資料夾下啟動裝置程式
      ```  
 
  3.  點擊**停止並完成操作(Stop to complete operation)** 讓主控台進入 **停止(STOP)**模式
 
     ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/Intel_Sound_of_Ch4/11.png)

*  從悟空系統中移除裝置   

   1.  點選**移除裝置(Remove Node)** 按鈕，主控台會進入**移除(DELETE)**模式，並提示"準備好移除裝置(ready to DELETE)"

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/Intel_Sound_of_Ch4/35.png)
   
  2.  啟動裝置程式，並令其進入**learing mode** 
  
      ```bash    
      python udpdevice_blink_led.py <IP address of gateway program> \
      <此網域的通訊閘的IP><此裝置使用的網路介面的 IP>:<任意的通訊埠>  
      #進入想移除的裝置上，重啟Python程式
      #等到Web介面顯示 "STOP" 後停止程式
      ```  
      ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/Intel_Sound_of_Ch4/36.png)
      
  3.  點擊**停止並完成操作(Stop to complete operation)** 讓主控台進入 **停止(STOP)**模式   
 
     ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/Intel_Sound_of_Ch4/37.png)
    
    
*  為每個裝置設定位置(location)
  
   修改裝置位置並點選**設定位置(Set Location)**儲存
 
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/LED_Control_of_Ch4/27.png)
 
 
 
*  **尋找裝置 (Discover Nodes)** 可以顯示有多少裝置是主控台已知的

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/21.png)

  

        

*  **細節(Details)** 可以確認各個裝置上的傳感器資料
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/LED_Control_of_Ch4/28.png)
