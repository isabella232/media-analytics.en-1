---
title: Test Call Details
description: Explore the calls you must make to validate your implementation.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Test call details{#test-call-details}

## Start the media player {#start-the-media-player}

### Adobe Analytics (AppMeasurement) Start call {#aa-start-call}

| Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Custom metadata fields**_ |
| _**`a.media.[value]`**_ | _**Standard metadata fields**_ |

**Notes:**

* Additional context data variables should be present and contain metadata. See metadata details below.
* Length for linear streams should be set to the best estimate for the current show.

### Standard metadata in Adobe Analytics (AppMeasurement) Start call {#std-metadata-aa}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Custom metadata in Adobe Analytics (AppMeasurement) Start call {#custom-metadata-aa}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics (heartbeats) Start call {#ma-start-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Custom metadata fields**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standard metadata fields**_ |

**Notes:**

* Additional context data variables should be present and contain metadata. See metadata details below.
* Playhead position for linear streams on video start should be set to the seconds elapsed since the start of the current show, not 0.

### Standard metadata in Media Analytics (heartbeats) Start call {#std-metadata-ma}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Custom metadata in Media Analytics (heartbeats) Start call {#custom-metadata-ma}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeats) Adobe Analytics Start call {#ma-aa-start}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notes:**

* This call indicates that the Media SDK has requested that an Adobe Analytics `pev2=ms_s` call be sent to the Adobe Analytics (AppMeasurement) server.
* This call does not contain custom metadata.

## View ad playback {#view-ad-playback}

### Adobe Analytics (AppMeasurement) Ad Start call {#aa-ad-start-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Metadata fields**_ |
| _**`a.media.[value]`**_ | _**Standard metadata fields**_ |

**Notes:**

* Additional context data variables should be present and contain metadata. See metadata details below.
* Ad length may be set to -1 if not available on ad start.

### Standard metadata in Adobe Analytics (AppMeasurement) Ad Start call {#std-metadata-aa-ad-start}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Custom metadata in Adobe Analytics (AppMeasurement) Ad Start call {#custom-metadata-aa-ad-start}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (heartbeats) Ad Start call {#ma-ad-start-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Custom metadata fields**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standard metadata fields**_ |

**Notes:**

* Additional context data variables should be present and contain metadata. See metadata details below.
* Ad length may be set to -1 if not available on ad start.

### Standard metadata in Media Analytics (heartbeats) Ad Start call {#std-metadata-ma-ad-start}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Custom metadata in Media Analytics (heartbeats) Ad Start call {#custom-metadata-ma-ad-start}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeats) Adobe Analytics Ad Start call {#ma-aa-ad-start-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Media Analytics (heartbeats) Ad Play call {#ma-ad-play-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (heartbeats) Ad Pause call {#ma-ad-pause-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (heartbeats) Adobe Analytics Ad Complete call {#ma-aa-ad-complete-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Play main content {#play-main-content}

### Media Analytics (heartbeats) Play call {#ma-play-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notes:**

* The playhead position should increment by 10 seconds with every play call.
* The `l:event:duration` value represents the number of milliseconds since the last tracking call and should be roughly the same value on each 10 second call.

## Pause main content {#pause-main-content}

### Media Analytics (heartbeats) Pause call {#ma-pause-call}

|  Parameter | &nbsp;Value (sample)&nbsp; |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
