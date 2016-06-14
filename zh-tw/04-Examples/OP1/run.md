##4.1.4 執行程式

等待部署完成後，我們可以透過發送 HTTP 封包給 UIButton 的方式來改變其參數，並檢查音樂是否有撥放。因為悟空是使用事件觸發模型，所以如果數值沒有改變，便不會透過資料流傳送出去，所以我們必須交替傳送 0 與 1。

![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/04-Examples/Intel_Sound/34.png)


