---
description: null
seo-description: null
seo-title: Sample Implementations for Standard Metadata
title: Sample Implementations for Standard Metadata
uuid: a01454d2-6885-4b4b-9ae7-7964bca6e485
index: y
internal: n
snippet: y
translate: y
---

# Sample Implementations for Standard Metadata


>
>```
>// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { }
>mediaContextData["videotype"] = "episode"
>
>standaradMetadata = {} standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyTMS_ID] = "sample tms_id" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyGENRE] = "sample genre"
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyFIRST_AIR_DATE] = "sample first_air_date" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE] = "sample first_digital_date" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyRATING] = "sample rating" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyORIGINATOR] = "sample originator" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyNETWORK] = "sample network" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW_TYPE] = "sample show type" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyAD_LOAD] = "sample ad load" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyMVPD] = "sample mvpd" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyAUTHORIZED] = "sample authorized" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyDAY_PART] = "sample day_part" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyFEED] = "sample feed" 
>standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySTREAM_FORMAT] = "sample format"
>
>mediaInfo = adb_media_init_mediainfo(content.name, content.id, content.length, content.streamType) 
>mediaInfo[ADBMobile().MEDIA_STANDARD_VIDEO_METADATA] = standaradMetadata 
>ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)
>
>```


>
>```
>// setting Standard Ad Metadata as context data on ad start event
>standardAdMetadata = {} 
>standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
>standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 
>standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCREATIVE_ID] = "sample creativeid"
>standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyPLACEMENT_ID] = "sample placement id" 
>standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeySITE_ID] = "sample site id" 
>standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCREATIVE_URL] = "sample creative url"
>
>adInfo = adb_media_init_adinfo(ad.title, ad.title, ad.position, ad.duration) 
>adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
>ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, ad.contextData)
>
>```

