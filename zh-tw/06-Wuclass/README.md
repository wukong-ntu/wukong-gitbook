#Chapter 6: 動手寫悟空類別元件

這章主要介紹如何在悟空系統中設計新的資料流編程(FBP)元件，讓開發者可以整合新的軟件服務與新的物聯網商品至悟空系統。以下將分成四個小節來說明：   

1. 第一節爲悟空屬性架構(WuKong Profile Framework, WKPF)，我們將解釋悟空系統的架構，以及這個架構如何執行在單一裝置上。  

2. 第二節將說明如何新增一個悟空類別(WuClass)的定義在函式庫中，因爲在開始實作元件之前，我們需要先定義元件的屬性和參數，並讓此元件出現在資料流編程介面的清單上。  

3. 接者，第三節將介紹實作類別元件的樣版，我們將按照所定義的屬性和參數來實作此類別元件，讓開發者可以在樣版中新增所需要的功能。  

4. 最後，我們將介紹現有的範例，這些範例整合了悟空系統與Grove感測器入門套件，這個套件在物聯網的開發板應用上十分普遍。

<!--#Chapter 6: Building New WuClasses -->   

<!--IoT applcation  developers  may create new WuClasses in WuKong to enrich their application design and to connect to new hardware. In this chapter, we show how to create new WuClasses in four sections:   

1. In the WuKong Profile Framework section, we explain the system architecture of the WuKong Profile Framework running on each device node.

2. [Adding a New WuClass Definition](Ch6_Add_a_New_Definition.md) shows how to add a new WuClass definition in the WuKong WuClass library.  Once a new WuClass is defined, a new entry will be created in the available WuClasses panel when restarting  Master's FBP editor.   

3. In the [Implementing a WuClass from Definition](Ch6_Implement_a_WuClass_by_Definition.md), we present the template of a WuKong device implementation.  
   
   Inside of the template, developers can create specific functionalities for the WuClasses defined earlier.
   
4. We show some examples on WuClasses built for Grove Sensor Modules. These modules are the most commonly used in many IoT applications.-->



