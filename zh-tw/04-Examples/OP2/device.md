##4.2.2 新增裝置

1. 使用 Chrome 瀏覽器開啟主控台介面： http://localhost:5000  
  <!-- (Currently, only Chrome browser supports FBP editor)  -->
   
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/19.png)

2. 點選 **Device Management** 分頁並點擊 **Discover Node** 按鈕來獲得初始狀態。
        
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/20.png)

3. 點擊主控台上的 **Add Node** 按鈕來新增物聯網裝置。
    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/201.png)
        
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/21.png)

4. 開啟一個新的終端機並且 SSH 登入至物聯網開發版。
    
  ```bash
  ssh root@<IP address of IoT board>
  ```

5. 當 SSH 登入成功後，移至物聯網開發版上的 Python 悟空類別的資料夾。
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/   
  ```   
        
6. 執行裝置程式 udpdevice_blink_led.py 。這個程式會啟動一個裝置並且從通訊閘取得一個裝置識別碼，之後在此裝置上產生兩個悟空物件，分別是 Button 跟 Light Actuator。
  ```bash
  python udpdevice_blink_led.py <IP address of Gateway> \
  <IP address of IoT board>:<arbitrary port number>
  ```
      ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/fig4-2-4.png)

7.  當主控台出現下列文字時，點擊 <font color="red">Stop to complete operation</font> 按鈕。
     
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/24.png)

8.  點擊 <font color="red">Discover Nodes</font> 按鈕以刷新裝置列表。  

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/26.png)

9. 更改裝置的位置並點擊 <font color="red">Set Location</font> 按鈕以儲存。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/27.png)

10. 點擊 <font color="red">Details</font> 按鈕即可查看此 Python 裝置的傳感器資料。

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/28.png)

