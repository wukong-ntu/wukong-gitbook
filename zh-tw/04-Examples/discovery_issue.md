#4.1.5. Discovery Issue

One common issue for **node discovery**  happens when computers or IoT devices are moved to another network environment. Although they obtain new IP addresses,  Master, gateways, or devices may still use old cached files that have old IP addresses.    

To solve the problem, whenever the WuKong network environment is changed,  you must follow the instructions below to reset the WuKong system to its default settings. Moreover, even if some nodes are in the same network but still cannot be discovered, use the instructions to reset the system as well. 
<!--If you find this solution still does not help, please contact us about your specific problems. -->

```bash    
cd <path_source_code>/wukong-darjeeling/wukong/master  
rm *.pyc *.json change*  

# Go to the WuKong Master directory  
# Remove the compiled Python files, JSON files, and also the changeset.  
# changeset is a history record of deployment. 
```

```bash
cd <path_source_code>/wukong-darjeeling/wukong/gateway  
rm *.pyc *.json device*  

# Go to the WuKong gateway directory  
# Remove the compiled python files, JSON files, and the devices.pkl.
# The device.pkl is a file that includes the discovery result for gateway program. 
```

```bash
cd <path_source_code>/wukong-darjeeling/wukong/gateway/udpwkpf  
rm *.pyc *.json  

# Go to the device program directory  
# Remove the compiled Python files and the JSON
# The *.json are files that include detailed information of each device.
```

After resetting a WuKong system to its default settings, you should restart  Master and gateway, and then add devices to the WuKong system again.   