---
description: null
seo-description: null
seo-title: Getting started on Android
title: Getting started on Android
uuid: cd4ace04-fefb-4c82-a68f-4a7db9a56124
index: y
internal: n
snippet: y
translate: y
---

# Getting started on Android


<a id="section_kkf_4d2_r2b"></a>


* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_A5E180C4D4314B63A5863B45DE952A05)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_BDDB542FD36D4AD6AB799796BEA333DB)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_F25C35A43C944F3CB593609847861761)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_fmy_11q_q2b)




## Prerequisites {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This information is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.



Before you start implementing the Android SDK, ensure that you have completed the following tasks: 

* **General VA Prerequisites -** [](c_vhl_prereqs.md)
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Implement ADBMobile for Android in your application** - For more information about the Adobe Mobile SDK documentation, see [ Android SDK 4.x for Experience Cloud Solutions ](https://marketing.adobe.com/resources/help/en_US/mobile/android/).
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.


## Download and set up the SDK {#section_BDDB542FD36D4AD6AB799796BEA333DB}


1. [](c_vhl_download-sdks.md)
1. Expand the Android zip file (e.g., [!DNL  VideoHeartbeatLibrary-android-v2.*.zip]).
1. Verify that the [!DNL  VideoHeartbeat.jar] file exists in the [!DNL  libs/] directory.This library is used with Android devices and simulators for video heartbeat tracking APIs. 

1. Add the SDK to your project. **IntelliJ IDEA** - To add the SDK to your project using IntelliJ IDEA: 


    1. Right click your project in the ** [!UICONTROL  Project navigation] ** panel.
    1. Select ** [!UICONTROL  Open Module Settings] **.
    1. Under ** [!UICONTROL  Project Settings] **, select ** [!UICONTROL  Libraries] **.
    1. Click ** [!UICONTROL  +] ** to add a new library.
    1. Select ** [!UICONTROL  Java] ** and navigate to the ` VideoHeartbeat.jar` file.
    1. Select the modules in which you plan to use the mobile library.
    1. Click ** [!UICONTROL  Apply] ** and then ** [!UICONTROL  OK] ** to close the Module Settings window.


   **Eclipse** - To add the SDK to your project using Eclipse: 


    1. In the Eclipse IDE, right-click on the project name.
    1. Click  ** [!UICONTROL  Build Path] ** > ** [!UICONTROL  Add External Archives] ** .
    1. Select [!DNL  VideoHeartbeat.jar].
    1. Click ** [!UICONTROL  Open] **.
    1. Right-click the project again, and click  ** [!UICONTROL  Build Path] ** > ** [!UICONTROL  Configure Build Path] ** .
    1. Click the ** [!UICONTROL  Order] ** and ** [!UICONTROL  Export] ** tabs.
    1. Ensure that the [!DNL  VideoHeartbeat.jar] file is selected.



## Adding app permissions {#section_F25C35A43C944F3CB593609847861761}

The Video Heartbeat Library requires the following permissions to send data in tracking calls: 

* ` INTERNET`
* ` ACCESS_NETWORK_STATE`
To add these permissions, add the following lines to your [!DNL  AndroidManifest.xml] file in the application project directory: 

* ` &amp;lt;uses-permission android:name="android.permission.INTERNET" /&amp;gt;`
* ` &amp;lt;uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /&amp;gt;`

## Migrating to version 2.x in Android {#section_fmy_11q_q2b}

This information helps you migrate from version 1.5 to 2.x of the Android library.

In versions 2.x, all of the public methods are consolidated into the ` com.adobe.primetime.va.simple.MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the ` com.adobe.primetime.va.simple.MediaHeartbeatConfig` class. 

For detailed information about migrating from 1.x to 2.x, see [](c_vhl_mig_1x_to_2x.md). 
