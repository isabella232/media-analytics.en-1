---
seo-title: Track quality of experience on iOS
title: Track quality of experience on iOS
uuid: cae2c142-ed39-4234-a711-765dcabc5415
index: y
internal: n
snippet: y
---

# Track quality of experience on iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../sdk-implement/download-sdks.md).

1. Identify when the bitrate changes during video playback and create the `MediaObject` instance using the QoS information.

   **QoSObject variables:** 

   | Variable | Description | Required |
   | --- | --- | :---: |
   | `bitrate` | Current bitrate | Yes |
   | `startupTime` | Startup time | Yes |
   | `fps` | FPS value | Yes |
   | `droppedFrames` | Number of dropped frames | Yes | 

   >[!TIP]
   >
   >These variables are only required if you are planning to track QoS.

   **QoS object creation:** 

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Make sure that `getQoSObject` method returns the most updated QoS information. 
1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance: 

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.

