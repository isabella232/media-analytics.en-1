---
description: null
seo-description: null
seo-title: Implement standard ad metadata on Roku
title: Implement standard ad metadata on Roku
uuid: 20a437d7-18b8-4099-ac81-9f3628384236

---

# Implement standard ad metadata on Roku{#implement-standard-ad-metadata-on-roku}

**Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform: 

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

