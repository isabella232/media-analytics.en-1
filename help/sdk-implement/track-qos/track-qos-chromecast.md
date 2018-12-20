---
seo-title: Track quality of experience on Chromecast
title: Track quality of experience on Chromecast
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
index: y
internal: n
snippet: y
---

# Track quality of experience on Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../sdk-implement/download-sdks.md).

## Overview {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core video heartbeat implementations. You can use the video player API to identify the variables related to QoS and error tracking. Here are the key elements of tracking quality of experience:

>[!TIP]
>
>Additional details for each section is available in the [Implement](../../sdk-implement/track-qos/track-qos-overview.md) section.

**On all bitrate change events**:

* Create/update the QoS object instance for the playback, `qosObject`
* Call `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

**On player errors**:

* Call `trackError(“video error id”);`

## Implement {#section_3B8EBEB167624D0481E8AF4761F83047}

1. Identify when the bitrate changes during video playback and create the `MediaObject` instance using the QoS information.

   **QoSObject variables:** 

   >[!TIP]
   >
   >These variables are only required if you are planning to track QoS.

   | Variable | Description | Required |
   | --- | --- | :---: |
   | `bitrate` | Current bitrate | Yes |
   | `startupTime` | Startup time | Yes |
   | `fps` | FPS value | Yes |
   | `droppedFrames` | Number of dropped frames | Yes |

   **QoS object creation:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.

1. Make sure that `getQoSObject()` method returns the most updated QoS information. 
1. When the video player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](../../sdk-implement/track-errors/track-errors-overview.md).) 

   >[!TIP]
   >
   >Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

