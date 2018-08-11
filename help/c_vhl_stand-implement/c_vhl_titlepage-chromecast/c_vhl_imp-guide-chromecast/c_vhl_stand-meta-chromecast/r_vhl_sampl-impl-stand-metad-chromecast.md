---
description: null
seo-description: null
seo-title: Sample Implementations for Standard Metadata
title: Sample Implementations for Standard Metadata
uuid: cdc4d67f-4bfa-4694-aaa6-0904924d9528
index: y
internal: n
snippet: y
translate: y
---

# Sample Implementations for Standard Metadata


>
>```
>js>// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
>mediaMetadata["videotype"] = "episode"; 
> 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
>standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
> 
>var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
>mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
>ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
>
>```


>
>```
>js>// setting Standard Ad Metadata as context data on ad start event 
>var standardAdMetadata = {}; 
>standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = “sample campaign”; 
>standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
>standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
>standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
>standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
>standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
> 
>var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
>adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
> 
>ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
>```

