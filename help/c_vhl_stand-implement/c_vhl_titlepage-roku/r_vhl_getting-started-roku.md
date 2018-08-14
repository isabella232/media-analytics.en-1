---
description: After you download the Roku SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes and so on.
seo-description: After you download the Roku SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes and so on.
seo-title: Getting started on Roku
title: Getting started on Roku
uuid: 71a5a0ff-5bc0-4baf-b024-482b1bb93a80
index: y
internal: n
snippet: y
translate: y
---

# Getting started on Roku


<a id="section_kkf_4d2_r2b"></a>


* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_A5E180C4D4314B63A5863B45DE952A05)
* [](#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD/section_DC5B6C26CD124C5087EA7BC7A67F7E16)




## Prerequisites {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This information is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.



Before you start implementing the SDK, ensure that you have completed the following tasks: 

* **General VA Prerequisites -** [](../../video_get_started/c_vhl_prereqs.md)
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.


## Download and setup the SDK {#section_DC5B6C26CD124C5087EA7BC7A67F7E16}


1. [](../../c_vhl_stand-implement/c_vhl_download-sdks.md)
1. The ` AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components: 
    * ` adbmobile.brs`: This library file will be included in your Roku app source folder. 

    * ` ADBMobileConfig.json` This SDK configuration file is customized for your app. 



1. Add the library file and JSON config file to your project source.

