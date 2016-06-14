##5.3 應用程式管理(application management)
###創建資料流編程(flow-based programming)  

<!--
*This section  is revised from [PREVIOUS WUKONG UI MANUAL](https://docs.google.com/document/d/1d06id4TxZu5Cp6MvyJ4-2rgaHDvMKR29IIUpdW72_IY/edit#).*
-->
點選 **應用程式管理 (Application Management)**，會列出目前已有的應用程式(application)。 我們可以經由點選**建立新的應用程式(Create New)**加入一個新的應用程式，或點選![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/7.png) 刪除一個應用程式。點選應用程式的名稱可以進入資料流編程(flow-based programming)的修改模式。


![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/0.png)

*  加入組件

  點選左側菜單**悟空類別(WuClass)**可以看到可用的物件(Object)，物件儲存於WuKongStandardLibrary.xml。接著，選擇想要的物件後點選**加入(ADD)**或雙擊在畫布上產生一個新的物件。下圖表示選取了感光器(Light_Sensor)物件。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/1.png)

 感光器(Light_Sensor) 物件有兩個參數。輸入屬性會以灰色顯示，輸出屬性會以白色顯示。在這個例子中，"更新速度(refresh rate)" 是表示此傳感器的多久測量一次(毫秒(ms))，"目前值(current value)"表示感光器(Light_Sensor)的收集到的資料。  
 
 在接下來的範例中，我們會建立一個應用程式：當感光器(Light_Sensor)的值低於某一個特定數值時，打開燈。這個範例會包含四個物件：   
  1.感光器(Light_Sensor) 物件：產生一個0到255的值   
  2.閥(threshold) 物件：比較light sensor的值是否低於設定的值   
  3.滑標(slider) 物件： 設定threshold的值   
  4.發光器(light actuator) 物件： 代表一個燈泡   
 
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/2.png)  
    
    
*  建立連線   

  在將所需的物件放入畫布後，將各物件的屬性鏈接(link)。  
  1. 點選想連接的來源物件(source object)  
  2. 點擊來源物件的屬性，一條鏈接(link)將會產生  
  3. 點選接收端(receiver)的物件的屬性  
  4. 會跳出一個視窗確認兩側想鏈接的屬性  
  
  下圖為加入了所需的物件和鏈接。滑標(slider)輸出至閥(threshold)。
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/4.png)  
   

*  設定位置(location) 

  當部屬程式(deploy)時，主控台會嘗試尋找適合的裝置執行物件。由於已知的裝置中可能有複數的物件符合條件，我們使用位置來標示我們想使用的裝置。

  為了設定物件的位置，將鼠標移到 空白的**位置(Location)**表格上，直到**裝置樹(Tree Node)**出現，如下圖所示。
   
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/8.png)    
   
   點擊 **裝置樹(Tree Node)**，會跳出一個畫面讓使用者選著目前已知的物件的位置。

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/9.png)  


###部屬應用程式

當使用者完成一個應用程式，使用者可能想執行它。
點擊左側菜單的 **應用程式(Application)**。

為了更好的控制和獲取中間過程的結果，部屬應用程式目前分為三個步驟。在未來，主控台將會自動執行三個步驟。
三個步驟為"目前裝置(current)", "配對(map)" , "部署程式(deply)"，如圖所示。

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/11.png)  


*  第一步 -- 目前裝置   

  點擊 "目前裝置(current)" 會列出當前尋找裝置的結果。當首次點擊時，主控台會探詢已知的裝置和其能力(WuObject)。會花上一些時間，之後會使用其結果。
  
  每一個裝置的內容會橫列表示，當裝置是紅色時，表示裝置目前無法連接，黑色表示裝置存活。  
  
  如果預期與結果不符，回到**裝置管理(Device Management)**重新作尋找裝置。  

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/13.png)
  
  
*  配對(map)

  當主控台知道他有哪個資源可用後，主控台依照資料流編程(FBP)配對物件(Object)和裝置(devices)。
  
  點擊**“配對 (Map)”** 將會使主控台嘗試依照資料流編程配對物件和裝置
  結果會顯示在一個表格如下：
  1. 悟空物件(WuObject)的名稱
  2. 配對的裝置ID
  3. 配對的裝置的通訊埠(port)

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/12.png)


*  部署程式  
  
  在配對結束後，應用程式需經由**部署程式 (Deploy)**部屬。這將會持續一段時間，大約30秒。部屬時，log會顯示主控台的過程，包含編譯和上傳到各個裝置。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP/14.png)



