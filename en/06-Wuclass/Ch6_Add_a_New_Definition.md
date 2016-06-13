##6.2 Adding a New WuClass Definition in Master

Before we implement a WuClass, we need to specify the interface of the WuClass. The definition of WuClass is straightforward. All definitions can be found in the <*path_of_source_code*>wukong/ComponentDefinitions/WuKongStandardLibrary.xml. Writing a definition requires the following steps.  

* **Define WuClass and property names**  

 Comparing our first FBP application to its WuClass definition as below, we can see that the name attribute of WuClass and property are identical to the names of the components in the FBP editor. In addition, the number of property is also defined by this xml file. For example, since there are two properties defined in the button WuClass, the component of the button in the FBP editor has two equivalent properties. In contrast, light actuator has only one property both in the WuClass definition and the FBP editor.
  
 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/name_definition.png)

* **Define identifier attribute**  

 Assign an unique identifier for a new WuClass definition. In our convention, the software WuClass ID starts from 1; the sensor WuClass ID starts from 1001; the actuator WuClass ID starts from 2001.

* **Define access attribute**  

 The access attribute defines the source and the destination of data flow link. For example, the access of the current value for a button is read-only because it is a source of data for reading. The access of on_off for a light actuator is write-only because it is a destination of data for controlling LED. If the access is set as read-write, it can be both a source and a destination of a data flow link.

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/access_definition.png)



* **Define datatype attribute**  

 Each property needs to have a datatype. Currently, the framework supports four datatypes: short (16 bit integer), boolean, enum, refresh rate. 

 The first two should be clear. Enum types can be used to make the code, both the FBP and the WuClass implementation more readable. Currently, this type is used primarily in logic components such as [threshold](https://github.com/wukong-m2m/wukong-darjeeling/blob/develop/src/lib/wkpf/c/common/native_wuclasses/wuclass_threshold_update.c) and [math operation](https://github.com/wukong-m2m/wukong-darjeeling/blob/develop/src/lib/wkpf/c/common/native_wuclasses/wuclass_math_update.c). 
 
 Since a sensor should take a new measurement periodically, the refresh rate datatype is designed to specify how often measurements will be taken. It is specified in **milliseconds** and is internally a 16 bit unsigned integer.  
 
  Therefore, since button is a sensor, when we define WuClass in the WuKongStandardLibrary.xml, we have to add refresh_rate property or else the value of button will not be propagated to the data link periodically.  

* **Define default attribute**  

 A default value can be specified for properties. For example, the refresh rate of button is set as 100 milliseconds. This means the current value of button will be checked per 100 msec.  

* **Define virtual and type attribute** 

 This is an advanced attribute to be covered in future documents to define whether the component can be created dynamically and can be in software implementation. For now, it's sufficient to know that for most cases, the virtual attribute is set as false, and the type attribute is set as hard.  
 
* **Delete cache files and restart master_server** 

	After a new WuClass is defined in the WuKongStandardLibrary.xml, you should restart  Master to read the new definition. Before that, you should remove the cache file to make sure Master will create a new list of WuClasses.

	```bash
	cd <path_of_source_code>/wukong-darjeeling/wukong/master/static/js/    
	rm __comp__*  
	# next, clean browser history of http://localhost:5000  
	# restart master server
	```    
 
 After following the above steps, you will see a new WuClass in the WuClasses list of the FBP editor just like the button and light actuator WuClasses shown below.

 ![](https://raw.githubusercontent.com/wukong-ntu/wukong-gitbook-figures/master/figures/06-Wuclass/add_new_wuclass_definition.png)