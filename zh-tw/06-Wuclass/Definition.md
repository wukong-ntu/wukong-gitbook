##6.2 新增一個悟空類別的定義至主控台  
<!--##6.2 Adding a New WuClass Definition in Master-->   
在開始實作悟空類別之前，我們需要先決定悟空類別的介面，包括具有哪些屬性，以及各屬性的參數，並將這個介面定義寫入函式庫`https://github.com/wukong-m2m/wukong-darjeeling/blob/release0.4/wukong/ComponentDefinitions/WuKongStandardLibrary.xml`，如同以下的步驟:
<!--Before we implement a WuClass, we need to specify the interface of the WuClass. The definition of WuClass is straightforward. All definitions can be found in the <*path_of_source_code*>wukong/ComponentDefinitions/WuKongStandardLibrary.xml. Writing a definition requires the following steps.-->  

* **定義悟空類別名稱(WuClass name)與各屬性名稱(property name)**      
下圖為比較4.2節的資料流編程範例與其悟空物件的定義，從中可觀察出兩者的名稱定義是一致的，此外，元件的屬性數量也與所定義的屬性數量相同。以按鈕(Button)來說，我們定義了兩個屬性名稱(current_value, refresh_rate)，因此，按鈕的資料流編程元件也就有兩個屬性;以燈光(Light Actuator)來說，我們只定義了一個屬性名稱(on_off)，因此，燈光的資料流編程元件只有ㄧ個屬性。   
<!--* **Define WuClass and property names**  

 Comparing our first FBP application to its WuClass definition as below, we can see that the name attribute of WuClass and property are identical to the names of the components in the FBP editor. In addition, the number of property is also defined by this xml file. For example, since there are two properties defined in the button WuClass, the component of the button in the FBP editor has two equivalent properties. In contrast, light actuator has only one property both in the WuClass definition and the FBP editor.-->    
  
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/name_definition.png)


* **定義悟空類別的識別號(id)**   
每一個悟空類別都需要給予一個獨特的識別號，ㄧ般我們習慣將運算用的悟空類別從號碼1開始給予;將感測用的悟空類別從號碼1001開始給予;將控制用的悟空類別從號碼2001開始給予。    
<!--* **Define identifier attribute**  

 Assign an unique identifier for a new WuClass definition. In our convention, the software WuClass ID starts from 1; the sensor WuClass ID starts from 1001; the actuator WuClass ID starts from 2001.-->

* **定義每個屬性的存取(access)**    
透過定義每個屬性的存取，我們可以決定該屬性為資料流上的來源或是目的，以按鈕的第一個屬性(current_value)來說，這個屬性的存取定義為唯讀(readonly)，代表我們預設這個屬性是作為資料流的來源;以燈光的第一個屬性(on_off)來說，這個屬性的存取定義為唯寫(writeonly)，代表我們預設這個屬性是作為資料流的目的;若屬性的存取定義為可讀可寫(readwrite)，則這個屬性可以同時作為某ㄧ個資料流的來源以及另一個資料流的目的。    
<!--* **Define access attribute**  

 The access attribute defines the source and the destination of data flow link. For example, the access of the current value for a button is read-only because it is a source of data for reading. The access of on_off for a light actuator is write-only because it is a destination of data for controlling LED. If the access is set as read-write, it can be both a source and a destination of a data flow link.-->   

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/access_definition.png)

* **定義每個屬性的資料型態(datatype)**   
每個屬性都需要定義資料型態，而目前可支援的資料型態為短整數型態(short integer, 16 bit),布林型態(boolean),列舉型態(enum)和刷新速度型態(refresh rate)。   

  短整數與布林型態的理解較爲直接，於是我們從列舉型態開始說明。使用列舉型態的目的是，讓資料流編程以及悟空類別的程式碼更容易被讀懂，此型態常被用在邏輯運算用的悟空類別，如臨界值比較(Threshold)和四則運算(Math)。      

  接者是刷新速度型態，此型態是爲了感測器的更新函式而設計的，用來定義更新函式的執行頻率，另外，按照一般對感測器的量測要求，刷新速度值的單位設爲毫秒(ms)，但由於屬性架構的資料型態有16位元的限制，若設定超過上限會被截除。   

  以按鈕感測器爲例，若按鈕的屬性定義中沒有刷新速度的資料型態的話，按鈕的更新函式將不會被屬性架構呼叫，按鈕的值也不會定期更新到屬性儲存區內。   

<!--* **Define datatype attribute**  

 Each property needs to have a datatype. Currently, the framework supports four datatypes: short (16 bit integer), boolean, enum, refresh rate. 

 The first two should be clear. Enum types can be used to make the code, both the FBP and the WuClass implementation more readable. Currently, this type is used primarily in logic components such as [threshold](https://github.com/wukong-m2m/wukong-darjeeling/blob/develop/src/lib/wkpf/c/common/native_wuclasses/wuclass_threshold_update.c) and [math operation](https://github.com/wukong-m2m/wukong-darjeeling/blob/develop/src/lib/wkpf/c/common/native_wuclasses/wuclass_math_update.c). 
 
 Since a sensor should take a new measurement periodically, the refresh rate datatype is designed to specify how often measurements will be taken. It is specified in **milliseconds** and is internally a 16 bit unsigned integer.  
 
  Therefore, since button is a sensor, when we define WuClass in the WuKongStandardLibrary.xml, we have to add refresh_rate property or else the value of button will not be propagated to the data link periodically.
-->    

* **定義每個屬性的初始值(default)**
每個屬性都需設定初始值，若沒有定義初始值，則預設值爲零。以按鈕爲例，若刷新速度的初始值設爲100，則按鈕的更新函式會每100毫秒執行一次，若未給予按鈕的刷新速度初始值，按鈕的刷新速度就會爲零，代表按鈕的更新函式將不會被執行。  
<!--* **Define default attribute**  

 A default value can be specified for properties. For example, the refresh rate of button is set as 100 milliseconds. This means the current value of button will be checked per 100 msec.-->    

* **定義悟空類別的進階參數(virtual and type)**   
這份文件將先跳過進階參數的描述，直到下一個版本再做詳細說明。目前請先參考最相近的悟空類別來給予定義，舉例來說，若要新增的悟空類別屬於感測器，則可以參考按鈕(Button)的進階參數定義;若要新增的悟空類別屬於控制物件，則可以參考燈光(Light Actuator)的進階參數定義。
<!--* **Define virtual and type attribute** 

 This is an advanced attribute to be covered in future documents to define whether the component can be created dynamically and can be in software implementation. For now, it's sufficient to know that for most cases, the virtual attribute is set as false, and the type attribute is set as hard.-->      
 
* **刪除暫存檔並重啓主控臺**   
當新增悟空類別至函式庫(WuKongStandardLibrary.xml)後，我們需要先把之前的暫存檔清除，確保主控臺會產生新的悟空類別清單，接者才重啓主控臺，以下爲執行步驟：   
```bash    
cd <path_of_source_code>/wukong-darjeeling/wukong/master/static/js/    
rm __comp__* 
# 接者，清除Chrome瀏覽器關於http://localhost:5000的歷史資料   
# 重啓主控臺  
```

  完成以上步驟並重啓主控臺後，在資料流編輯介面的左側悟空類別清單上，就可以看到新增的悟空類別，如同下圖的按鈕與燈光。   
  
  ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/add_new_wuclass_definition.png)