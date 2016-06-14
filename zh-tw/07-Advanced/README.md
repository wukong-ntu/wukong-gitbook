#第7章: 建立與連接非悟空系統(Non-WuKong)的服務
<!--##Chapter 7: Building Connections to Non-WuKong Services-->    

在這章中，我們將透過一些範例來介紹如何建立與非悟空系統所提供的服務通訊，並在悟空類別中使用TCP封包(TCP socket)與網頁封包(Web socket)的通訊協定，有了這些通訊方式，我們就能將現有的資料流連接至外部的網頁服務以及市售的物聯網商品，以實現更有彈性與強大的分散式物聯網應用。
<!--In this chapter, we show some advanced examples on how to create an external data flow in WuClass using protocols such as TCP and Web sockets. With these types of non-WuKong data flow, we can connect WuKong FBP components to external Web-based services and commercial IoT products. Such connections allow users to implement flexible and powerful distributed IoT applications by integrating WuKong and Web.-->   

這章的悟空類別範例將會比上一章的複雜，有的悟空類別是使用該產品專有的API來取得服務，有的悟空類別則是用網頁存取的協定(web-access protocols)來取得服務，因此，爲了讓這些範例能被清楚地呈現，部分非必要的實作細節將被省略，介紹將着重於如何與各式的物聯網商品建立資料流。以下是各章節範例的簡述：       
<!--We show three examples that uses TCP server and Web connections respectively. The WuClass examples in this chapter are more complex than the ones in the previous chapter. 
Some of these WuClass examples use device-specific APIs to invoke their services. Other examples show how to use various web-access protocols in IoT applications.
To keep examples simple and easy to understand, some non-essential details may be omitted. The presentation is focused on how to create data flows with different types of products.-->    

* 使用TCP伺服器(TCP Server)連線的悟空類別   
<!--* [TCP Server WuClass  ](Ch7_For_RealSense_Camera.md)-->  
  在這個範例中，我們使用Python的Twisted函式庫來建立TCP連線，將悟空類別與Intel RealSense攝影機連接起來，如此一來，每當攝影機接受到新的輸入訊號後，都會將讀取到的值傳送給悟空類別，這樣的通訊方式也適合用於與Intel RealSense攝影機相仿的產品，如Kinect for Xbox One。  
<!--  In this example, we use Twisted library to establish a TCP connection between Intel RealSense Camera and FBP components so that whenever the camera captures a new gesture, it will send the reading to WuKong. This design can apply to other external sensing devices as well.-->   
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/twisted_tcp_server_application2.png)   

* 使用網頁客戶端(Web Client)連線的悟空類別  
<!--*  [Web Client WuClass ](Ch7_For_Philip_Hue_Series.md)-->     
  在這個範例中，我們使用Python的Twisted函式庫來傳送HTTP請求訊息(HTTP requests)給Philip Hue燈泡系列產品，當Hue的伺服器接受到訊息後，該伺服器就會依照訊息內容來調控Hue的燈光。    
<!--   In this example, we use the Twisted Web library to send HTTP requests to a Philip Hue hub. When the Hue's hub server receives messages, it will control Hue lights accordingly and return a response.-->   
   
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/twisted_web_client_application2.png)

* 使用網頁伺服器(Web Server)連線的悟空類別
<!--*  [Web Server WuClass](Ch7_For_Web_Application.md) -->    
  在這個範例中，我們使用Python的Twisted函式庫來實作一個網頁伺服器，用來接收瀏覽器發出的網址請求(URL requests)，只要我們在網頁伺服器中設計好HTTP APIs，並實作使用這個API的網頁客戶端(Web Client)，就能透過這個網頁伺服器，使外部的瀏覽器或應用程式控制悟空類別的輸出。  
<!--   In this example, we use the Twisted Web library to implement a Web server to receive URL requests from a browser application. The browser application provides a UI for users to control the output value of a UISlider component. In this way, we can provide HTTP APIs for developers to control WuKong applications. As long as they implement a Web client on their platform, they can use the HTTP API to make a connection to WuKong FBPs.-->     
   
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/07-Advanced/twisted_web_server_application2.png)
  


