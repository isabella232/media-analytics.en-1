---
title: Implement standard ad metadata on JavaScript
description: 
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3

---

# Implement standard ad metadata on JavaScript{#implement-standard-ad-metadata-on-javascript}

## Ad constants

|  Constant name  | Description&nbsp;&nbsp;  |
|---|---|
|  `StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad Object  |

## Implemement standard ad metadata

For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform: 

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

