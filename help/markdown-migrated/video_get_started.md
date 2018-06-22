---
description: 
seo-description: 
seo-title: Getting Started
title: Getting Started
---

# Getting Started

Before you begin your Adobe Analytics for Video implementation you have some early decisions to make, regarding which implementation scenario makes the most sense for your situation. The information in the following sections will help you determine how best to proceed:


* **Video Analytics** - Implement one of the Video Analytics implementation paths using the latest Video Analytics SDKs (recommended)
* **Milestone** - Implement with Milestone (the older Adobe tracking implementation)
* **Data Insertion APIs** - Implement without using Video Analytics SDKs (video tracking with Data Insertion APIs).

## Video Analytics Implementation Paths {#section_vfg_dbz_kbb}

Video Analytics (using the Heartbeats model) is Adobe’s standardized video solution. It has replaced Adobe's older Milestone model.

For each of the paths described below, customers will need to contact their Sales Representative/Account Manager to sign a new Sales Order as Video Analytics has a unique SKU and changes from a pricing model based on server calls to a model based on video streams.


* **Video Analytics Path** - The Video Analytics path features the Video Analytics SDK, which can be used across any video player, including customer and/or OVP players such as Brightcove, Ooyala, thePlatform, and so on.
  >[!IMPORTANT]
  >
  >To use Video Analytics, customers also need to use Adobe Analytics. If Video Analytics is your intended path, see[Standard Implementation](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_stand-implement.html).
  
* **Analytics and Ratings Path** - Adobe has partnered with Nielsen so that customers can opt-in to share data, collected by Adobe SDKs/tags, directly with Nielsen to provide the data that fuels their ratings solutions. For the Nielsen partnership, Adobe created a Combo SDK that comprises the Nielsen and Adobe Heartbeat SDKs. With one implementation, customers can capture data for analytics and ratings (Nielsen’s Digital Content Ratings). To leverage this partnership, a customer must complete the following steps:
  
    1. Sign an Adobe Sales Order for the Video Analytics SKU, based on streams.
    1. Sign an Adobe Addendum in which the customer gives permission to Adobe to share data directly with Nielsen.
    1. Contact your Nielsen Account team and complete paperwork from Nielsen to leverage Digital Content Ratings (DCR).
    1. After completing steps 1-3, contact your Adobe Account Manager to get the location where you can download the Combo SDK.
       
       >[!NOTE]
       >
       >The Combo SDK is not available on GitHub.
       
       
  
  For more information about the partnership and how to implement this path, see [Digital Content Ratings, powered by Adobe](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/nielsen/).
  
  With this partnership, to ensure proper implementation and to guarantee quality data based on agreed upon standardized metrics, Adobe will certify your builds before you release them to production.
  
  >[!NOTE] {type="note"}
  >
  >To send data to our ratings partners, customers need to contact their Sales Representative/Account Manager to purchase Adobe Certifications.
  
