##4.1.2 新增裝置

在我們利用悟空部署物聯網程式前，主控台必須先找到能夠執行此一程式的裝置。在這一個章節，我們會說明如何使用主控台上的裝置管理功能。

1.  使用 Chrome 瀏覽器開啟主控台介面：http://localhost:5000  
   <!--- (Currently, only the Chrome browser supports FBP editor)   --->
 
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/19.png)

2.  點選 **Device Management** 分頁並點擊 **Discover Node** 按鈕來獲得初始狀態。
     ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/8_0.png)

3.  點擊主控台上的 **Add Node** 按鈕來新增裝置。
    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/8.png)

    注意: 如果沒有顯示出 <font color="red">ready to ADD</font> 的訊息的話請點擊 <font color="red">Stop to complete operation</font> 按鈕並重試一次。
    
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/9.png)

4.  開啟一個新的終端機並且移至裝置程式所在的資料夾下。

    ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/   
    ```
        
5.  執行裝置程式 udpdevice_intel_sound.py 。這個程式會啟動一個包含 Intel_Sound 悟空類別的裝置並且從通訊閘取得一個裝置識別碼。  
      
    ```bash
    python udpdevice_intel_sound.py <IP address of gateway> \
    <IP address of device program>:<arbitrary port number>
    ```
    
    <font color="red">注意: 當裝置程式啟動後，裝置會從主控台取的一個裝置識別碼。</font>
    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-5.png)  
    
6.  點擊 <font color="red">Stop to complete operation</font> 按鈕。

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/11.png)

7.  點擊 <font color="red">Discover Nodes</font> 按鈕以刷新裝置列表。
  
    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/13.png)

8.  點擊 <font color="red">Details</font> 按鈕即可查看此裝置得傳感器資料。
  
    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/14.png)  

9.  裝置的位置可以用下列方法設定。 
 
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/Intel_Sound_15.png)
   
10.  重複步驟 3 至步驟 9 執行另一個名為 udpdevice_logic.py 的裝置程式。之後您會在裝置管理介面看到下面的畫面。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/18.png)
