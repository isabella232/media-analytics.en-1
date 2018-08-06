---
description: Before you can use Video Heartbeat 2.x in Android, you must set up a Experience Cloud account, enable the Visitor ID service, and obtain valid configuration parameters for measuring video heartbeats.
seo-description: Before you can use Video Heartbeat 2.x in Android, you must set up a Experience Cloud account, enable the Visitor ID service, and obtain valid configuration parameters for measuring video heartbeats.
seo-title: Getting started on Android
title: Getting started on Android
uuid: d349cef2-00f3-45be-83dc-bd15e39ff9cd
index: y
internal: n
snippet: y
translate: y
---

# Getting started on Android


## Prerequisites to implementing Video Analytics {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This guide is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.


Before you start implementing Video Heartbeat for Android in the next section, ensure that you have completed the following tasks:

* **Set up an Experience Cloud account** - Contact an Adobe representative to assist you in setting up an Experience Cloud account for doing video analytics.
* **Implement ADBMobile for Android in your application** - For more information about the Adobe Mobile SDK documentation, see [Android SDK 4.x for Experience Cloud Solutions](https://marketing.adobe.com/resources/help/en_US/mobile/android/).
* **Implement the Visitor ID service** - For more information about the Visitor ID service, see [Experience Cloud ID Service](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.

