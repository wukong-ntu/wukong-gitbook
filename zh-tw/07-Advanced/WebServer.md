##7.3 使用網頁伺服器(Web Server)的悟空類別
   
在這個章節中，我們將先部署一個有使用網頁伺服器的悟空類別的應用程式，這個悟空類別的名稱是UISlider，意思是UI介面的旋轉電位器(以下稱爲UI旋轉電位器)，當了接如何使用這個悟空類別後，我們接者說明如何實作這個悟空類別。      

* ###使用UI旋轉電位器的應用程式   
  1. 這個應用程式共有三個元件：   
  
    * UI旋轉電位器(UISlider)   
如同旋轉電位器(Slider)的輸出從零到電源電壓(vcc)伏特，UI旋轉電位器會接收從瀏覽器傳來的數字(number)，並將這個數字轉換成短整數，短整數就成爲UI旋轉電位器的第一個屬性(number)的值，當值改變後，就會按照資料流被傳遞到下一個屬性。  
    * 閥值比較器(Threshold)
閥值比較器會將其第二個屬性(threshold)的值當做閥值，用來和第三個屬性(value)的值做比較，比較的方式將由第一個屬性(operator)的設定來決定，如果仔細對照元件函式庫的話，會發現這個屬性的資料型態是列舉，其中有LT(小於),LTE(小於和等於),GT(大於)和GTE(大於和等於)這四種選項，預設值是LT，比較後的結果會由第四個屬性(output)傳遞下去。    
    * 數值標示(Number)    
這個元件主要是用來偵錯，它會將接收到的值顯示在執行程式的畫面上。    
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/Logic/1.png)  
  
  2. 初始值設定   
  爲了要在應用程式中使用多個UI旋轉電位器物件，我們多定義了兩個屬性，分別是裝置識別號(device)與埠識別號(port)，每個UI旋轉電位器在部署前都需設定這兩個屬性的初始值，如此一來，當瀏覽器傳值給UI旋轉電位器的時候，才能明確地指定是傳給哪一個UI旋轉電位器。   
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/Logic/2.png)
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/Logic/3.png)
  3. 爲了解數據在資料流的傳遞過程，我們在UI旋轉電位器內加了一個名稱爲ShowAll的類別，可以透過瀏覽器把每個物件屬性即時的變化印出來，如同下圖中的左半部，在瀏覽器的網址列輸入localhost:11006/show。     
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/Logic/4.png)   

  4. 在下圖中，當我們透過瀏覽器傳值(number)100給UI旋轉電位器(較上的)時，從呼叫ShowAll的瀏覽器頁面中，可以看出來閥值比較器的閥值屬性(threshold)改變了，同時也可以確認傳遞的值爲100。  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/Logic/5.png)   
  
  5. 當我們透過瀏覽器傳值(number)80給UI旋轉電位器(較下的)時，從呼叫ShowAll的瀏覽器頁面中，可以看出來閥值比較器的比較值(value)改變了，接者，比較完這兩個屬性(threshold和value)後，就把比較的結果傳遞給數字標示物件。   
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/Logic/8.png)
 
* ###實作UI旋轉電位器(UISlider)的悟空類別
UI旋轉電位器的悟空類別的實作如下圖，由於這個悟空類別更新的方式與之前介紹的悟空類別不同，是每當有瀏覽器呼叫的時候做更新，所以在撰寫UI旋轉電位器時，我們沒有使用更新函式(update function)，而是直接將訪問屬性儲存區的函式寫在下圖的render_GET函式。
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/uislider_wuclass2.png)  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/uislider_wuclass3.png)

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1.png)render_GET函式的用途在於回應客戶端的HTTP GET請求，回傳的資料型態是字串，字串的內容視開發者實作而定。  

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no2.png)這三行程式是從HTTP的請求中把關於UI旋轉電位器屬性的值取出。     

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)當我們使用這個標記(FLAG_APP_CAN_CREATE_INSTANCE, FLAG_VIRTUAL)來加入悟空類別時，這個悟空類別就可以在部署應用程式的階段，被用來產生多個新的悟空物件，而不需先用addObject函式來產生新的悟空物件。   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)由於沒有使用更新函式，悟空屬性架構不會傳要被更新的物件給render_GET，於是這兩行程式比對同一個裝置上所有的悟空物件，直到找到UI旋轉電位器的悟空物件爲止。   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no5.png)由於同一個裝置上有可能有多個UI旋轉電位器，於是這行程式是用來篩選出所指定的UI旋轉電位器，這也是我們先前需要設定裝置識別號(device)與埠識別號(port)的初始值的原因。      

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no6.png)putChild函式是用來定義UI旋轉電位器的網址列關鍵字。  
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no7.png)標示哪一個埠會用來接收HTTP GET請求，在UI旋轉電位器的範例中，埠的識別碼是11006，網址列關鍵字是slider，所以http://localhost:11006/slider 是傳送HTTP GET請求的最前段的網址列。  
