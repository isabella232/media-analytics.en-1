---
description: 
seo-description: 
seo-title: Measuring Video in Adobe Analytics
title: Measuring Video in Adobe Analytics
---

# Measuring Video in Adobe Analytics

>[!IMPORTANT]
>
>The video documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's Video Analytics SDK for heartbeat measurement, and does not include instructions around the legacy milestone video implementation. We encourage all customers to move towards adopting the latest Video Analytics SDK to capitalize on the improvements and expanded measurement. You can view the[benefits of transitioning to the SDK](video_overview.md#concept_ADA4B5C612D24280955BD0B7E79B4271/section_cnj_5st_p1b) below. While Adobe will continue to support the Milestone method of tracking videos, there will not be any planned updates, fixes or feature improvements. Please reach out to your Adobe Account Manager if you have any further questions.
## Overview {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Video (Video Analytics) is an add-on to the base Analytics offering that provides clients with robust video measurement for content, audio and advertisements. Video Analytics provides many benefits to customers to allow for real-time monitoring, detailed analysis, actionable insights and monetization opportunities. Video tracking is enabled through SDK integrations with the most commonly used video players. The latest SDKs have the additional capability of capturing audio related metrics.

Adobe Analytics for Video enables clients to track the full customer journey across their site, which includes video consumption, and these measures are easily integrated into Analytics reporting and other Experience Cloud products. Video measurement allows you to slice and dice your data into multiple dimensions and segments, capturing all of the metadata you need to do a full detailed analysis, and to attribute success criteria to fully viewed videos, average time spent and completed ads.

The video solution not only measures vital video delivery metrics related to QoS, such as dropped frames, time spent buffering, and average bitrate, but it can also be combined with your website or app data to visualize the flow of the customer and their interests to better be able to make recommendations and personalize their experiences through the Adobe Experience Cloud.

## Benefits {#section_7712BA90EAE64C118218D1C581EF68B7}

Some of the many benefits that Adobe's video solution provides include:

* **Timely analysis** - Make real-time, actionable decisions utilizing key video performance metrics (e.g., duration) across multiple channels. Video events are measured in **10-second** intervals to capture all activity as it occurs.
* **Drive engagement** - Fully engage users through fewer buffering events and by understanding where and when ads should display within video content to provide a smooth, less intrusive viewing experience that brings users back and delivers repeat visits.
* **Holistic picture** - Combine multiple data points across all of your content distributors to get a full view of all your video activity, and measure engagement and views across all possible channels through [](federated-analytics.md).
* **Increased granularity** - Evaluate viewing behavior at the most granular level, including individual visitor time of day, concurrent viewers by minute, and average duration the content was viewed.
* **Precise measurement** - Measure across the multiple devices used for video consumption, including OTT, smartphone, tablet, desktop, and more, to monitor user engagement patterns and habits.
* **Segmentation** - Apply classifications to your players, devices, genres, chapters, and shows to see how each has an impact on your overall views and customer engagement with content, audio, ads, and combined.
<!-- <p>Here is how video and video ad data flow into Adobe: </p> 
<p> 
 <fig id="fig_5A574F71C807481B8E1D66335CB836F3"> 
  <img href="graphics/how_aa_video_works.png" id="image_D3A97A67B8AF4055B6BF72F92190E18B" /> 
 </fig> </p> -->
## Heartbeat versus Milestone Benefits {#section_cnj_5st_p1b}

Adobe Analytics for Video is able to be measured through two means: the legacy Milestone method and the current Heartbeats method. The Heartbeats method is the preferred method of measurement and we encourage all clients to move to this version if they haven’t already, to take advantage of the benefits described below.

The legacy Milestone method is based on individual server calls to the Analytics server, for video starts, quartiles, duration, and completes. The Heartbeats method provides a more robust video tracking solution that measures video in 10 second intervals to provide enhanced, standardized video metrics. In addition, Adobe has derived learnings from our Milestone method to provide a smoother, streamlined implementation process through the Video Analytics SDK utilized by heartbeats.

Some of the many benefits of the Heartbeats method include:

