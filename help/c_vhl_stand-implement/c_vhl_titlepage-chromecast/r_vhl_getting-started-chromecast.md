---
description: You can use this information to help you get starting with the Chromecast SDK for Experience Cloud Solutions. This section assumes that you have configured a report suite through Adobe Mobile Services to collect app data.
seo-description: You can use this information to help you get starting with the Chromecast SDK for Experience Cloud Solutions. This section assumes that you have configured a report suite through Adobe Mobile Services to collect app data.
seo-title: Getting started on Chromecast
title: Getting started on Chromecast
uuid: 9556dc42-cb24-46d0-9435-3a3528ba4290
index: y
internal: n
snippet: y
translate: y
---

# Getting started on Chromecast


<a id="section_kkf_4d2_r2b"></a>


* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_A5E180C4D4314B63A5863B45DE952A05)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_DC5B6C26CD124C5087EA7BC7A67F7E16)




Adobe Mobile Services is the primary reporting interface for mobile app analytics and targeting. After you complete the configuration steps, you can download a configuration file that is preconfigured with your data collection server, report suite, and many other settings. 

## Prerequisites {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This information is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.



Before you start implementing the Android SDK, ensure that you have completed the following tasks: 

* **General VA Prerequisites -** [](../../video_get_started/c_vhl_prereqs.md)
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.


## Download and set up the SDK {#section_DC5B6C26CD124C5087EA7BC7A67F7E16}


1. [](../../c_vhl_stand-implement/c_vhl_download-sdks.md)
1. The ` [ AdobeMobileLibrary-Chromecast-2.0.2.zip ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases/download/chromecast-v2.0.2/AdobeMobileLibrary-Chromecast-2.0.2.zip)` download file consists of the following software components: 
    * ` adbmobile-chromecast.min.js`: This library file will be included in your Chromecast app source folder. 

    * ` ADBMobileConfig` config This SDK configuration file is customized for your app. 


1. Add the library file to your [!DNL  index.html] file, and create the ` ADBMobileConfig` global variable as follows: 
   ```
   <script> 
   var ADBMobileConfig = { 
       "marketingCloud": { 
           "org": "06074954519E38710A490D16@AdobeOrg" 
       }, 
       "target": { 
           "clientCode": "", 
           "timeout": 5 
       }, 
       "audienceManager": { 
           "server": "mobileservices.demdex.net" 
       }, 
       "analytics": { 
           "rsids": "mobile1figueroa-dev", 
           "server": "obumobile1.sc.omtrdc.net", 
           "ssl": false, 
           "offlineEnabled": true, 
           "charset": "UTF-8", 
           "lifecycleTimeout": 300, 
           "privacyDefault": "optedin", 
           "batchLimit": 0, 
           "timezone": "MDT", 
           "timezoneOffset": -360, 
           "referrerTimeout": 0, 
           "poi": [] 
       } 
   }; 
   </script> 
   <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script> 
   
   ```



