##7.1 TCP伺服器連線  
<!--###7.1  TCP Server Connection-->  

在這個章節中，我們介紹如何將Intel RealSense SDK與悟空資料流編程的物件透過TCP互相連線，同時也介紹如何在悟空資料流編程的介面上，部署使用RealSense攝影機的物聯網應用程式。 
<!--In this section, we explain how to create a TCP connection between the Intel RealSense SDK and the WuKong FBP components. We also show an FBP application on how to adopt a RealSense camera in an IoT application.-->     

* ###將Intel RealSense攝影機與悟空類別互相連線
<!--* ###Connecting Intel RealSense Camera with WuKong-->   
  1.  Intel RealSense攝影機提供了許多專屬的功能，如臉部辨識,手勢辨識,聲音分析與擴增實境，在這個章節中，我們只使用手勢辨識的功能，目的是展示如何在悟空類別內新增TCP客戶端(TCP Client)，而Intel RealSense攝影機的手勢辨識範例可以直接從它的SDK(`https://software.intel.com/en-us/realsense/home`)取得，範例的檔案資料夾位置在Intel/RSSDK/sample/FF_HandsViewer/.
<!--  1.  The Intel RealSense camera provide many features for facial analysis, hand and finger tracking, sound processing, and augmented reality. In this example, we use only the feature of finger tracking to show how to add a TCP client in WuKong FBPs. Since RealSense has provided its SDK on the website https://software.intel.com/en-us/realsense/home, we simply use its HandsViewer code. The example is under the Intel folder, Intel/RSSDK/sample/FF_HandsViewer/.-->   
 
  2.  爲了要將RealSense攝影機捕捉的手勢訊號傳給悟空物件，我們在原有的手勢辨識範例中加了一些檔案與函式，用來定義如何傳送訊號，這份改版的程式可以從以下連結(`https://drive.google.com/open?id=0B31WAUDq3a3uZWZzb21iR0NwMDQ`)取得，若要使用這份下載的程式，需要取代掉這個資料夾下(Intel/RSSDK/sample/FF_HandsViewer/src)的原有檔案，接者用Microsoft Visual Studio來打開名稱爲FF_HandsViewer_vs201*的SLN檔。當RealSense攝影機連接至USB3.0的插槽後，便可執行SLN檔，執行後跳出的畫面如下，代表攝影機已在接收手勢訊號並做辨識分析。      
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/realsense.png)
  在HandsViewer.cpp的檔案中，新增TCP客戶端的連線是發生在第535行，接者將這個TCP檔案描述子(socket file descriptor)傳送給DisplayGesture函式，這個函式會持續地辨認手勢，並將事前定義好的手勢的值用SendMessage傳送給悟空類別上的TCP伺服器，如此一來，收到訊號的悟空類別就可進一步做反應。   
<!-- In the HandsViewer.cpp file, a socket client is created on line 535 and passed to the DisplayGesture function which is responsible to identify gestures. After getting the gesture, the SendMessage function will send different pre-defined number to there TCP server. In that way, WuKong can respond to each gesture accordingly.-->  

  3.  而這個悟空類別的實作是在udpdevice_mux_gesture_control.py，如同下圖中的RealSenseProtocol類別所示，這個類別主要的功能在於分析與反應TCP客戶端傳回來的資料。  
