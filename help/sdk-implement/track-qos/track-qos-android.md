---
title: Learn How to Track Quality of Experience on Android
description: "Learn about implementing quality of experience (QoE, QoS) tracking using the Media SDK on Android."
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Track quality of experience on Android{#track-quality-of-experience-on-android}

The following instructions provide guidance for implementation across all 2.x SDKs.

>[!IMPORTANT]
>
>If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implemement QoS

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

    ```java
    MediaObject qosObject =  
      MediaHeartbeat.createQoSObject(<BITRATE>,  
                                     <STARTUP_TIME>,  
                                     <FPS>,  
                                     <DROPPED_FRAMES>);
    ```

1. Make sure that `getQoSObject()` method returns the most updated QoS information.
1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance:

    ```java
    public void onBitrateChange(Observable observable, Object data) {  
        _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null);
    }
    ```

    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
