---
title: Learn to Track Quality of Experience Using JavaScript 2.x
description: "Learn about implementing quality of experience (QoE, QoS) tracking using the Media SDK in browser apps using JavaScript 2.x."
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Track quality of experience using JavaScript 2.x{#track-quality-of-experience-on-javascript}

The following instructions provide guidance for implementation across all 2.x SDKs.

>[!IMPORTANT]
>
>If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implemement QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

    QoSObject variables:

    >[!TIP]
    >
    >These variables are only required if you are planning to track QoS.

     | Variable | Description | Required |
     | --- | --- | :---: |
     | `bitrate` | Current bitrate | Yes |
     | `startupTime` | Startup time | Yes |
     | `fps` | FPS value | Yes |
     | `droppedFrames` | Number of dropped frames | Yes |

    QoS object creation:

    ```js
    // Replace <bitrate>, <startuptime>, <fps> and  
    // <droppeFrames> with the current playback QoS values.  
    var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                   <startuptime>,  
                                                   <fps>,  
                                                   <droppedFrames>);

    ```

1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance:

    ```js
    _onBitrateChange = function() {
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
    };
    ```

    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.

1. Make sure that `getQoSObject()` method returns the most updated QoS information.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.
