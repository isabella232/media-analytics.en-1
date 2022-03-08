---
title: How to Set up the Media SDK for Roku
description: Follow these steps to setup the Media SDK application on Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Set Up Roku{#set-up-roku}

## Prerequisites

* **Obtain valid configuration parameters for Heartbeats**
   These parameters can be obtained from an Adobe representative after you set up your media analytics account.
* **Provide the following capabilities in your media player:**
    * _An API to subscribe to player events_ - The Media SDK requires that you call a set of simple APIs when events occur in your player.
    * _An API that provides player information_ - This information includes details such as the media name and the play head position.

Adobe Mobile services provides a new UI that brings together mobile marketing capabilities for mobile applications from across the Adobe Marketing Cloud. Initially, the Mobile service provides seamless integration of app analytics and targeting capabilities for the Adobe Analytics and Adobe Target solutions.

Learn more at [Adobe Mobile Services documentation.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Roku SDK 2.x for Experience Cloud Solutions lets you measure Roku applications written in BrightScript, leverage and collect audience data through audience management, and measure video engagement through Video heartbeats.

## SDK Implementation

1. Add your [downloaded](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku library to your project.

    1. The `AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components:

       * `adbmobile.brs`: This library file will be included in your Roku app source folder.

       * `ADBMobileConfig.json`: This SDK configuration file is customized for your app.

    1. Add the library file and JSON config file to your project source.

       The JSON that is used to configure Adobe Mobile has an exclusive key for media heartbeats called `mediaHeartbeat`. This is where the configuration parameters for the media heartbeats belong.

       >[!TIP]
       >
       >A sample `ADBMobileConfig` JSON file is provided with the package. Contact your Adobe representatives for the settings.

       For example:     

       ```    
       {
         "version":"1.0",
         "analytics":{
           "rsids":"",
           "server":"",
           "charset":"UTF-8",
           "ssl":true,
           "offlineEnabled":false,
           "lifecycleTimeout":30,
           "batchLimit":50,
           "privacyDefault":"optedin",
           "poi":[ ]
       },
       "marketingCloud":{
         "org":""
       },
       "target":{
         "clientCode":"",
         "timeout":5
       },
       "audienceManager":{
         "server":""
       },
       "acquisition":{
         "server":"example.com",
         "appid":"sample-app-id"
       },

       "mediaHeartbeat":{
          "server":"example.com",
          "publisher":"sample-publisher",
          "channel":"sample-channel",
          "ssl":true,
          "ovp":"sample-ovp",
          "sdkVersion":"sample-sdk",
          "playerName":"roku"
          }    
       }
       ```

       | Config Parameter | Description&nbsp;&nbsp;&nbsp;&nbsp; |
       | --- | --- |
       | `server` | String that represents the URL of the tracking endpoint on the backend.  |
       | `publisher` | String that represents the content publisher unique identifier.  |
       | `channel` | String that represents the name of the content distribution channel.  |
       | `ssl` | Boolean that represents whether SSL should be used for tracking calls.  |
       | `ovp` | String that represents the name of the video player provider.  |
       | `sdkversion` | String that represents the current version of the app/SDK.  |
       | `playerName` | String that represents the name of the player.  |

       >[!IMPORTANT]
       >
       >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

1. Configure Experience Cloud Visitor ID.

    The Experience Cloud Visitor ID service provides a universal Visitor ID across Experience Cloud solutions. The Visitor ID service is required by Video heartbeat and other Marketing Cloud integrations.

    Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

    ```
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

    | &nbsp;Method&nbsp;&nbsp; | Description |
    | --- | --- |
    | `visitorMarketingCloudID` | Retrieves the Experience Cloud visitor ID from the visitor ID service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
    | `visitorSyncIdentifiers` | With the Experience Cloud Visitor ID, you can set additional customer IDs that can be associated with each visitor. The Visitor API accepts multiple customer IDs for the same visitor and a customer type identifier to separate the scope of the different customer IDs. This method corresponds to `setCustomerIDs`. For example: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
    | `setAdvertisingIdentifier` | Used to set the Roku ID for Advertising (RIDA) on the SDK. For example: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>&nbsp;&nbsp;`"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Get the Roku ID for Advertising (RIDA) using the Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API. |
    | `getAllIdentifiers` | Returns a list of all the identifiers stored by the SDK including Analytics, Visitor, Audience Manager and custom Identifiers. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()`|
    <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

    **Additional Public APIs**

    **DebugLogging**

    | &nbsp;Method&nbsp;&nbsp; | Description |
    | --- | --- |
    | `setDebugLogging` | Used to enable or disable debug logging for the SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` |
    | `getDebugLogging` | Returns true if debug logging is enabled.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

    **PrivacyStatus**

    | &nbsp;Constant&nbsp;&nbsp; | Description |
    | --- | --- |
    | `PRIVACY_STATUS_OPT_IN` | Constant to be passed while calling setPrivacyStatus to opt in. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`|
    | `PRIVACY_STATUS_OPT_OUT` | Constant to be passed while calling setPrivacyStatus to opt out. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

    | &nbsp;Method&nbsp;&nbsp; | Description |
    | --- | --- |
    | `setPrivacyStatus` | Sets the privacy status on the SDK.  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
    | `getPrivacyStatus` | Gets the current privacy status set on the SDK.  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

    >[!IMPORTANT]
    >
    >Ensure that you call `processMessages` and `processMediaMessages` function in the main event loop every 250 ms to ensure that the SDK sends out the pings properly.

    | &nbsp;Method&nbsp;&nbsp; | Description |
    | --- | --- |
    | `processMessages` | Responsible to pass the Analytics events to the SDK to be handled.  <br/><br/>`ADBMobile().processMessages()`|
    | `processMediaMessages` | Responsible to pass the Media events to the SDK to be handled. <br/><br/>`ADBMobile().processMediaMessages()`|


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
