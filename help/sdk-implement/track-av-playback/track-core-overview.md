---
seo-title: Overview
title: Overview
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
index: y
internal: n
snippet: y
---

# Overview{#overview}

>[!IMPORTANT]
>
>This documentation covers tracking in version 2.x of the SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md)

<a id="section_904E0524877241939A0E0557E7395C4A"></a>

Tracking core playback includes tracking media load, media start, media pause, and media complete. Although not mandatory, tracking buffering and seeking are also core components used for tracking content playback. In your media player API, identify the player events that correspond with the Media SDK tracking calls, and code your event handlers to call tracking APIs, and to populate required and optional variables.

**On media load:**

* Create the media object 
* Populate metadata 
* Call `trackSessionStart`; for example: `trackSessionStart(mediaObject, contextData)`

**On media start:**

* Call `trackPlay`

**On pause/resume:**

* Call `trackPause`
* Call `trackPlay` *when playback resumes*

**On media complete:**

* Call `trackComplete`

**On media abort:**

* Call `trackSessionEnd`

**When scrubbing starts:**

* Call `trackEvent(SeekStart)`

**When scrubbing ends:**

* Call `trackEvent(SeekComplete)`

**When buffering starts:**

* Call `trackEvent(BufferStart);`

**When buffering ends:**

* Call `trackEvent(BufferComplete);`

>[!TIP]
>
>The playhead position is set as part of the set-up and configuration code. For more information about `getCurrentPlayheadTime`, see *Set up and configure:* [](../../sdk-implement/setup/setup-overview.md).

## Implement {#section_BB217BE6585D4EDEB34C198559575004}

1. **Initial tracking setup -** Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance using the media information for content name, content ID, content length, and stream type.

   **`MediaObject` reference:** 

   |  Variable Name  | Description  | Required  |
   |---|---|---|
   |  `name`  | Content name  | Yes  |
   |  `mediaid`  | Content unique identifier  | Yes  |
   |  `length`  | Content length  | Yes  |
   |  `streamType`  | Stream type  | Yes  |
   |  `mediaType`  | Media type (audio or video content)  | Yes  |

   **`StreamType` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  `VOD`  | Stream type for Video on Demand.  |
   |  `LIVE`  | Stream type for Live content.  |
   |  `LINEAR`  | Stream type for Linear content.  |
   |  `AOD`  | Stream type for audio on demand  |
   |  `AUDIOBOOK`  | Stream type for audio book  |
   |  `PODCAST`  | Stream type for Podcast  |

   **`MediaType` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  `Audio`  | Media type for Audio streams.  |
   |  `Video`  | Media type for Video streams.  |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Attach metadata -** Optionally attach standard and/or custom metadata objects to the tracking session through context data variables.

    * **Standard metadata -** 
    
      >[!NOTE]
      >
      >Attaching the standard metadata object to the media object is optional.

      Instantiate a standard metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object.

      See the comprehensive list of metadata here: [](../../metrics-and-metadata/audio-video-parameters.md)
    
    * **Custom metadata -** Create a variable object for the custom variables and populate with the data for this content.

1. **Track the intention to start playback -** To begin tracking a session, call `trackSessionStart` on the Media Heartbeat instance. 

   >[!IMPORTANT]
   >
   >`trackSessionStart` tracks the user intention of playback, not the beginning of the playback. This API is used to load the data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Track the actual start of playback -** Identify the event from the media player for the beginning of the playback, where the first frame of the content is rendered on the screen, and call `trackPlay`. 

1. **Track the completion of playback -** Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`. 

1. **Track the end of the session -** Identify the event from the media player for the unloading/closing of the playback, where the user closes the content and/or the content is completed and has been unloaded, and call `trackSessionEnd`. 

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Track all possible pause scenarios -** Identify the event from the media player for pause and call `trackPause`.

   **Pause Scenarios -** Identify any scenario in which the Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

    * The user explicitly hits pause in the app.
    * The player puts itself into the Pause state.
    * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
    * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the content from the point of interruption.

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`. 

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. Listen for playback seeking events from the media player. On seek start event notification, track seeking using the `SeekStart` event.
1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event. 
1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event. 
1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

See examples of each step in the following platform-specific topics, and look at the sample players included with your SDKs.

For a simple example of playback tracking, see this use of the JavaScript 2.x SDK in an HTML5 player: 

```js
/* Call on media start */ 
if (e.type == "play") { 
 
    // Check for start of media 
    if (!sessionStarted) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                            <VIDEO_ID>,  
                                            <VIDEO_LENGTH>, 
                                            MediaHeartbeat.StreamType.VOD);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    sessionStarted = false;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## Validate {#section_ABCFB92C587B4CAABDACF93452EFA78F}

**Content Start**

On start of a media player, these key calls are sent in the following order:

1. Media analytics start
1. Heartbeat start
1. Heartbeat analytics start

Calls 1 and 2 contain additional metadata variables for both custom and standard.

**Content Play**

During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds.

**Content Complete**

At the 100% point, on content or at a show boundary on a linear stream, a Heartbeat complete call will be sent.

**Content Pause**

When the player pauses, player pause event calls will be sent every 10 seconds. After pause ends, the play events should resume.

**Content Scrub/Seek**

On scrubbing of the playhead, no special tracking calls are sent. However, when playback resumes after scrubbing, the playhead value should reflect the new position in the main content.

**Content Buffer**

When the media player buffers, player buffer event calls are sent every 10 seconds. After buffering ends, the play events should resume. 
