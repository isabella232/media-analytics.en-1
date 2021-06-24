---
title: How to Set up the Media SKD Using JavaScript 2.x
description: Follow these steps to setup the Media SDK application on JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: "Business Practitioner, Administrator, Data Engineer"
---
# Set up JavaScript 2.x{#set-up-javascript}

## Prerequisites

* **Obtain valid configuration parameters**
   These parameters can be obtained from an Adobe representative after you set up your analytics account.
* **Implement `AppMeasurement` for JavaScript in your media application**
   For more information about the Adobe Mobile SDK documentation, see [Implementing Analytics Using JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)

* **Provide the following capabilities in your media player:**

    * *An API to subscribe to player events* - The Media SDK requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.

1. Add your [downloaded](/help/sdk-implement/download-sdks.md#download-2x-sdks) library to your project. Create local references to the classes for convenience.

   1. Expand the `MediaSDK-js-v2.*.zip` file that you downloaded.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      This core JavaScript file must be hosted on a web server that is accessible to all pages on your site. You need the path to these files for the next step.

   1. Reference `MediaSDK.min.js` on all site pages.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. For example:     

      ```    
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. To quickly verify that the library was successfully imported, instantiate the `ADB.va.MediaHeartbeatConfig` class.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. For easy access to the APIs, create local references to the `MediaHeartbeat` classes.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Create a `MediaHeartbeatConfig` instance.

   This section helps you to understand `MediaHeartbeat` config parameters and how to set correct config values on your `MediaHeartbeat` instance, for accurate tracking.

   Here is a sample `MediaHeartbeatConfig` initialization:

   ```js
   //Media Heartbeat initialization
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
   mediaConfig.playerName = Configuration.PLAYER.NAME;
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
   mediaConfig.ssl = false;
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate();

   // Replace <currentPlaybackTime> with the video player current playback time
   mediaDelegate.getCurrentPlaybackTime = function() {
       return <currentPlaybackTime>;
   };

   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. This instance will be used for all of the following tracking events.

   >[!TIP]
   >
   >`MediaHeartbeat` requires an instance of `AppMeasurement` to send calls to Adobe Analytics. Here is an example of an `AppMeasurement` instance:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```   

## Migrate from JavaScript 1.x to 2.x

In version 2.x, all of the public methods are consolidated into the `ADB.va.MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the `ADB.va.MediaHeartbeatConfig` class.

For detailed information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
