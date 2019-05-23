---
seo-title: Track quality of experience on Roku
title: Track quality of experience on Roku
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a

---

# Track quality of experience on Roku{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Implemement QOS

1. Identify when the bitrate changes during media playback, and use the `mediaUpdateQoS` API to update the QoS info on the Media SDK.

    QoSObject variables: 
 
    >[!TIP]
    >
    >These variables are only required if you are tracking QoS.
 
    | Variable | Description | Required |
    | --- | --- | :---: |
    | `bitrate` | Current bitrate | Yes |
    | `startupTime` | Startup time | Yes |
    | `fps` | FPS value | Yes |
    | `droppedFrames` | Number of dropped frames | Yes |
 
    For example:

    ```
    bitrate = 200000
    fps = 0
    droppedFrames = 1
    startupTime = 2
    qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)

    ADBMobile().mediaUpdateQoS(qosinfo)
    ```

    <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. When playback switches bitrates, call `trackEvent(BitrateChange)` to notify the Media SDK that the Bitrate changed. 

    ```
    ADBMobile().trackMediaEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
    ```

    >[!NOTE]
    >
    >You need to call `updateQoSObject` with the updated bitrate value.

    <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](../../sdk-implement/track-errors/track-errors-overview.md).)

    >[!TIP]
    >
    >Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

