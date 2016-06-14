##4.2.3 撰寫物件流程式


現在，我們要撰寫一個控制 LED 燈的程式，並且部署到物聯網開發版上

1.  點擊 **Application Management** 標籤。   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/29.png)

2.  點擊 **Create New** 按鈕並且輸入任意的程式名稱。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/30.png)

3.  點擊剛才建立的程式名稱，進入編輯畫面。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/31.png)

4.  點擊 **WuClasses** 標籤。  

   ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/32.png)

5.  捲動此列表直到找到名為 **Button** 的元件。點擊該元件即可選取，之後點擊下方的 **Add** 按鈕。現在，編輯畫面中會出現一個 **Button** 元件方塊。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/33.png)

6.   重複上一步驟加入 **Light_Actuator** 元件。因為新加進來的元件可能會疊在上一個元件上，請把他們拉開。
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/34.png)      

7.  在兩個元件之間新增資料流。首先，點擊來源元件，該元件會被框起。之後，點擊被選取元件的目標參數。最後，移動游標到目標元件，並點擊。
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/35.png)

8.  此時，你可以確認所新增的資料流的來源與目標是否正確。如果有錯誤，可以在下拉式選單中做修正。   

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/36.png)

9.  點擊 **Application** 標籤頁中的 **Save** 按鈕。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/38.png)

10.  然後我們就可以開始部屬我們的程式。首先，點擊 **Map** 按鈕，開始配對程序。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/39.png)

11. 之後在畫面上就會顯示配對的結果。如果配對成功了，每一個物件流程式上的元件都會對應到一個裝置 ID 和連接埠(port)。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/40.png)

12.  點擊 Deploy 按鈕以開始部署程式。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/41.png)

13.  您可以透過顯示在主控台上的訊息得知部署是否成功。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/LED_Control_of_Ch5/42.png)




