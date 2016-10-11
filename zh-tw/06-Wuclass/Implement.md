## 6.3 實作悟空類別

在這一章節中，我們會搭配[4.2節](../04-Examples/LED.md)的資料流編程範例來介紹如何實作悟空類別，實作出來的悟空類別可以同時用於Edison, Galileo和Raspberry Pi，使用的方式如同[5.2節](../05-Web/Device.md)所述。  

#### **悟空裝置的Python樣版**   
以下爲悟空裝置的樣版，從樣版中可看到，悟空裝置會加入悟空類別(addClass)，並產生悟空物件(addObject)。目前所有的悟空裝置程式都存放在`https://github.com/wukong-m2m/wukong-darjeeling/tree/release0.4/wukong/gateway/udpwkpf`

* ###**更新IoT開發板上的WuKongStandardLibrary.xml**   
  請留意，若已按照前一小節所述，新定義了一個悟空類別在master端的WuKongStandardLibrary.xml的話，記得把這份檔案也複製到IoT開發板的相同位置，指令如下。      
```bash
#Copy from master to Intel Edison:
cd <path_of_source_code>wukong/ComponentDefinitions/ 
scp WuKongStandardLibrary.xml root@<IP address of Intel Edison>:<path_of_source_code_on_Intel_Edison>wukong/ComponentDefinitions/  
#Copy from master to Raspberry Pi:
cd <path_of_source_code>wukong/ComponentDefinitions/ 
scp WuKongStandardLibrary.xml pi@<IP address of Raspberry Pi>:<path_of_source_code_on_Raspberry_Pi>wukong/ComponentDefinitions/  
```

```python
  from twisted.internet import reactor
  from udpwkpf import WuClass, Device
  import sys
  
  if __name__ == "__main__":
      class XXX(WuClass):
          def __init__(self):
              WuClass.__init__(self)
              self.loadClass('XXX')

          def update(self,obj,pID=None,val=None):
              pass
              
      class MyDevice(Device):
          def __init__(self,addr,localaddr):
              Device.__init__(self,addr,localaddr)

          def init(self):
              cls = XXX()
              self.addClass(cls,0)
              self.addObject(cls.ID)

      d = MyDevice(sys.argv[1],sys.argv[2])
      reactor.run()
```

