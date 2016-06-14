##4.1.3 Build an Application FBP

現在我們準備好可以撰寫一個撥放音樂的程式了。

1.  點擊 **Application Management** 標籤。

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/19.png)

2.  點擊 **Create New** 按鈕並且輸入任意的程式名稱，我們的範例使用 "app1" 為例子。 <!--**(The dialog is in Chinese!!)**-->
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/20.png)

3.  點擊剛才建立的程式名稱，進入編輯畫面。 

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/21.png)  

4.  點擊 **WuClasses** 標籤，此時會顯示出所有可以在物件流編程時所使用的悟空類別。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/22.png)  

5.  捲動此列表直到找到名為 UIButton 的元件。點擊該元件即可選取，之後點擊下方的 **Add** 按鈕。重複此一步驟加入 Intel_Sound 元件。現在，編輯畫面中會出現兩個元件方塊。
    
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/23.png)  

6.  在兩個元件之間新增資料流。首先，點擊來源元件，該元件會被框起。之後，點擊被選取元件的目標參數，如範例中的 "click" 參數。最後，移動游標到目標元件，並點擊。
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/24.png)     

7.  此時，你可以確認所新增的資料流的來源與目標是否正確。如果有錯誤，可以在下拉式選單中做修正。
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/25.png)   

8.  (非必須) 依照下列圖片中的5個步驟輸入元件所在位置。即使位置為空白，主控台仍然會依照每個裝置的傳感器資料來挑選合適的裝置。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/30.png)

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/31.png)

9.  點擊 **Application** 標籤頁中的 **Save** 按鈕。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/27.png)

10.  點擊 **Map** 按鈕以為每個元件挑選適合的執行裝置。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/27-1.png)   

11.  等待配對完成後，配對結果會顯示在畫面上。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/28.png)   

12.  如果配對結果沒有錯誤，你可以點擊 **Deploy** 按鈕以開始部署程式。 

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/27-2.png)   

13.  您可以透過顯示在主控台上的訊息得知部署是否成功。

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/29.png)