##7.2 使用網頁客戶端(Web Client)的悟空類別   
<!--##7.2 Web Client WuClass for Philip Hue-->  

在這一章節中，我們將先說明如何使用現有的悟空類別來控制Philip Hue燈泡，接者說明此悟空類別如何使用網頁客戶端來連線Philip Hue的智慧橋接器(bridge)。   
<!--In this section, we show how to create and use the Philip Hue WuClass in FBP.-->   

###用悟空物件來控制Philip Hue燈泡  
<!--* ###Controlling Philip Hue Light in WuKong##-->  
   1. 爲讓使用者能開發應用程式來控制Hue系列的產品，Philip Hue開放了HTTP API供開發者使用，但在使用之前，我們需先取得智慧橋接器的網址，請參照Hue官方網站(http://www.developers.meethue.com/documentation/getting-started) 的說明，並使用API除錯工具(API Debugger Tool)來取得網址。網址如同以下樣式：    
```bash
/api/1028d66426293e821ecfd9ef1a0731df/lights  
``` 
中間的長字串代表智慧橋接器的使用者名稱，此名稱會在取得網址的過程中產生出來。  
<!--   1. To allow users build their own apps, Philip Hue provides the HTTP API to get information and   control Hue systems. Before using HTTP API, we must get the URL address of the Hue hub. Please follow http://www.developers.meethue.com/documentation/getting-started to find the URL address by API Debugger Tool. The URL address will be something like:
```bash
/api/1028d66426293e821ecfd9ef1a0731df/lights  
```
The long number above is the username of the Philip Hue Bridge, which is created if you follow the instructions of the above website.-->   

   2. 取得使用者名稱後，需要更改Philip Hue的悟空類別中原有的使用者名稱，更改步驟如下：   
```bash
cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/
vim udpdevice_philip_hue_*.py  
# 在大約第34行的地方，將原有的使用者名稱改寫成新取得的名稱。    
```
<!--# change the user around line34 according to user name of your hue hub.--> 
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_user.png)
<!--   2. Go to the directory of Philip Hue WuClass and change the URL address definition in a Philip Hue utility file according to your bridge.   
```bash
cd <path_of_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf/
vim udpdevice_philip_hue_*.py  
# change the user around line34 according to user name of your hue hub.
```
  ![](img/hue_user.png)-->

   3. 將Philip Hue的悟空裝置程式，按照第5.2節所述的步驟加入至悟空系統。   
   <!--3. Add udpdevice_philip_hue_\*.py  to WuKong according to [Section 5.2](../Ch5/Ch5_Device_Management.md).-->  
   
   4. 按照第5.3節所述的步驟建立一個Hue燈泡的應用程式，並設定初始值。   
   <!--4. Create the FBP and set the initial value-->
      一個基本的Hue燈泡應用程式如下圖所示，按鈕物件(Button)連接到Hue燈泡物件的開關屬性(on)，旋轉電位器(Slider)連接到Hue的紅色屬性(red)以調整紅色佔有的比例，另外，當點選Hue燈泡物件時，左方的欄位就會顯示出來，這個欄位是用來填寫其餘屬性的初始值。  
<!--      An example Philip Hue FBP can be seen as below. Button is used to turn on/off Philip Hue Bulb, and slider is used to adjust the intensity of the red color. The rest of properties can be filled in the left menu, which will pop up once the Philip Hue component is clicked.-->   
       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_fbp.png)
       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1_2.png)這兩個欄位填寫的是智慧橋接器的IP4位址，由於將應用程式部署到開發板的執行過程不支援字串型態(string datatype)，並且每個屬性的型態最長支援16位元，因此，我們必須將IP4位址轉換成短整數，並且需要用兩個屬性(ip_high, ip_low)來存取IP4位址，以下是計算如何轉換的範例：    