####**悟空裝置範例程式：按鈕和燈光**
此範例程式是根據以上的樣版所寫成，在此裝置樣版中實作了兩個悟空類別，一個是第10行的按鈕(Button)，另一個是第25行的燈光(Light_Actuator)，有了這兩個悟空類別的實作，我們就可以照者4.2節的步驟來部署應用程式，因此，在往下看程式之前，建議可以先照者4.2節所述的步驟操作一遍，將有助於對此程式的理解。接者，每個悟空類別都有初始函式(init)與更新函式(update)，初始函式是用來設定各變數,狀態與硬體參數的起始值，而更新函式則是用來被屬性架構重覆地呼叫執行。最後，當悟空裝置範例程式被執行後，這兩個悟空類別將會被加入(addClass)悟空裝置中，並用來產生(addObject)悟空物件。   
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/python_wuclass_blink_led_1_new.png)
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/python_wuclass_blink_led_2_new.png)

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/python_wuclass_blink_led_3_new.png)

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no1.png)爲了透過GPIO控制按鈕和燈光，我們需要在悟空裝置最前面匯入(import)物聯網開發板的GPIO函式庫，而且，爲了盡可能讓同一個悟空裝置程式能執行在不同的物聯網開發板，我們新增了這個介面(udpdevice_io_interface.py)來決定如何使用三個不同的GPIO函式庫，下一個章節會繼續說明這個GPIO介面。  
<!-- ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no1.png)Since we control button and LED through gpio, we need to import the gpio library for the IoT board. To make this template work with various IoT boards, we create an interface to define how to use gpio. We will see more about this interface in the next section.  -->   

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no2.png)這個函式的輸入參數必須是悟空類別的名稱，並且，此名稱要與WuKongStandardLibrary.xml所定義的名稱相同，當這個函式取得悟空類別名稱後，就會分析WuKongStandardLibrary.xml所定義的內容，截取這個悟空類別的每個參數。    
<!-- ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no2.png)The input argument of self.loadClass function must be a WuClass name defined in the WuKongStandardLibrary.xml. With WuClass name, this function will parse all its attributes from WuKongStandardLibrary.xml file.-->             

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no3.png)使用第1點所提的GPIO介面來設定哪個GPIO腳位會被用到，並設定該腳位是數位(digital)還是類比(analog)，以及設定是輸入(input)或輸出(output)。
<!-- ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no3.png)Use the function of udpwkpf_io_interface.py to specify which gpio pin will be used. We also specify whether this pin is digital or analog, and whether its direction is input or output.-->  

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no4.png)由於在6.2節中，按鈕感測器有定義刷新速度(refresh rate)屬性，所以更新函式(update)會定期被執行並透過GPIO讀取其感測到的值。
<!--  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no4.png)Since button is a sensor, the update function should be run periodically to read sensing data from gpio. For this reason, we have defined a property with refresh_rate datatype for the button WuClass, so the update function of the button WuClass will be called by WKPF regularly.-->       

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no5.png)setProperty函式是用來將某屬性的值寫入屬性架構的屬性儲存區，當屬性架構監測到此屬性的值改變後，就會按照資料流表單來傳遞值。setProperty函式的第一個參數是屬性辨別號(property ID, pID)，在第20行中，pID等於零表示按鈕的第1個屬性的值將被寫入屬性儲存區，若我們對照WuKongStandardLibrary.xml，可知道按鈕的第1個屬性是current_value，也就是說，按鈕的感測數值會被寫入屬性儲存區。   
<!--  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no5.png)The **setProperty** function of button will send its value to WKPF which then propagates the value according to the data link of FBP. The first parameter of setProperty function is pID. In this example, pID=0 indicates the first property of button, which is current_value (you can confirm with the WuKongStandardLibrary.xml). That is, the current_value is going to be propagated.-->   

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no6.png)由於燈光悟空類別沒有定義刷新速度(refresh rate)，所以燈光的更新函式只會在其屬性的值改變時被呼叫。以4.2節的範例來說，當按鈕被按下去時，屬性架構會知道按鈕的第1個屬性的值已改變，於是就照着資料流清單把值傳遞給燈光屬性儲存區，並且呼叫燈光的更新函式，當函式被執行時，就會照者讀取到的值來開關燈光。在屬性架構呼叫更新函式時，同時也會傳遞改變的**obj**(悟空物件),**pID**(屬性識別號)和**value**(值)給更新函式做運用。   
<!--  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no6.png)This update function will be called whenever there is a new data propagated to the light actuator. And because we doesn't define a property with refresh_rate for the light actuator, its update function will only run responsively. For example, in the FBP of Ch4.2, when button is pressed, its value will propagate through data link to light actuator. And then, the update function of light actuator will be called by WKPF. WKPF also passes three parameters including **obj**(WuObject of light actuator), **pID**(which property of WuObject going to be updated), and **value**.  After being called, the update function will turn on or off the light actutator responsively.-->         

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no7.png)這個函式爲用來加入悟空類別到悟空裝置，在這個範例程式中，按鈕和燈光均加入到同一個悟空裝置程式，所以會共同使用一個屬性架構。關於此函式的第2個輸入參數，是用來表示這個悟空類別可否自行產生悟空物件，零代表此悟空類別不能自行產生悟空物件，因此需要用下一行的函式(addObject)來產生悟空物件。在7.3節時，我們將會使用到能自行產生悟空物件的悟空類別，屆時就不需要用addObject來產生悟空物件。   
<!--  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no7.png)Add WuClass to the WuClass list of the WuKong device so that this WuClass will share the same WKPF as other WuClasses on a node. About the second parameter of addClass function, this value indicates whether this WuClass can be used to create objects. "0" means this WuClass can't create objects. That's why we use addObject function in the next line to create an object(self.obj_button) for the device. In the Ch7.3, we will use a WuClass which can create objects.-->    

  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no8.png)由於屬性架構的實作是用Python的Twisted函式庫，所以最後記得要加這行程式，否則按鈕的值不會被定期更新。   
<!--  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/no8.png)Don't forget to add **reactor.run()** or else the value of button will neither be refreshed periodically nor be propagated to light actuator through data link.-->   

####**要點**   
這一章節的最後，我們歸納出實作悟空類別的幾個要點：    
  * 首先是新增並仿照悟空裝置樣版到<*path_of_source_code*>/wukong/gateway/udpwkpf/udpdevice_XXX.py   
  * 若是要新增感測器(sensor)，請參考按鈕的悟空類別寫法;若是要新增控制器(acutator)，請參考燈光的悟空類別寫法。   
  * 最後加入悟空類別到裝置上(addClass)，並在裝置上產生悟空物件(addObject)。  

<!--
###**Summary**  
In this section, we show the steps to implement the Python code for an IoT device:   
  * Copy the template to a new file as  <*path_of_source_code*>/wukong/gateway/udpwkpf/udpdevice_XXX.py  
  * Write a WuClass for each of the sensors according to the pattern of Button, or write a WuClass for actuator according to the pattern of Light_Actuator.  
  * Add WuClass to MyDevice and use this WuClass to create an object on the device.-->  
