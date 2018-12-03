---
seo-title: Roku metadata keys
title: Roku metadata keys
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
index: y
internal: n
snippet: y
---

# Roku metadata keys{#roku-metadata-keys}

Standard video and ad metadata can be set on media and ad info objects respectively. Using the constants keys for video/ad metadata set the dictionary containing standard metadata on info object before calling the track APIs. Refer the tables below for the entire list of standard metadata constants, followed by sample.

## Video metadata constants {#section_D26B0478688D4DC5AEFD82E9AC0F0C0D}

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

## Ad metadata constants {#section_5290E1BA54A24D30875F4F55C6CF9458}

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

## Constants {#section_F55145DBE77F45B988849C42C044C7DA}

You can use the following constants to track media events:

### Other constants

|  Constant  | Description  |
|---|---|
| `ERROR_SOURCE_PLAYER`  | Constant for Error source being Player  |

### MediaObjectkey constants (Used as keys within MediaObject instances)

<table id="table_cqh_44m_ddb">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Constant </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MEDIA_STANDARD_VIDEO_METADATA</span> </td> 
   <td colname="col2">Constant to set video metadata on the <span class="codeph"> MediaInfo</span> object in the <span class="codeph"> trackLoad</span> API. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MEDIA_STANDARD_AD_METADATA</span> </td> 
   <td colname="col2">Constant to set the ad metadata on the <span class="codeph"> EventData</span> object in the <span class="codeph"> trackEvent</span> API for Ad start. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> VIDEO_RESUMED</span> </td> 
   <td colname="col2"> <p>Constant for sending a video-resumed heartbeat. To resume video tracking of previously stopped content, you need to set the <span class="codeph"> VIDEO_RESUMED</span> <i>property</i> on the <span class="codeph"> mediaInfo</span> object when you call <b><span class="codeph"> mediaTrackLoad</span></b>. (<span class="codeph"> VIDEO_RESUMED</span> is not an event that you can track using the <b><span class="codeph"> mediaTrackEvent</span></b> API.) <span class="codeph"> VIDEO_RESUMED</span> should be set to <span class="codeph"> true</span> when an application wants to continue to track content that a user stopped watching but now intends to resume watching. </p> <p>For example, say a user watches 30% of the content, then closes the app. This will lead to the session being ended. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they previously left off, then the application should set <span class="codeph"> VIDEO_RESUMED</span> to "true" while calling the <span class="codeph"> mediaTrackLoad</span> API. The result is that these two different media sessions for the same video content can be linked together. Following is the implementation example: 
     <codeblock>
      mediaInfo&nbsp;=&nbsp;
      
&nbsp;&nbsp;adb_media_init_mediainfo("test_media_name",&nbsp;
      
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"test_media_id",&nbsp;
      
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;10,&nbsp;
      
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"vod")
      
mediaInfo[ADBMobile().VIDEO_RESUMED]&nbsp;=&nbsp;true
      
mediaContextData&nbsp;=&nbsp;{}
      
ADBMobile().mediaTrackLoad(mediaInfo,&nbsp;mediaContextData)
     </codeblock> This will create a new session for the video, but it also causes the SDK to send a heartbeat request with the event type "resume", which can be used in reporting to tie two different media sessions together.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Content type constants

|  Constant  | Description  |
|---|---|
|  `MEDIA_STREAM_TYPE_LIVE`  | Constant for Stream Type LIVE  |
|  `MEDIA_STREAM_TYPE_VOD`  | Constant for Stream Type VOD  |

### Event Type Constants (Used for the trackEvent call)

|  Constant  | Description  |
|---|---|
|  `MEDIA_BUFFER_START`  | Event Type for Buffer Start  |
|  `MEDIA_BUFFER_COMPLETE`  | Event Type for Buffer Complete  |
|  `MEDIA_SEEK_START`  | Event Type for Seek Start  |
|  `MEDIA_SEEK_COMPLETE`  | Event Type for Seek Complete  |
|  `MEDIA_BITRATE_CHANGE`  | Event Type for Bitrate change  |
|  `MEDIA_CHAPTER_START`  | Event Type for Chapter Start  |
|  `MEDIA_CHAPTER_COMPLETE`  | Event Type for Chapter Complete  |
|  `MEDIA_CHAPTER_SKIP`  | Event Type for Ad Start  |
|  `MEDIA_AD_BREAK_START`  | Event Type for Ad Start  |
|  `MEDIA_AD_BREAK_COMPLETE`  | Event Type for AdBreak Complete  |
|  `MEDIA_AD_BREAK_SKIP`  | Event Type for AdBreak Skip  |
|  `MEDIA_AD_START`  | Event Type for Ad Start  |
|  `MEDIA_AD_COMPLETE`  | Event Type for Ad Complete  |
|  `MEDIA_AD_SKIP`  | Event Type for Ad Skip  |

