---
description: null
seo-description: null
seo-title: Implement standard ad metadata on JavaScript
title: Implement standard ad metadata on JavaScript
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
index: y
internal: n
snippet: y
---

# Implement standard ad metadata on JavaScript{#implement-standard-ad-metadata-on-javascript}

|  Constant name  | Description  |
|---|---|
|  | |
|  `StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad Object  |

* **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform: 

  ```js
  var adObject =  
    MediaHeartbeat.createAdObject(<AD_NAME>,  
                                  <AD_ID>,  
                                  <POSITION>,  
                                  <LENGTH>); 
       
  // Set standard Ad Metadata 
  var standardAdMetadata = {}; 
  standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser"; 
  standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign"; 
  adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
  ```