<!-- In WuKong, the TCP server is implemented in the udpdevice_mux_gesture_control.py, under the  RealSenseProtocol class as shown below. This class implements the user-defined network protocol parsing and handling for TCP servers, as an example of explaining how we can support different protocols in WuKong.-->        
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/realsense_protocol2.png)
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no1.png) 這個類別繼承了basic.LineReceiver，這是Twisted函式庫內用來通訊的一種協定，它有許多種接收TCP連線訊號的模式，其中一種是lineReceived模式，用lineReceived函式來接收一整行(lines)的數據。詳細的資訊可以參考以下網頁： `https://twistedmatrix.com/documents/9.0.0/api/twisted.protocols.basic.LineReceiver.html`
<!-- ![](img/no1.png) This class inherits basic.LineReceiver which is a protocol that receives lines and/or raw data, depending on the mode. For further information, please refer to https://twistedmatrix.com/documents/9.0.0/api/twisted.protocols.basic.LineReceiver.html-->   
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no2.png) 在lineReceived模式中，每接收到一筆數據，lineReceived函式就會被呼叫(callback)，換句話說，lineReceived會接收到其它TCP客戶端的封包，也就是手勢辨識範例(HandsViewer.cpp)透過SendMessag函式所傳遞的。
<!-- ![](img/no2.png) In the lineReceived mode, each line received becomes a callback to lineReceived. In other words, data is the packet received from other TCP client. So data is a message sent by the SendMessage function in the HandsViewer.cpp file.-->     
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no3.png)一旦接收到數據，便會按照程式的設計被分析與處理。在這個悟空類別中，我們定義了模式(mode)與手勢(gesture)兩種屬性，手勢的值是在RealSense範例中所事先定義好的數字，而模式屬性的設計目的是，爲了可以讓同一組手勢運用在不同的場景，所以模式屬性的值就是用來做場景的切換，由於在RealSense範例中，不能捕捉比數字的手勢，於是我們選擇用它內建的輕拍(Tap)手勢來表示要更換模式，並且，輕拍手勢很像在按虛擬的按鈕，手勢屬性的值也與按鈕一樣是布林值(True oe False)。  
<!-- ![](img/no3.png) Once received a message, the code can split and parse the message according to the design. In this WuClass, we define the mode and gesture properties. The meaning of gesture is straightforward, but the meaning of mode requires some explanation. Since RealSense doesn't provide the sample code to identify the number gesture, we cannot change mode simply by using the number gesture. One alternative is using True or False to indicate whether a user wants to change mode or not. The changing mode property corresponds to the "tap" gesture. When a user posts a tap gesture (similar to pressing a virtual button), the mode property will propagate a signal to next component.-->
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no4.png)每次當我們接收到一筆新數據後，都要用這兩行程式將模式屬性的值設爲False，將手勢屬性的值設爲零，因爲如同第六章所述的屬性架構，只有當屬性的值被屬性架構發現有改變後，這個值才會按照資料流的來源與目的傳遞，若沒有重新設定這兩個屬性的值，輕拍的手勢將無法更換場景，因爲輕拍手勢的值每次都相同，所以不會被屬性架構傳遞。   
<!-- ![](img/no4.png) Every time we receive new data, we have to reset mode and gesture before calling the setProperty function because WuKong adopts the even-driven model. If we don't reset the property, the same continual mode and gesture signal will be propagated only once.-->
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no5.png)每次模式屬性的值都會被儲存，並用於跟下一回新的值做比較。
<!-- ![](img/no5.png) The previous state of mode property will be stored and compared to the new mode property, or otherwise we will count mode change incorrectly.-->    
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/no6.png)最後，手勢屬性的值透過這行程式傳遞至資料流的目的。  
<!-- ![](img/no6.png) Finally, the gesture value is propagated to the next component.-->      
 
* ###部署使用RealSense攝影機的物聯網應用程式 
<!--* ###FBP Using Intel RealSense Camera-->  
這張圖可以用來說明，如何透過悟空系統部署使用RealSense攝影機的物聯網應用程式。如同上述，圖中的RealSense元件有模式與手勢的屬性，這兩個屬性的值會連接到一個交換器(GestureSwitch)，此交換器會使用模式屬性的值，來決定要更新哪一個場景的資料流，分別有影片播放(GestureToVideoControl),視訊通話(GestureToHangoutControl)與燈光明暗控制(GestureToBrightnessControl)，再由該場景元件根據手勢屬性的值來執行應用服務。   
![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/FBP_RealSense.png)