* **Adobe Primetime Path** - Adobe Primetime is an Adobe Marketing Cloud solution that helps content programmers and distributors monetize video on every connected screen. Primetime eliminates the complexity of reaching, monetizing, and activating global audiences across devices by providing a modular platform for video publishing, advertising, personalization, and analytics. Additionally, Primetime offers solutions and value around the following:
  
    * Support for accurately measuring Linear and VOD content types.
    * Support for measuring ad breaks with (or without) dynamic ad insertion.
    * TVSDK's seamless ad insertion model allows for analytics that directly measures the ad playback, which increases accuracy.
    * Robust set of events and metadata to ensure accuracy across QoS buffering or mobile connectivity interruptions issues and end-user interactions such as seeking, pausing, and backgrounding on mobile.
    * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
  
  TVSDK is already integrated with the Video Analtyics (Heartbeats) SDK, which makes implementation much easier and faster across every supported platform. Primetime also supports the partnership with Nielsen. To leverage Primetime, follow the same guidelines and prerequisites found in [Video Analytics](c_vhl_va-path.md#concept_928146A7583A482187BB3D5FEAC205B6) along with the following docs for your platform(s):
  
  
    * [Video Analytics in TVSDK 1.4 for Android](http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#Video_analytics)
    * [Video Analytics in TVSDK 2.4 for Browser TVSDK](http://help.adobe.com/en_US/primetime/psdk/browser/2.4/index.html#Video_analytics)
    * [Video Analytics in TVDSK 1.4 for Desktop HLS](http://help.adobe.com/en_US/primetime/psdk/dhls/1.4/index.html#Video_analytics)
    * [Video Analytics in TVDSK 2.3 for Desktop HLS](http://help.adobe.com/en_US/primetime/psdk/dhls/2.3/index.html#Video_analytics)
    * [Video Analytics in TVSDK 1.4 for iOS](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#Video_analytics)
  
  You should also contact your Sales Representative/Account Manger to discuss what you need to do to purchase TVSDK.
  
  

## Video Milestone Implementation (Old) {#section_ulc_bcz_kbb}

The Video Milestone measurement model is the previous method Adobe supported to track video. This has since been replaced by the Video Analytics (Heartbeats) model.

The Milestone model allows a completely custom implementation where customers can decide when and how frequently to send in server calls during playback. It was called "Milestone" because the most common implementations sent in server calls at the start, 25%, 50%, 75%, and at the completion of the video. The solution uses your own custom eVars and events to track video by using Adobe's Media Module. The Heartbeats solution was designed to build upon some of the limitations of Milestones, specifically around providing more granularity and accuracy around engagement and to provide a more standardized measurement solution across our entire customer base.

<table id="table_1B3C2797AA6F4DBF90166485CD3353C2"> 
 <title>Feature Differences Between Milestone and Heartbeat Video Measurement</title> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" align="center" class="entry">Feature</th> 
    <th colname="col2" align="center" class="entry">Milestone</th> 
    <th colname="col3" align="center" class="entry">Heartbeat</th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <p>Quartile tracking</p> </td> 
    <td colname="col2" align="center" valign="middle"><b>✔</b> </td> 
    <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Real-Time Reporting</p> </td> 
    <td colname="col2" align="center" valign="middle"><b>✔</b> </td> 
    <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>10 second time spent granularity</p> </td> 
    <td colname="col2" align="center" valign="middle"></td> 
    <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Standardized data and benchmarking</p> </td> 
    <td colname="col2" align="center" valign="middle"></td> 
    <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Chapter tracking</p> </td> 
    <td colname="col2" align="center" valign="middle"></td> 
    <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Pricing based on streams</p> </td> 
    <td colname="col2" align="center"></td> 
    <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Player Mapping implementation model</p> </td> 
    <td colname="col2" align="center" valign="middle"><b>✔</b> </td> 
    <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Required variables ONLY in base objects</p> </td> 
    <td colname="col2" align="center"></td> 
    <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Streamlined configuration</p> </td> 
    <td colname="col2" align="center"></td> 
    <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Error state recovery</p> </td> 
    <td colname="col2" align="center"></td> 
    <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>Video ad tracking included in solution</p> </td> 
    <td colname="col2" align="center"></td> 
    <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

The Milestone model can be used at the same time as the Heartbeats model in a specific report suite, but both solutions should not be used at the same time in the same player. Data captured from both models can live and be reported on in the same report suite. This will allow you to gradually migrate to the Heartbeats model without having to update everything at the same time.

For more information, see the [Video Milestone documentation](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).

## Video Data Insertion APIs {#section_rfb_dcz_kbb}

The Data Insertion API is a way to track video playback on devices and platforms where Adobe does not currently have a Video Heartbeats SDK. HTTP POSTs and HTTP GETs enable a server-side method to collect data.

When using the API, during playback you will determine which events and metadata that you want to send to Adobe with server calls. However, these API calls are completely independent of Adobe's Video Analytics solution (Heartbeats). This means that you cannot leverage Adobe's solution/reserved variables to standardize your video implementation, nor will Adobe send any of this data to our ratings partners.

For more information about the Data Insertion API, see [Data Insertion: Overview](https://marketing.adobe.com/developer/documentation/data-insertion/c-data-insertion-api).

