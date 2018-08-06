---
description: Before you can use Video Heartbeat 2.x in JavaScript, you must set up an Experience Cloud account, enable the Visitor ID service, and obtain valid configuration parameters for measuring video heartbeats.
seo-description: Before you can use Video Heartbeat 2.x in JavaScript, you must set up an Experience Cloud account, enable the Visitor ID service, and obtain valid configuration parameters for measuring video heartbeats.
seo-title: Getting started
title: Getting started
uuid: f9b571a3-07a3-48dc-a942-15776580a6ed
index: y
internal: n
snippet: y
translate: y
---

# Getting started


## Prerequisites to implementing Video Analytics {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This guide is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.


Before you start implementing Video Heartbeat for JavaScript in the next section, ensure that you have completed the following tasks:

* **Set up an Experience Cloud account** - Contact an Adobe representative to assist you in setting up an Experience Cloud account for doing video analytics.
* **Implement `AppMeasurement` for JavaScript in your video application** - For more information about the Adobe Mobile SDK documentation, see [Implementing Analytics Using JavaScript](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html).
* **Implement the Visitor ID service** - For more information about the Visitor ID service, see [Implementing Analytics Using JavaScript](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html).
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.

