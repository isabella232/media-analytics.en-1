---
title: Learn About Media Traking Timelines�Chapters
description: Learn about the playhead timeline and when a chapter starts and ends.
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
exl-id: e3f5bbdb-7007-435b-920c-566d163e57ad
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Timeline 3 - Chapters {#timeline-3-chapters}

## VOD, pre-roll ads, pausing, buffering, viewing content to the end


The following diagrams illustrate the playhead timeline and the corresponding timeline of a user's actions. The details for each action and its accompanying requests are presented below.


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## Action details


### Action 1 - Start session {#Action-1}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Auto-play or Play button pressed, video starts loading.  | 0 | 0 | `/api/v1/sessions`  |

**Implementation details**

This call signals _the intention of the user to play_ a video. It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. The player state is not yet "playing", but is instead "starting".  [Mandatory session parameters](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) must be included in the `params` map in the request body.  On the backend, this call generates an Adobe Analytics initiate call.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Action 2 - Ping timer starts {#Action-2}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App starts ping event timer | 0 | 0 | |

**Implementation details**

Start your ping timer. First ping event should then fire 1 second in if there are pre-roll ads, 10 seconds in otherwise.  

### Action 3 - Ad break start {#Action-3}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track pre-roll ad break start | 0 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ads can only be tracked within an ad break.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### Action 4 - Ad start {#Action-4}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 start | 0 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Start tracking the first pre-roll ad, which is 15 seconds long. Including custom metadata with this `adStart` .

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Action 5 - Ad pings {#Action-5}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 10 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 1 second. (Subsequent ad pings not shown in the interest of brevity.)

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 6 - Ad complete {#Action-6}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 complete | 15 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Track the end of the first pre-roll ad.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 7 - Ad start {#Action-7}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #2 start | 15 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Track the start of the second pre-roll ad, which is 7 seconds long.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 8 - Ad pings {#Action-8}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 16 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 1 second. (Subsequent ad pings not shown in the interest of brevity.)

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 9 - Ad complete {#Action-9}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #2 complete | 22 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Track the end of the second pre-roll ad.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 10 - Ad break complete {#Action-10}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track pre-roll ad break complete | 22 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

The ad break is over. Throughout the ad break, the play state has remained "playing".

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Action 11 - Play content {#Action-11}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track play event | 22 | 0 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

After the `adBreakComplete` event, put the player in the "playing" state using the `play` event.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 12 - Chapter start {#Action-12}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track chapter start event | 23 | 1 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

After the play event, track the start of the first chapter.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### Action 13 - Ping {#Action-13}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 30 | 8 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 10 seconds.

**Sample request body**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 14 - Buffer start {#Action-14}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Buffer start event occurred | 33 | 11 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Track the move to the "buffering" state.

**Sample request body**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### Action 15 - Buffer end (play) {#Action-15}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Buffering ended, the app tracks resumption of content | 36 | 11 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Buffering ends after 3 seconds, so put the player back to the "playing" state. You must send another track play event coming out of buffering.  **The `play` call after a `bufferStart` infers a "bufferEnd" call to the back end,** so there is no need for a `bufferEnd` event.

**Sample request body**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 16 - Ping {#Action-16}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 40 | 15 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 10 seconds.

**Sample request body**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 17 - Chapter end {#Action-17}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App tracks chapter end | 45 | 20 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

The first chapter ends, right before the second ad break.

**Sample request body**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### Action 18 - Ad break start {#Action-18}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track mid-roll ad break start | 46 | 21 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Mid-roll ad of 8 seconds duration: send `adBreakStart` .

**Sample request body**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### Action 19 - Ad start {#Action-19}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #3 start | 46 | 21 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Track the mid-roll ad.

**Sample request body**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 20 - Ad Pings {#Action-20}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 47 | 21 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 1 second. (Subsequent ad pings not shown in the interest of brevity.)

**Sample request body**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 21 - Ad complete {#Action-21}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #1 complete | 54 | 21 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

The mid-roll ad is complete.

**Sample request body**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 22 - Ad break complete {#Action-22}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track mid-roll ad break complete | 54 | 21 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

The ad break is complete.

**Sample request body**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Action 23 - Chapter start {#Action-23}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Track the start of Chapter 2 | 55 | 22 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**



**Sample request body**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### Action 24 - Ping {#Action-24}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 60 | 27 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 10 seconds.

**Sample request body**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 25 - Pause {#Action-25}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| User pressed Pause | 64 | 31 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

The user action moves the play state to "paused".

**Sample request body**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Action 26 - Ping {#Action-26}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 70 | 31 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 10 seconds. Player is still in the "buffering" state; the user is stuck at 20 seconds of content. Fuming...

**Sample request body**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 27 - Play content {#Action-27}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| User pressed Play to resume main content | 74 | 31 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Move the play state to "playing".  **The `play` call after a `pauseStart` infers a "resume" call to the back end**, so there is no need for a `resume` event.

**Sample request body**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 28 - Ping {#Action-28}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| App sends ping event | 80 | 37 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Ping the backend every 10 seconds.

**Sample request body**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 29 - Chapter end {#Action-29}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| Chapter 2 ends | 87 | 44 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Track the end of the second and final chapter.

**Sample request body**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### Action 30 - Session complete {#Action-30}

| Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request |
| --- | :---: | :---: | --- |
| The user finishes watching the content to the end.  | 88 | 45 | `/api/v1/sessions/{sid}/events`  |

**Implementation details**

Send `sessionComplete` to the backend to indicate that the user finished watching the entire content.

**Sample request body**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**No Seek Events? -** There is no explicit support in the Media Collection API for `seekStart` or `seekComplete` events. This is because certain players generate a very large number of such events when the end-user is scrubbing, and several hundred users could easily bottleneck the network bandwidth of a backend service. Adobe works around explicit support for seek events by computing heartbeat duration based on device timestamp, rather than playhead position.
