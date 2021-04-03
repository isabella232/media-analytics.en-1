---
title: Setup Overview
description: Overview of setting up the Media SDK for media tracking in your mobile, OTT, and browser (JS) applications.
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
---
# Setup Overview{#setup-overview}

>[!IMPORTANT]
>
>With the end of support for Version 4 Mobile SDKs on August 31, 2021, Adobe will also end support for the Media Analytics SDKs for iOS and Android.  For additional information, see [Media Analytics SDK End-of-Support FAQs](/help/sdk-implement/end-of-support-faqs.md).

The following instructions apply to the 2.x Media SDKs. If you are implementing a 1.x version of the Media SDK, see the [1.x Media SDK Documentation.](/help/sdk-implement/download-sdks.md) For Primetime integrators, see _Primetime Media SDK Documentation_ below.

## Minimum Platform Version Support {#minimum-platform-version}

The following table describes the minimum platform versions supported for each SDK, beginning February 19, 2019.

| OS/Browser | Min Version Required |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## General Implementation Guidelines {#general-implementation-guidelines}

There are three main SDK components involved in media tracking:
* Media Heartbeat Config - The config contains the basic settings for reporting.
* Media Heartbeat Delegate - The delegate controls playback time and the QoS object.
* Media Heartbeat - The primary library containing members and methods.

Complete the following implementation steps:

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  &nbsp;Variable Name&nbsp; | Description&nbsp; | Required | &nbsp;Default Value&nbsp; |
   |---|---|:---:|---|
   |  `trackingServer`  | Tracking server for media analytics. This is different from your analytics tracking server. | Yes | Empty String |
   |  `channel`  | Channel name  | No  | Empty String  |
   |  `ovp`  | Name of the online media platform through which content gets distributed  | No  | Empty String  |
   |  `appVersion`  | Version of the media player app/SDK  | No  | Empty String  |
   |  `playerName`  | Name of the media player in use, i.e., "AVPlayer", "HTML5 Player", "My Custom Player"  | No  | Empty String  |
   |  `ssl`  | Indicates whether calls should be made over HTTPS  | No  | false  |
   |  `debugLogging`  | Indicates whether debug logging is enabled  | No  | false  |

1. Implement the `MediaHeartbeatDelegate`.

    | &nbsp;Method name&nbsp; | &nbsp;Description&nbsp; | Required |
    | --- | --- | :---: |
    | `getQoSObject()` | Returns the `MediaObject` instance that contains the current QoS information. This method will be called multiple times during a playback session. Player implementation must always return the most recently available QoS data.  | Yes |
    | `getCurrentPlaybackTime()` | Returns the current position of the playhead. For VOD tracking, the value is specified in seconds from the beginning of the media item. For LINEAR/LIVE tracking, the value is specified in seconds from the beginning of the program.  | Yes |

   >[!TIP]
   >
   >The Quality of Service (QoS) object is optional. If QoS data is available for your player and you wish to track that data, then the following variables are required:

   |  Variable name  | Description&nbsp;&nbsp;  | Required  |
   | --- | --- | :---: |
   |  `bitrate`  | The bitrate of media in bits per second.  | Yes  |
   |  `startupTime`  | The start up time of media in milliseconds.  | Yes  |
   |  `fps`  | The frames displayed per second.  | Yes  |
   |  `droppedFrames`  | The number of dropped frames so far.  | Yes  |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. This instance will be used for all the following media tracking events.

   >[!TIP]
   >
   >`MediaHeartbeat` requires an instance of `AppMeasurement` to send calls to Adobe Analytics.

1. Combine all of the pieces.

   The following sample code utilizes our JavaScript 2.x SDK for an HTML5 video player:

   ```javascript
   // Create local references to the heartbeat classes
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;

   //Media Heartbeat Config
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net";
   mediaConfig.playerName = "HTML5 Basic";
   mediaConfig.channel = "Video Channel";
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = "2.0";
   mediaConfig.ssl = false;
   mediaConfig.ovp = "";

   // Media Heartbeat Delegate
   var mediaDelegate = new MediaHeartbeatDelegate();

   // Set mediaDelegate CurrentPlaybackTime
   mediaDelegate.getCurrentPlaybackTime = function() {
       return video.currentTime;
   };

   // Set mediaDelegate QoSObject - OPTIONAL
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes);
   }
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Validate {#validate}

Media Analytics tracking implementations generate two types of tracking calls:

* Media and ad Start calls are sent directly to the Adobe Analytics (AppMeasurement) server.
* Heartbeat calls are sent to the Media Analytics (heartbeats) tracking server, processed there, and passed on to the Adobe Analytics server.

* **Adobe Analytics (AppMeasurement) server**
   For more information about tracking server options, see [Correctly populate the trackingServer and trackingServerSecure variables.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >An RDC tracking server or CNAME resolving to an RDC server is required for Experience Cloud Visitor ID service.

  The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Media Analytics (Heartbeats) server**
   This always has the format "`[your_namespace].hb.omtrdc.net`". The value of "`[your_namespace]`" specifies your company, and is provided by Adobe.

Media tracking works the same across all platforms, desktop and mobile. Audio tracking currently works on mobile platforms. For all tracking calls there are a few key universal variables to be validated:

## SDK 1.x Documentation {#sdk-1x-documentation}

| Video&nbsp;Analytics&nbsp;1.x&nbsp;SDKs&nbsp; | &nbsp;Developer&nbsp;Guides&nbsp;(PDFs only) |
| --- | --- |
| Android | [Configure for Android ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [Configure for AppleTV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configure for Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configure for iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configure for JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android: &nbsp; [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS: &nbsp; [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_ ) </li> <li> iOS: &nbsp; [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configure for TVML ](vhl_tvml.pdf) |

## Primetime Media SDK Documentation {#primetime-docs}

* [Primetime User Guides](https://helpx.adobe.com/primetime/user-guide.html)
