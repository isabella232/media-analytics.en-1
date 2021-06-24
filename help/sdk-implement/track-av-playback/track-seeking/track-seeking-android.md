---
title: Learn How To Track Seeking on Android
description: Learn how to track Seek Start and Seek Complete events using the Media SDK on Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Media Analytics
role: "Business Practitioner, Administrator, Data Engineer"
---
# Track seeking on Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Seek tracking constants

|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `MediaHeartbeat.Event.SeekStart`  | Constant for tracking Seek Start event.  |
|  `MediaHeartbeat.Event.SeekComplete`  | Constant for tracking Seek Complete event.  |

## Implement seeking

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event: 

    ```java
    public void onSeekStart(Observable observable, Object data) {  
        _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
    }
    ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event: 

    ```java
    public void onSeekComplete(Observable observable, Object data) {  
        _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
    }
    ```

See the tracking scenario [VOD playback with seeking in the main content](/help/sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
