## 3.1 設定Intel Edison

安裝Intel edison成悟空裝置有**四個**主要步驟

**步驟一 開發版組裝:**  
在Arduino擴充開發版上組裝Intel edison模組

**步驟二 開發版設定:**  
設定Intel edison的密碼，以便我們可以用SSH指令連線到開發版

**步驟三 韌體更新:**  
獲得相容性的Yocto 映像檔，目前版本為159.devkit，可以支援更大的root 分割容量 以及更好的Python工具

**步驟四 Python 工具安裝:**  
安裝執行悟空所必備的Python函式庫

**步驟五 下載悟空原始碼: **  
從Github上複製悟空的原始碼到Edison開發版

---

* **步驟一 : 開發版組裝**

  Intel提供了兩種擴充開發版給Intel Edison所使用，分別為:Arduino 擴充開發版和mini breakout board，  
  在此章節中，我們使用Arduino擴充開發版，不須焊接就可以很方便的連接組合包中的感應器。

  請依照下列網頁的指示來組裝Intel Edison 開發版：  
  [https://software.intel.com/en-us/assembling-intel-edison-board-with-arduino-expansion-board](https://software.intel.com/en-us/assembling-intel-edison-board-with-arduino-expansion-board)

  組裝完後，再依照下列網頁的指示來設定序列終端機，以便連線到開發版：  
  [https://software.intel.com/en-us/setting-up-serial-terminal-intel-edison-board](https://software.intel.com/en-us/setting-up-serial-terminal-intel-edison-board)

---

* **步驟二 : 開發版設定**

  * 在終端機上輸入下方的指令去設定開發版

    ```bash
    configure_edison --setup
    ```

  * 終端機出現提示時，你必須輸入密碼，以便我們可以透過**SSH**的指令連線到開發版

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/03-Board/fig3-1-0.png)

  * 終端機出現提示時，你可以替開發版取名字；或者空白，則 **"root"** 將會成為預設的名字

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/03-Board/fig3-1-1.png)

  * 下一步是設定WiFi，輸入"Y"來設定WiFi，而開發版會開始掃描WiFi熱點，一旦開發版完成掃描，  
    可選擇一個WiFi熱點，並輸入密碼。下方圖片為設定WiFi的例子。

    ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/03-Board/fig3-1-2.png)

  * 假如你需要連別的WiFi熱點，你可以使用下方的指令來重新設定WiFi。

    ```bash
    configure_edison --wifi
    ```

---

* **步驟三 : 韌體更新**

  請確保開發版的韌體為最新版本，你可以使用下方的指令來確認版本:

  ```bash
  configure_edison --version
  ```

  如果螢幕秀出`159.devkit`，則此版本可兼容，反之，請依照下列網頁來更新韌體:  
  [https://software.intel.com/en-us/iot/hardware/edison/downloads](https://software.intel.com/en-us/iot/hardware/edison/downloads)

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