<!--       ![](img/no1_2.png)Currently, WuKong has not supported string type, so we have to convert ip address to integer first. Since the integer length in the WuKong is only 2 bytes, we have to use two properties ip_high and ip_low to indicate the ip address of Philip Hue bridge. Here is an example:-->  
       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_ip_example2.png)
       
       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)指數屬性(index)代表每個Hue燈泡的識別號，這個識別號可以從Hue提供的應用程式(app)來做確認，如下圖所示:  
       <!--![](img/no3.png)index is the id of each Philip Hue lamp, which shows on the Hue app as below.-->   

       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/hue_app2.png)

       ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)這個欄位代表三原色各自的比例，我們定義的範圍值是從0到254，也就是短整數能表示的範圍。  
       <!--![](img/no4.png)The range of rgb light intensity is from 0 to 254. The number filled in this blank will be set as the default value for the FBP component.-->         
   
   5. 按照第5.3節所述的步驟來部署Hue燈泡的應用程式
   <!--5.  Deploy this FBP according to [Section 5.3](../05-Web/Ch5_Application_Management.md)-->    
   
###實作網頁客戶端的悟空類別   
以下將說明悟空類別如何使用網頁客戶端來連線智慧橋接器，藉此控制燈泡的顏色與亮度。ㄧ旦了解Hue的悟空類別如何實作後，就能夠用相同的方式，跟其它有提供HTTP API的物聯網商品互通。由於Hue有一系列的產品，爲減少重覆的程式在各個Hue的悟空類別中，因此我們把部分共用的程式獨立成一個工具檔案，名叫philip_hue_utils.py，其中包含網頁客戶端，如下圖所示：      

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_1.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_2.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_3.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_4.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_utility_5.png)

附註: 關於如何透過Twisted使用網頁客戶端的詳細內容，請參考Twisted官方網頁 (http://twistedmatrix.com/documents/current/web/howto/client.html)   

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1.png)這個類別初始化的變數包含http_get_path與http_put_path，這兩組字串是根據Hue所提供的HTTP API而訂。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no2.png)put_command函式是用來傳送HTTP PUT請求(request)的信息，請求信息中的參數分別有，HTTP請求方法，請求的URI編碼，HTTP的標頭(header)，以及負責產生(produce)HTTP body的物件，接者，HTTP的代理物件(agent)會根據請求信息的參數來建立連線。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)get_gamma函式是透過傳送HTTP GET請求(request)的信息，來取得Hue燈泡的gamma值，由於Hue系列的產品對色彩範圍的支援並不相同，按照產品的區別可以分成三種範圍，然而，並非每個三原色的組合都會落在這些色彩範圍內，因此需要gamma值來做校正，才能夠將顯示的顏色接近原本的三原色組合。  
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)HTTP GET請求信息的回傳物件(response)能透過deliverBody顯示回傳物件的HTTP body。       
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no5.png)BeginningPrinter是專用在deliverBody函式的協議(Protocol)，當有HTTP GET的物件回傳時，dataReceived函式會接收到物件的HTTP body。      
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no6.png)在分析所收到的HTTP body之後，就能判斷gamma的值是多少。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no7.png)當HTTP body被接收完畢後，BeginningPrinter協議的connectionLost函式會緊接地被執行。   

接者，以下的悟空類別使用了工具檔案中的網頁客戶端來控制Hue燈泡。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_hue_wuclass_1.png)

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_hue_wuclass_2.png) 

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/7_2_philip_hue_wuclass_3.png)
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1.png)匯入Hue工具檔的網頁客戶端類別。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no2.png)從悟空屬性架構的屬性儲存區取得智慧橋接器的網路位址(ip),智慧橋接器的使用者名稱(username)以及Hue燈泡的識別號(index)之後，就能新增一個Hue的網頁客戶端物件。  
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)由於智慧橋接器接收到太頻繁的HTTP訪問訊息時，會導致延遲反應或者丟失訊息，於是，我們需要限定最短的訪問時間間隔，來確保智慧橋接器正常工作，以這個範例來說，最短間隔設定爲0.55秒。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)使用Hue的網頁客戶端物件來取得gamma值。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no5.png)使用gamma值來校正輸入的三原色值。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no6.png)這兩個command將會是HTTP body裏的訊息，於put_command函式傳給智慧橋接器。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no7.png)FileBodyProducer函式負責產生(produce)HTTP body的物件。  
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no8.png)使用Hue的網頁客戶端物件，透過put_command函式將HTTP請求的訊息傳給智慧橋接器。   