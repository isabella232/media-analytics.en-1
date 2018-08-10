---
description: null
seo-description: null
seo-title: Getting started on JavaScript
title: Getting started on JavaScript
uuid: 5f8f76fd-6cce-4c3d-b9da-430285160abe
index: y
internal: n
snippet: y
translate: y
---

# Getting started on JavaScript


<a id="section_kkf_4d2_r2b"></a>


* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_A5E180C4D4314B63A5863B45DE952A05)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_BDDB542FD36D4AD6AB799796BEA333DB)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_wmk_pjf_r2b)




## Prerequisites {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This information is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.



Before you start implementing Video Heartbeat for JavaScript in the next section, ensure that you have completed the following tasks: 

* **General VA Prerequisites -** [](c_vhl_prereqs.md)
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Implement ` AppMeasurement` for JavaScript in your video application** - For more information about the Adobe Mobile SDK documentation, see [ Implementing Analytics Using JavaScript ](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html).
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.


## Download and set up the SDK {#section_BDDB542FD36D4AD6AB799796BEA333DB}


1. [](c_vhl_download-sdks.md)
1. Expand the ` VideoHeartbeatLibrary-js-v2.*.zip` file that you downloaded.
1. Verify that the ` VideoHeartbeat.min.js` file exists in the ` libs` directory: This library is designed for use with desktop/browsers, with APIs for video heartbeat tracking. 

1. Host the [!DNL  VideoHeartbeat.min.js] file. This core JavaScript file must be hosted on a web server that is accessible to all pages on your site. You need the path to these files for the next step. 

1. Reference [!DNL  VideoHeartbeat.min.js] on all site pages. Include ` VideoHeartbeat` for JavaScript by adding the following line of code in the ` &amp;lt;head&amp;gt;` or ` &amp;lt;body&amp;gt;` tag on each page. For example: 
   ```
   <script type="text/javascript" 
   src="http://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/VideoHeartbeat.min.js"></script>
   ```


1. To quickly verify that the ` VideoHeartbeat` library was successfully imported, instantiate the ` ADB.va.MediaHeartbeatConfig` class.

>[!NOTE]
>
>From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and [!DNL  VideoHeartbeat.min.js] can also be used with compatible module loaders. 



## Migrate to version 2.x in JavaScript {#section_wmk_pjf_r2b}

In version 2.x, all of the public methods are consolidated into the ` ADB.va.MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the ` ADB.va.MediaHeartbeatConfig` class. 

For detailed information about migrating from 1.x to 2.x, see [ VHL 1.x to 2.x Migration ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_mig_1x_to_2x.html). 
