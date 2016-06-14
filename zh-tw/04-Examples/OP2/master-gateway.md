##4.2.1 啟動主控台及通訊閘程式

此章節的步驟與章節 4.1.1 相比有些許的不同。因為通訊閘程式將執行在物聯網開發版上，所以當我們執行主控台程式後，需遠端連線到物聯網開發版上，並執行訊閘程式。

<font color="red">**注意:**</font> 在進入此章節前，如果您已執行過上一個章節的範例，您必須依照 [章節 4.1.5](../OP1/issue.md) 的步驟清除快取資料。

1. 請先輸入下列指令從 github 下載程式碼到您的電腦。

  ```bash
  git clone -b release0.4 http://github.com/wukong-m2m/wukong-darjeeling
  ```

2. 建立 infuser。
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/src/infuser/  
  gradle 
      ```      
        
3. 複製主控台設定。
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/wukong/config/  
  cp master.cfg.dist master.cfg  
  ```

4. 確認主控臺的網路介面資訊
   ```bash
   ifconfig  
   # 此範例中，主控臺的網路介面是 wlan0  
   # 主控臺的網路位址是192.168.4.17  
   ```
   <font color="red">**Note:**</font> 這個網路位址爲步驟9的MASTER_IP。  
   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/4_2_1_master_ifconfig2.png)


5. 執行主控台程式。
    ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/master/   
    python master_server.py   
    ```

6. 開一個新的終端機，並且使用 SSH 指令連結到物聯網開發版。此章節，我們使用 Edison 當作範例， Raspberry Pi 也可以執行相同的指令。    
    ```bash
    ssh root@<IP address of Intel Edison board> 
    ```
    
7. 當SSH成功登入後，下載程式碼到物聯網開發版。
    ```bash
    git clone -b release0.4 http://github.com/wukong-m2m/wukong-darjeeling  
    ```   
    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/fig4-2-0.png)

8. 複製通訊閘程式的設定。
    ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/  
    cp gtwconfig.py.dist gtwconfig.py
    ```
         
9. 編輯 gtwconfig.py 檔案。
   ```bash
   ifconfig 
   # 使用此指令來獲得物聯網開發版的網路資訊
   # 此範例中，Edison 的網路介面是 wlan0
   ```
      ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/fig4-2-1.png)
 
   ```bash
   vim gtwconfig.py 
   # 如果你無法使用 vim ，請用 "opkg install vim" 指令來安裝
   # 在 MASTER_IP 位置填入主控台所在電腦的IP
   # 在 TRANSPORT_INTERFACE_ADDR 填入物聯網開發版的網路介面
   ```
      ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/fig4-2-2.png)

10. 執行通訊閘程式
  ```bash
  cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/
  python start_gateway.py
  ```  
      ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control/fig4-2-3.png)

