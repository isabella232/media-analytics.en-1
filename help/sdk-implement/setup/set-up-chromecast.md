---
title: How to Set up the Media SDK for Chromecast
description: Follow these steps to setup the Media SDK application on Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Set up Chromecast{#set-up-chromecast}

## FAQ

_Should I use the Chromecast JavaScript SDK or can I use the Standard JavaScript SDK?_

The correct answer is "Chromecast", for the following reasons:
* The AppMeasurement and VisitorAPI libraries in the Standard JS SDK are not certified to work on OTT platforms. In the Chromecast JS SDK, the Video Heartbeats Library (VHL), Analytics, and VisitorAPI are all built-in to the single, unified, certified-for-Chromecast SDK.
* The Chromecast SDK is much more lightweight than the standard JS SDK. This is very crucial for the lower-end hardware used by OTT platforms.

## Prerequisites

* **Obtain valid configuration parameters for Heartbeats**
   These parameters can be obtained from an Adobe representative after you set up your media analytics account.
* **Provide the following capabilities in your media player:**
   * *An API to subscribe to player events* - The Media SDK requires that you call a set of simple APIs when events occur in your player.
   * *An API that provides player information* - This information includes details such as the media name and the play head position.

Adobe Mobile services provides a new UI that brings together mobile marketing capabilities for mobile applications from across the Adobe Marketing Cloud. Initially, the Mobile service provides seamless integration of app analytics and targeting capabilities for the Adobe Analytics and Adobe Target solutions. Learn more at [Adobe Mobile Services documentation.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Chromecast SDK 2.x for Experience Cloud Solutions lets you measure Chromecast applications written in JavaScript, leverage and collect audience data through audience management, and measure video engagement through Video heartbeats.

## SDK Implementation

1. Add your [downloaded](/help/sdk-implement/download-sdks.md#download-2x-sdks) Chromecast library to your project.

    1. The `AdobeMobileLibrary-Chromecast-[version]` zip file consists of the following software components:

        * `adbmobile-chromecast.min.js`:

          This library file will be included in your Chromecast app source folder.

        * `ADBMobileConfig` config

          This SDK configuration file is customized for your app. A sample `ADBMobileConfig` implementation is provided with the SDK (under `samples/`). Obtain the proper settings from an Adobe representative.

    1. Add the library file to your `index.html` file, and create the `ADBMobileConfig` global variable as follows (the global variable used to configure Adobe Mobile for Heartbeats has an exclusive key named `mediaHeartbeat`):

       ```js    
       <script>
           var ADBMobileConfig = {
             "marketingCloud": {
               "org": "972C898555E9F7BC7F000101@AdobeOrg"
             },
             "target": {
               "clientCode": "",
               "timeout": 5
             },
             "audienceManager": {
               "server": "obumobile5.demdex.net"
             },
             "analytics": {
               "rsids": "mobile5vhl.sample.player",
               "server": "obumobile5.sc.omtrdc.net",
               "ssl": true,
               "offlineEnabled": false,
               "charset": "UTF-8",
               "lifecycleTimeout": 300,
               "privacyDefault": "optedin",
               "batchLimit": 0,
               "timezone": "MDT",
               "timezoneOffset": -360,
               "referrerTimeout": 0,
               "poi": []
             },
             "mediaHeartbeat": {
               "server": "obumobile5.hb.omtrdc.net",
               "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
               "channel": "test-channel-chromecast",
               "ssl": true,
               "ovp": "chromecast-player",
               "sdkVersion": "chromecast-sdk",
               "playerName": "Chromecast"
             }
           };
         </script>
       <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
       ```

       >[!IMPORTANT]
       >
       >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

       ADBMobile Config Parameters for mediaHeartbeat key:

   | Config Parameter | Description&nbsp;&nbsp;&nbsp;&nbsp; |
   | --- | --- |
   | `server` | String that represents the URL of the tracking endpoint on the backend.  |
   | `publisher` | String that represents the content publisher unique identifier.  |
   | `channel` | String that represents the name of the content distribution channel.  |
   | `ssl` | Boolean that represents whether SSL should be used for tracking calls.  |
   | `ovp` | String that represents the name of the video player provider.  |
   | `sdkversion` | String that represents the current version of the app/SDK.  |
   | `playerName` | String that represents the name of the player.  |


1. Configure Experience Cloud Visitor ID.

   The Experience Cloud Visitor ID service provides a universal Visitor ID across Experience Cloud solutions. The Visitor ID service is required by Video heartbeat and other Marketing Cloud integrations.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   After the configuration is complete, an Experience Cloud Visitor ID is generated and is included on all hits. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud Visitor ID Service Methods**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | Method | Description |
   | --- | --- |
   | `getMarketingCloudID()` | Retrieves the Experience Cloud Visitor ID from the Visitor ID service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | With the Experience Cloud Visitor ID, you can set additional customer IDs that can be associated with each visitor. The Visitor API accepts multiple customer IDs for the same visitor and a customer type identifier to separate the scope of the different customer IDs. This method corresponds to `setCustomerIDs()` in the JavaScript library.  For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. For tracking media, implement MediaDelegate protocol
   
   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }

    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
