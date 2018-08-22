---
description: null
seo-description: null
seo-title: Standard Metadata Parameters - Roku
title: Standard Metadata Parameters - Roku
uuid: 06a895e4-9c6a-488a-8df8-b985a770c7d9
index: y
internal: n
snippet: y
translate: y
---

# Standard Metadata Parameters - Roku

Standard video and ad metadata can be set on media and ad info objects respectively. Using the constants keys for video/ad metadata set the dictionary containing standard metadata on info object before calling the track APIs. Refer the tables below for the entire list of standard metadata constants, followed by sample. 

## Video Metadata Constants {#section_D26B0478688D4DC5AEFD82E9AC0F0C0D}



<table id="table_CE88520886C74050978BDA218E5D2E7D"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Metadata Name </th> 
   <th colname="col2" class="entry"> Context Data Key </th> 
   <th colname="col3" class="entry"> Constant Name </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Show </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.show</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeySHOW</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Season </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.season</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeySEASON</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Episode </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.episode</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyEPISODE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Asset </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.asset</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyASSET_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Genre </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.genre</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyGENRE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>First Air Date </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.airDate</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyFIRST_AIR_DATE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>First Digital Air Date </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.digitalDate</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Rating </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.rating</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyRATING</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Originator </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.originator</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyORIGINATOR</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Network </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.network</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyNETWORK</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Show Type </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.type</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeySHOW_TYPE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Ad Load </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.adLoad</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyAD_LOAD</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>MVPD </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.pass.mvpd</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyMVPD</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Authorized </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.pass.auth</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyAUTHORIZED</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Day Part </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.dayPart</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyDAY_PART</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Feed </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.feed</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeyFEED</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Stream Format </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.format</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_VideoMetadataKeySTREAM_FORMAT</span> </p> </td> 
  </tr> 
 </tbody> 
</table>


## Ad Metadata Constants {#section_5290E1BA54A24D30875F4F55C6CF9458}


<table id="table_5E6F5DA489E4454AB6D94BB7CEEFAA65"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Metadata Name </th> 
   <th colname="col2" class="entry"> Context Data Key </th> 
   <th colname="col3" class="entry"> Constant Name </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Advertiser </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.advertiser</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_AdMetadataKeyADVERTISER</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Campaign ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.campaign</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_AdMetadataKeyCAMPAIGN_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Creative ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.creative</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_AdMetadataKeyCREATIVE_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Placement ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.placement</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_AdMetadataKeyPLACEMENT_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Site ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.site</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_AdMetadataKeyPLACEMENT_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Creative URL </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.creativeURL</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> MEDIA_AdMetadataKeyCREATIVE_URL</span> </p> </td> 
  </tr> 
 </tbody> 
</table>


## Sample Implementation for Roku {#section_ij3_xcn_w2b}


```
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { }
mediaContextData["videotype"] = "episode"

standaradMetadata = {} standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyTMS_ID] = "sample tms_id" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyGENRE] = "sample genre"
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyFIRST_AIR_DATE] = "sample first_air_date" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE] = "sample first_digital_date" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyRATING] = "sample rating" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyORIGINATOR] = "sample originator" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyNETWORK] = "sample network" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW_TYPE] = "sample show type" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyAD_LOAD] = "sample ad load" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyMVPD] = "sample mvpd" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyAUTHORIZED] = "sample authorized" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyDAY_PART] = "sample day_part" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeyFEED] = "sample feed" 
standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySTREAM_FORMAT] = "sample format"

mediaInfo = adb_media_init_mediainfo(content.name, content.id, content.length, content.streamType) 
mediaInfo[ADBMobile().MEDIA_STANDARD_VIDEO_METADATA] = standaradMetadata 
ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)

```



```
// setting Standard Ad Metadata as context data on ad start event
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCREATIVE_ID] = "sample creativeid"
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyPLACEMENT_ID] = "sample placement id" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeySITE_ID] = "sample site id" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCREATIVE_URL] = "sample creative url"

adInfo = adb_media_init_adinfo(ad.title, ad.title, ad.position, ad.duration) 
adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, ad.contextData)

```

