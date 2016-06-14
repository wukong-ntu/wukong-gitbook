#Chapter 5: 悟空管理介面  
<!--
* **需求**

  像第四章一樣，執行 主控台(master) 和 通訊閘(gateway)後，我們可以連到悟空的網頁介面(web interface)。預設畫面是資料流編程編輯器(flow-based programming)。
  
  下載與安裝Chrome流覽器。 目前，悟空Web介面只支援Chrome和Opera。
  
  使用Chrome流覽器開啟網頁介面。 預設是：http://localhost:5000

* **悟空Web介面**  

 在悟空管理介面中，分為三個主要部分，前端(front-end)，後端(back-end)和通訊閘(gateway)。 前端是悟空的圖形使用者介面，使用者可以使用此介面知道並管理所有裝置(device)和應用程式(application)。後端是python tornado伺服器，執行前端傳來的功能需求。通訊閘是純軟體模組，用來橋接(bridge)不同的網路區段。

 -->
接著，我們會示範如何使用悟空管理介面：
  1. 網路管理(network management)： 展示悟空的網路架構和解釋如何設定主控台和通訊閘。
  2. 裝置管理(device management)：如何將裝置加入悟空系統、設定其位置(location)和獲取裝置可使用的悟空物件(WuObject)。
  3. 應用程式管理(application management)：建立一個簡單的資料流編程，建立與資料流相對應的傳感器表格，部署應用程式到各個裝置上。
  4. 應用程式商店(application store)：一個可以儲存和分享使用者的應用程式的介面。

 
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/05-Web/FBP_editor_layout.png)
