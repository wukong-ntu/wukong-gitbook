## 3.2 設定Intel Galileo Gen2

安裝Intel Galileo Gen2成悟空裝置有**四個**步驟

**步驟一 準備Linux 映像檔:**  
準備可燒錄Linux 映像檔的microSD卡

**步驟二 開發版組裝:**   
組裝Intel Galileo 開發版

**步驟三 開發版設定:**  
設定Intel Galileo的密碼，以便我們可以用SSH指令連線到開發版

**步驟四 Python 工具安裝:**  
安裝執行悟空所必備的Python函式庫

**步驟五 下載悟空原始碼: **  
從Github上複製悟空的原始碼到Galileo開發版

---

* **步驟一 準備Linux 映像檔**

  Galileo Gen2不像Edison，沒有內建的快閃記憶體，所以我們需要準備可燒錄的microSD卡。

  請依照下列網頁的指示來燒錄microSD卡，當成開機的SD卡  
  [https://software.intel.com/en-us/get-started-galileo-linux-step1](https://software.intel.com/en-us/get-started-galileo-linux-step1)

---

* **步驟二 開發版組裝**

  根據Intel 官方物聯網的網頁，需要的硬體有

  * Intel Galileo Gen 2,
  * 一片SD卡\(&gt;2GB\),
  * 6 pin序列到Type A USB（例如：FTDI \#TTL-232R-3V3）
  * 一個7-15伏特並至少有1500毫安培的電壓器
  * \(可選擇\)WiFi網路卡（例如: Intel® Centrino® Wireless-N 135 or Intel® Centrino® Advanced –N 6205）

  準備好硬體後，請依照下列網頁的指示來組裝Intel Galileo Gen 2開發版：  
  [https://software.intel.com/en-us/get-started-galileo-linux-step2](https://software.intel.com/en-us/get-started-galileo-linux-step2)

  組裝完後，再依照下列網頁的指示來設定序列終端機，以便連線到開發版：  
  [https://software.intel.com/en-us/get-started-galileo-linux-step3](https://software.intel.com/en-us/get-started-galileo-linux-step3)

---

* **步驟三 開發版設定**

  如果在步驟二你有推薦的WiFi模組，依照下列網頁的指示來安裝WiFi網卡並設定WiFi   
  [https://software.intel.com/en-us/get-started-galileo-linux-step4](https://software.intel.com/en-us/get-started-galileo-linux-step4)

  假如沒有，依照下列網頁的指示來設定乙太網路連線，不需要序列終端機，可以使用Arduino IDE來和開發版溝通。  
  [https://software.intel.com/en-us/articles/intel-galileo-getting-started-ethernet](https://software.intel.com/en-us/articles/intel-galileo-getting-started-ethernet)

---

* **步驟四：Python 工具安裝**

  * 複製下方的指令到 `/etc/opkg/base-feeds.conf`

    ```
    src/gz all http://repo.opkg.net/edison/repo/all
    src/gz edison http://repo.opkg.net/edison/repo/edison
    src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32
    ```

  * 安裝 **pip** 和其他工具

    ```bash
    opkg update  
    opkg install python-pip
    opkg install sqlite3 
    opkg install git 
    pip install twisted 
    pip install python-cjson  
    pip install gevent  
    pip install netifaces
    ```

---

* **步驟五 下載悟空原始碼 \(已於2017.11.14更新\)**
  * 複製原始碼並下載到開發版上，放在你想要的資料夾路徑
    ```bash
    git clone -b release0.4 http://github.com/wukong-m2m/wukong-darjeeling.git
    ```