* **Streamlined implementation process** - Map variables more easily through your player API and validate implementations through the Adobe Debug Tool to ensure all the necessary variables are tracked accurately.
* **Automatic Adobe Experience Cloud Integration** - Take advantage of the automatic integration with the Adobe Experience Cloud through the Marketing Cloud ID, segment your video audiences, target them, and make video recommendations based on user preferences.
* **Shared video data through Federated Analytics** - Capitalize on our industry-first video sharing capabilities, to evaluate data holistically across all of your video distribution partners—operators, programmers, and distributors.
* **Partnerships with Certified Ratings Partners** - Adobe partners with audience ratings partner Nielsen to provide neutral census third party measurement to allow for trusted, certified video ratings.
* **Standardized solution across all platforms** - Enable consistent, standardized variables across all of your videos and platforms to allow for a more efficient cross-campaign, device and vendor comparison.
<table id="table_mmx_f5t_p1b"> 
 <title><b>Comparison Chart</b></title> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" /> 
  <colspec colnum="2" colname="col2" /> 
  <colspec colnum="3" colname="col3" /> 
  <thead> 
   <tr> 
    <th class="entry"></th> 
    <th class="entry"><b>Video Analytics - Milestone</b> </th> 
    <th class="entry"><b>Video Analytics - Heartbeats</b> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td><b>Video Events</b> </td> 
    <td>High-level Standard Events </td> 
    <td>Detailed and Custom Events every 10s </td> 
   </tr> 
   <tr> 
    <td><b>Metrics and Dimensions</b> </td> 
    <td>Variances among Vendors, Non-Standardized Metrics and Dimensions </td> 
    <td>Clear, Standardized Metrics, Dimensions, and Benchmarks across Vendors </td> 
   </tr> 
   <tr> 
    <td><b>Integrations w/ Adobe Products</b> </td> 
    <td>Individual Sessions w/ some Mappings and Integrations </td> 
    <td>Stitched Marketing Cloud ID linked to full Adobe Experience Cloud for easier cross-analysis </td> 
   </tr> 
   <tr> 
    <td><b>Pricing</b> </td> 
    <td>Tracked and billed against each server call </td> 
    <td>Transparent tracking by video stream (single) </td> 
   </tr> 
   <tr> 
    <td><b>Implementation and Support</b> </td> 
    <td>Longer integrations with limited support on legacy versions &amp; no upgrades </td> 
    <td>Streamlined configuration with ongoing updates and improvements </td> 
   </tr> 
   <tr> 
    <td><b>Partner Sharing</b> </td> 
    <td>N/A </td> 
    <td>Federated Analytics and Certified Metrics </td> 
   </tr> 
   <tr> 
    <td><b>Advanced Tracking</b> </td> 
    <td>N/A </td> 
    <td>Error Recovery Tracking and Concurrent Viewers </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>



## Devices Supported {#section_lkm_l5t_p1b}

Adobe Analytics for Video has evolved with the industry to provide strong data collection tools to ensure each video stream is collected and reported across all meaningful devices. Our Video Analytics SDK is developed for all of the most utilized devices, including:

* iOS and Android smartphones and tablets
* OTT devices for ROKU, AppleTV, FireTV, and Android TV
* JavaScript Browser for Desktop and Laptop
The SDK’s are routinely updated when new versions of devices are released, and you can use these SDKs to integrate with most of the largest video players today, including Brightcove and Ooyala.

<table id="table_znx_dvt_p1b"> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" align="left" colwidth="1*" /> 
  <colspec colnum="2" colname="col2" align="center" colwidth="1.08*" /> 
  <colspec colnum="3" colname="col3" align="center" colwidth="1.19*" /> 
  <tbody> 
   <tr> 
    <td></td> 
    <td align="center"><b>Adobe Video SDK</b> </td> 
    <td align="center"><b>Video Analytics Collection API</b> </td> 
   </tr> 
   <tr> 
    <td><b>JavaScript Browser</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td align="center"></td> 
   </tr> 
   <tr> 
    <td><b>iOS Devices</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td align="center"></td> 
   </tr> 
   <tr> 
    <td><b>Android Devices</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td align="center"></td> 
   </tr> 
   <tr> 
    <td><b>Windows </b> </td> 
    <td align="center"></td> 
    <td align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td><b>Blackberry</b> </td> 
    <td align="center"></td> 
    <td align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td><b>Apple TV (new/legacy)</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td align="center"></td> 
   </tr> 
   <tr> 
    <td><b>ROKU</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td></td> 
   </tr> 
   <tr> 
    <td><b>OSX</b> </td> 
    <td align="center"></td> 
    <td align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td><b>Fire TV</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td></td> 
   </tr> 
   <tr> 
    <td><b>Android TV</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td></td> 
   </tr> 
   <tr> 
    <td><b>Chromecast</b> </td> 
    <td align="center"><b>✔</b> </td> 
    <td></td> 
   </tr> 
   <tr> 
    <td><b>Xbox 1</b> </td> 
    <td align="center"></td> 
    <td align="center"><b>✔</b> </td> 
   </tr> 
   <tr> 
    <td><b>Sony PS3/PS4</b> </td> 
    <td align="center"></td> 
    <td align="center"><b>✔</b> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

The table below provides a list of the devices that are currently supported through our SDK implementation or Analytics API. To download the most recent version of the SDK, visit[](c_vhl_download-sdks.md). If there is a device that is not listed which you are seeking measurement against, please contact customer care or your solution consultant for the status of that device.
