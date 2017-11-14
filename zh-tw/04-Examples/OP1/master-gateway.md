## 4.1.1 啟動主控台及通訊閘程式

1. 請先輸入下列指令從 github 下載程式碼到您的電腦

   ```bash
   git clone -b release0.4 https://github.com/wukong-m2m/wukong-darjeeling.git
   ```

2. 建立 infuser

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/src/infuser/  
   gradle
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-0.png)

3. 複製主控台設定

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/config/  
   cp master.cfg.dist master.cfg
   ```

4. 執行主控台程式

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/master/   
   python master_server.py
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-1.png)

5. 開一個新的終端機，並且複製通訊閘程式的設定

   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/  
   cp gtwconfig.py.dist gtwconfig.py
   ```

6. 編輯 gtwconfig.py 檔案

   ```bash
   # 使用 ifconfig 指令來獲得網路資訊   
   ifconfig
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-2.png)

   ```bash
   vim gtwconfig.py 
   # 在 MASTER_IP 位置填入主控台的IP     
   # 在 TRANSPORT_INTERFACE_ADDR 填入根據上面方法取得的網路介面卡編號
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-3.png)

7. 執行通訊閘程式

   ```bash
    cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/
    python start_gateway.py
   ```

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/fig4-1-4.png)



