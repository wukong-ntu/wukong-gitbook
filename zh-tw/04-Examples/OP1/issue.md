#4.1.5. 尋找裝置問題

在**尋找裝置**時，一個很常見的問題是當移動到不同的網路環境下，並且獲取了新的 IP 位置。然而在主控台、通訊閘或裝置們，依舊保存了之前舊的 IP 位置，而沒有更新。
為了解決這個問題，你必須依照下列步驟來重設悟空系統。此外，當有部分裝置在同一網域內，但卻無法被尋找到時也可以用此方法重設整個系統。

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

當重設完成後，你必須重新啟動主控台、通訊閘，並一一把裝置加回。  