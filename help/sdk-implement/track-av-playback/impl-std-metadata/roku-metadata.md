---
title: Roku Metadata Keys Explained
description: Learn about the available Roku metadata keys and view the entire list of standard metadata constants.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Roku metadata keys{#roku-metadata-keys}

Standard video, audio, and ad metadata can be set on media and ad info objects respectively. Using the constants keys for video/ad metadata set the dictionary containing standard metadata on info object before calling the track APIs. Refer the tables below for the entire list of standard metadata constants, followed by sample.

## Video metadata constants {#video-metadata-constants}

| Metadata Name | Context Data Key | Constant Name |
| --- | --- | --- |
| Show | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Season | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episode | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Asset | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genre | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| First Air Date | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| First Digital Air Date | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Rating | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Originator | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Network | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Show Type | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Ad Load | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Authorized | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Day Part | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Stream Format | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` | 

## Audio metadata constants {#audio-metadata-constants}

| Metadata Name | Context Data Key | Constant Name |
| --- | --- | --- |
| Artist | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Label | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Author | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Station | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Publisher | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Ad metadata constants {#ad-metadata-constants}

| Metadata Name | Context Data Key | Constant Name |
| --- | --- | --- |
| Advertiser | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| Campaign ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| Creative ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| Placement ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Site ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Creative URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` | 

## Constants {#constants}

You can use the following constants to track media events:

### Other constants

|  Constant  | Description&nbsp;&nbsp;  |
|---|---|
| `ERROR_SOURCE_PLAYER`  | Constant for Error source being Player  |

### MediaObjectkey constants (Used as keys within MediaObject instances)

| Constant | Description&nbsp;&nbsp; |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` |Constant to set metadata on the `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` |Constant to set the ad metadata on the `EventData` `trackEvent` |
| `MEDIA_RESUMED` | Constant for sending a video-resumed heartbeat. To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) `MEDIA_RESUMED` should be set to true when an application wants to continue to track content that a user stopped watching but now intends to resume watching. <br/><br/>For example, say a user watches 30% of the content, then closes the app. This will lead to the session being ended. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. The result is that these two different media sessions for the same video content can be linked together. Following is the implementation example: <br/><br/> `mediaInfo =` <br/> &nbsp;&nbsp;`adb_media_init_mediainfo(` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`"test_media_name",` <br/> &nbsp;&nbsp;&nbsp; `"test_media_id",`<br/> &nbsp;&nbsp;&nbsp;&nbsp; `10,` <br/>&nbsp;&nbsp;&nbsp;&nbsp; `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>This will create a new session for the video, but it also causes the SDK to send a heartbeat request with the event type "resume", which can be used in reporting to tie two different media sessions together.  | 

### Content type constants

|  Constant  | Description&nbsp;&nbsp;  |
|---|---|
|  `MEDIA_STREAM_TYPE_LIVE`  | Constant for Stream Type LIVE  |
|  `MEDIA_STREAM_TYPE_VOD`  | Constant for Stream Type VOD  |

### Event Type Constants (Used for the trackEvent call)

|  Constant  | Description&nbsp;&nbsp;  |
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
