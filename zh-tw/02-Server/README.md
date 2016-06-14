#第2章: 設定伺服器環境

這份章節呈現出在Linux-based的電腦上安裝發展悟空環境所需要的指令，
這些指令在**Ubuntu 14.04 LTS**的電腦上執行，我們計畫在未來提供OSX和Windows的安裝指南。
在那之前，對於PC使用者可能的選項就是安裝虛擬機器並執行Ubuntu。

執行悟空需要四個工具，Git可以取得悟空專案的原始碼，Java執行主控台(Master)軟體，
Gradle可以建立專案，而Python是用來實作悟空屬性架構(Wukong Profile Framework)，如果你的伺服器已經安裝上述的軟體，你可以跳過任何一步。

* **安裝 Git**

  ```bash
  sudo apt-get install git-core
  ```
  
* **安裝 Java**

  ```bash
  sudo add-apt-repository ppa:webupd8team/java
  sudo apt-get update && sudo apt-get install oracle-java7-installer
  ```
  
* **安裝 Gradle**  

  下載Gradle2.4 [（連結）](https://services.gradle.org/distributions/gradle-2.4-all.zip)
  並且解壓縮到一個資料夾，例如：~/gradle-2.4，將Gradle的資料夾路徑加到環境變數，如下表示
  ```bash  
  vim ~/.bashrc  
  ```
  加環境變數

  ```bash
  export PATH=$PATH:~/gradle-2.4/bin
  ``` 
  
  添加環境變數在（bash startup）檔案中的最後一行，並使用source的指令去執行腳本（script）

  ```bash  
  source ~/.bashrc
  ``` 

* **安裝 Python 工具** 

  ```bash  
  sudo apt-get install libevent-dev  
  sudo apt-get install python-dev  
  sudo apt-get install python-setuptools  
  sudo apt-get install libxml2-dev libxslt1-dev zlib1g-dev  
  sudo apt-get install python-pip 
  sudo pip install configobj simplejson gevent greenlet tornado jinja2 pyserial \
  lxml  
  sudo pip install netifaces  
  sudo pip install python-cjson  
  sudo apt-get install python-pyaudio  
  ```

在下一章節，我們會呈現如何安裝物聯網裝置(例如Intel Edison,Galileo,樹莓派(Raspberry Pi2))，來實作出可以感測和控制環境裝置的應用程式(Application)。如果目前沒有上述的物聯網裝置，只要使用個人電腦和這章節所介紹的工具套件，就可以發展悟空的物聯網應用程式，範例將在[4.1節](../04-Examples/Music.md)展示。

