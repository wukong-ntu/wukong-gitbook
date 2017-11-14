## 3.3 設定Raspberry Pi Board

安裝Raspberry Pi成悟空裝置有**四個**主要步驟

**步驟一 準備 Raspbian Linux 映像檔:**  
準備可燒錄Raspbian Linux 映像檔的microSD卡

**步驟二 開發版組裝:**  
組裝Raspberry Pi board及相關的配件

**步驟三 開發版設定:**  
設定Raspberry Pi的密碼

**步驟四 Python 工具安裝:**  
安裝執行悟空所必備的Python函式庫

**步驟五 下載悟空原始碼: **  
從Github上複製悟空的原始碼到Raspberry Pi Board

---

* **步驟一 準備Raspbian Linux映像檔**

  請依照下列網頁的指示來安裝NOOBS:  
  [https://www.raspberrypi.org/help/noobs-setup/](https://www.raspberrypi.org/help/noobs-setup/)

  我們也推薦到官方網站下載映像檔，請依照下列網頁的指示來燒錄映像檔到SD卡，變成可開機的SD卡。  
  [https://www.raspberrypi.org/documentation/installation/installing-images/README.md](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)

  預設放入映像檔的SD卡容量為4GB，如果你需要更多的空間，請依照官方網頁的解決方式。  
  [https://www.raspberrypi.org/documentation/configuration/raspi-config.md](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)

---

* **Step 2. 開發版組裝**

  需要的硬體包含：

  * Raspberry Pi Board
  * 一片 SD 卡 \(&gt;4GB\)
  * HDMI cable
  * 一個7-15伏特並至少有1500毫安培的電壓器
  * （可選擇） USB WiFi 網卡
  * （可許澤） Grove Pi 擴充開發版

  你可以觀看下列影片來組裝Raspberry Pi  
  [https://www.youtube.com/watch?v=JiTNdwD1fS0](https://www.youtube.com/watch?v=JiTNdwD1fS0)

---

* **Step 3. 開發版設定**  
  一旦RPi啟動後，你可以使用圖形化介面或透過SSH指令登入，帳號為`pi`，密碼為`raspberry`

  * 在終端機輸入指令來改變鍵盤佈局

    ```
    sudo nano /etc/default/keyboard
    ```

    在檔案中找到下列這行：

    ```
    XKBLAYOUT=”gb”
    ```

    將gb改成你所在的國家代碼，為兩個字母，例如 "us"。輸入Ctrl+X 儲存並關閉檔案

    假如你不知道你的國家代碼，可以到下列的維基百科網頁搜尋目前的國家代碼（使用第二行:alpha-2 的代碼）  
    [Here](https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes)

  * 變更Raspbian的更新套件來源

    ```
    sudo nano /etc/apt/sources.list
    ```

    請從下方的官方網站上，  
    [https://www.raspbian.org/RaspbianMirrors](https://www.raspbian.org/RaspbianMirrors)  
    找到最近的伺服器連結，去取代檔案中的下方連結

    ```
    http://mirrordirector.raspbian.org/raspbian
    ```

    並使用下列指令進行更新。

    ```
    deb http://mirrordirector.raspbian.org/raspbian jessie ...
    ```

---

* **步驟四：Python 工具安裝**

  * Python工具安裝: 安裝`pip`和其他工具

    ```
    sudo apt-get update  
    sudo apt-get install python-twisted python-cjson python-gevent  
    sudo apt-get install sqlite3 python-netifaces
    ```

  * \(可選\)在終端機輸入指令，安裝grovepi函式庫來啟動I2C對Grove pi擴充開發版的介面

    ```
    sudo apt-get install python-smbus i2c-tools
    sudo raspi-config
    ```

    一旦表單出現，使用方向鍵和Enter鍵選擇**Advanced Options**，以及**I2C**，選擇**YES**去啟動I2C介面，以及**YES**去啟動預設模組，最後重開RPi

    ```
    sudo reboot
    ```

    重開後，如果你有Pi Model A, B+ 或 2 B\(記憶體：512 MB\)，在終端機上使用下列指令去檢查I2C是否有開啟

    ```
    sudo i2cdetect -y 1
    ```

    如果為Pi 1 B \(記憶體：256MB\), 則執行下列指令

    ```
    sudo i2cdetect -y 0
    ```

    在表格中應該會顯示一些位址如20,40 或70

    ```
    git clone https://github.com/DexterInd/GrovePi.git  
    cd <source code>/GrovePi/Software/Python  
    sudo python setup.py install
    ```

---

* **步驟五 下載悟空原始碼 \(已於2017.11.14更新\)**
  * 複製原始碼並下載到開發版上，放在你想要的資料夾路徑。
    ```bash
    git clone -b release0.4 https://github.com/wukong-m2m/wukong-darjeeling.git
    ```



