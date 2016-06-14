
##5.1 網路管理(Natwork managerment)  

在悟空的應用程式(application)部署(deploy)之前，我們必須設定好網路，主控台(master)、通訊閘(gateway)和裝置(devices)之間的連線。 如同 [Section 1.1](../01-HowToUse/README.md) 提到，一個悟空系統由三個部分組成：主控台、通訊閘和裝置(實體裝置或虛擬裝置)。 各個部分可以都在同一個網域內執行或都在不同網域內執行。在此章節，我們會先展示三個部分皆於同網域內執行，之後會展示於不同網域上執行。

* **
#### 同個網域

網路設定如下列附圖。此網路設定包含：一台筆電、兩個含有作業系統的物聯網版子(edison & raspberry Pi)和一個不含作業系統的物聯網版子(Arduino)。
筆電可執行章節4.1提到的系統程式。含有作業系統的物聯網版子可執行章節4.2提到的通訊閘和裝置，不含作業系統的物聯網版子只可以當作一般裝置使用。
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/subnet/network_management_LAN.png)
        
下列步驟是用來啟動同個網域下的主控台和通訊閘。跟章節4.2.1完全相同。

1. 確認筆電連接到同個網域。如果網路環境改變，請依照章節4.1.5回復原始設定。

2. 確認infuser已編譯。 如果未編譯，請執行以下步驟：
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/src/infuser/  
   gradle 
   ``` 
3. 確認設定檔案(config file)是否創建。如果未建立，請執行以下步驟。
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/config/  
   cp master.cfg.dist master.cfg  
   ```
4. 啟動主控台(master)。
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/master/   
   python master_server.py   
   ```     
   
5. 在啟動主控台後，開啟終端機(terminal)並啟動通訊閘(gateway)。通訊閘可以選擇在筆電或是含有作業系統的物聯網版子上執行。注意：在首次啟動時，必須依照主控台，通訊閘的順序執行。 

6.  確認通訊閘的設定檔案是否創建。如果未建立，請執行以下步驟：
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/  
   cp gtwconfig.py.dist gtwconfig.py
 
   # 如果要在物聯網版子上執行通訊閘
   # 需在物聯網版子中有程式碼，可經由git下載
   # git clone http://github.com/wukong-m2m/wukong-darjeeling
   ```  
 
7. 確認通訊閘的網路介面(network interfaces),例如: eth0, wlan0...。

8. 根據通訊閘的網路介面設定 gtwconfig.py。
 
   ```bash
   vim gtwconfig.py  

   # 將 MASTER_IP 改為主控台程式的IP
   # 將 TRANSPORT_INTERFACE_ADDR 改為通訊閘使用的網路介面
   ```
9. 啟動通訊閘。   
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/
   python start_gateway.py
   ```   
   
10. 使用Chrome瀏覽器連入Web介面，預設為: http://<*主控台ip*>:5000. 
   
* **
#### 不同網域

網路設定如附圖。在此次範例中，有三個子網域(subnet)：A,B,C。子網域A中有raspberry Pi且Pi的ip為192.168.16.3，子網域B中有edison且edison的ip為192.168.4.18。在各個子網域必須各有一個通訊閘，由於目前我們未處理網路地址轉換(NAT)的問題，主控台(master)必須在子網域C執行。

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/subnet/network_management_subnets.png)

下列步驟用來啟動主控台和通訊閘

1. 在每個路由器中開啟9010和9001的通訊埠轉發。通訊埠9010用於主控台從通訊閘傳接封包，通訊埠9001用於通訊閘與主控台溝通。下列圖片是ASUS RT-AC68 WiFi router的設定畫面。  
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/subnet/port_forward.png)

2. 在每個路由器中設定不同的網址前綴(network prefix)。原因是如果兩個子網域使用相同的網址前綴，主控台無法辨認其封包(packet)是從哪個子網域傳出。因此，在範例中，我們使用不同的網址前綴。
 
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/subnet/ip_wifi_router.png)

3. 在子網域中的主控台，設定如同單一網域，請依照單一網域中，步驟1到4設定並啟動。

4. 在啟動主控台後，使用終端機登入Raspberry Pi。

5. 確定Raspberry Pi中有程式碼，如果沒有請依照下列步驟下載
   ```bash
   git clone http://github.com/wukong-m2m/wukong-darjeeling 
   ```
6. 確認通訊閘的設定檔案是否創建。如果未建立，請執行以下步驟： 
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/  
   cp gtwconfig.py.dist gtwconfig.py
   ```
7. 從每個路由器中找到路由器公共IP或WAN IP。在此範例中，子網域A的路由器IP為233.1.1.2，子網域B的路由器IP為     233.1.1.3，子網域C的路由器IP為233.1.1.4。  

8. 設定gtwconfig.py.       
 
   ```bash
   vim gtwconfig.py  

   # 將 MASTER_IP 改為主控台網域的WIFI路由器的公共IP
   # 此範例中，主控台IP為233.1.14
   # 將 TRANSPORT_INTERFACE_ADDR 改為筆電或Pi使用的網路介面
     
   ```
9. 在筆電或Raspberry Pi上啟動通訊閘
   ```bash
   cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/
   python start_gateway.py  
   ```

10. 重複步驟4到9設定子網域B的筆電或Edison。  

11. 使用Chrome連入(預設)http://<*主控台_IP*>:5000。如要在子網域A,B中存取，需在子網域C的路由器上，設定通訊埠轉發(port forwarding)。



