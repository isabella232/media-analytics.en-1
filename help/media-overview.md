---
seo-title: Measuring audio and video in Adobe Analytics
title: Measuring audio and video in Adobe Analytics

---

# Measuring audio and video in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. It does not include instructions around the legacy Milestone video implementation. We encourage all customers to move towards adopting one or both of the two latest media tracking solutions, in order to capitalize on improvements and expanded measurement. You can view the [benefits of transitioning to the latest solutions](media-overview.md#heartbeat-versus-milestone-benefits) below. While we will continue to support the Milestone method of tracking videos, there will not be any planned updates, fixes, or feature improvements. Please reach out to your Adobe Account Manager if you have any further questions.

## Overview {#overview}

Adobe Analytics for Media (also referred to as Media Analytics) is an add-on to the base Analytics offering that provides clients with robust media measurement for content, audio and advertisements. Media Analytics provides many benefits to customers to allow for real-time monitoring, detailed analysis, actionable insights and monetization opportunities.

Media tracking is enabled through either of the following:

* **Media SDK -** Integrates with the most commonly used media players. 
* **Media Collection API -** (RESTful API) Integrates with players for which there is no SDK support (or with players for which no SDK integration is desired).

Adobe Analytics for Media enables clients to track the full customer journey across their site, which includes media consumption, and these measures are easily integrated into Analytics reporting and other Experience Cloud products. Media measurement allows you to slice and dice your data into multiple dimensions and segments, capturing all of the metadata you need to do a full detailed analysis, and to attribute success criteria to fully consumed media, average time spent, and completed ads.

The media solutions not only measure vital delivery metrics related to QoS, such as dropped frames, time spent buffering, and average bitrate. They can also be combined with your website or app data to visualize the flow of the customer and their interests, to better be able to make recommendations and personalize their experiences through the Adobe Experience Cloud.

## Benefits {#benefits}

Some of the many benefits that Adobe's media measurement solutions provide include:

* **Timely analysis -** Make real-time, actionable decisions utilizing key performance metrics (e.g., duration) across multiple channels. Main content events are measured in **10-second** intervals to capture all activity as it occurs. Ad tracking events occur at **1-second** intervals.
* **Drive engagement -** Fully engage users through fewer buffering events and by understanding where and when ads should play within content to provide a smooth, less intrusive experience that brings users back and delivers repeat visits. 
* **Holistic picture -** Combine multiple data points across all of your content distributors to get a full view of all your media activity, and measure engagement and views/listens across all possible channels through the [Federated Analytics](/help/federated-analytics.md) feature.
* **Increased granularity -** Evaluate viewing behavior at the most granular level, including individual visitor time of day, concurrent viewers/listeners by minute, and average duration the content was consumed. 
* **Precise measurement -** Measure across the multiple devices used for media consumption, including OTT, smartphone, tablet, desktop, and more, to monitor user engagement patterns and habits. 
* **Segmentation -** Apply classifications to your players, devices, genres, chapters, and shows to see how each has an impact on your overall views/listens and customer engagement with content, audio, ads, and combined.

## Heartbeat versus Milestone benefits {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media is able to be measured through two means: the legacy Milestone method (video only) and the current Heartbeats method (audio and video, featured in both the Media SDK and the Media Collection API). The Heartbeats method is the preferred method of measurement and we encourage all clients to move to this version if they haven’t already, to take advantage of the benefits described below.

The legacy Milestone method is based on individual server calls to the Analytics server, for video starts, quartiles, duration, and completes. The Heartbeats method provides a more robust media tracking solution that measures main content in 10-second intervals to provide enhanced, standardized metrics. In addition, Adobe has derived learnings from our Milestone method to provide a smoother, streamlined implementation process through either the Media SDK or Media Collection API utilized by Heartbeats.

Some of the many benefits of the Heartbeats method include:

* **Streamlined implementation process -** Map variables more easily through your player API and validate implementations through the Adobe Debug Tool to ensure all necessary variables are tracked accurately. 
* **Automatic Adobe Experience Cloud Integration** - Take advantage of the automatic integration with the Adobe Experience Cloud through the Experience Cloud ID, segment your media audiences, target them, and make media recommendations based on user preferences. 
* **Shared data through Federated Analytics -** Capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. 
* **Standardized solution across all platforms -** Enable consistent, standardized variables across all of your media and platforms to allow for a more efficient cross-campaign, device and vendor comparison.
* **Downloaded content tracking -** Track media content (video and audio) that is downloaded and played on a device regardless of its connectivity. 

### Comparison Chart

|  | Video Analytics - Milestone | Media Analytics - Heartbeats |
|---|---|---|
| **Media Events** | High-level Standard Events  | Detailed and Custom Events every 10s for main content, every 1s for ads |
| **Metrics and Dimensions** | Variances among Vendors, Non-Standardized Metrics and Dimensions  | Clear, Standardized Metrics, Dimensions, and Benchmarks across Vendors  |
| **Integrations w/ Adobe Products** | Individual Sessions w/ some Mappings and Integrations  | Stitched Experience Cloud ID linked to full Adobe Experience Cloud for easier cross-analysis  |
| **Pricing** | Tracked and billed against each server call  | Transparent tracking by media stream (single)  |
| **Implementation and Support** | Longer integrations with limited support on legacy versions & no upgrades  | Streamlined configuration with ongoing updates and improvements  |
| **Partner Sharing** | N/A  | Federated Analytics and Certified Metrics  |
| **Advanced Tracking** | N/A  | Error Recovery Tracking and Concurrent Viewers  |

## Devices supported {#devices-supported}

Adobe Analytics for Media has evolved with the industry to provide strong data collection tools to ensure each media stream is collected and reported across all meaningful devices. Our Media SDK is developed for all of the most utilized devices, including:

* iOS and Android smartphones and tablets 
* OTT devices for ROKU, AppleTV, FireTV, and Android TV 
* JavaScript Browser for Desktop and Laptop

The SDKs are routinely updated when new versions of devices are released, and you can use these SDKs to integrate with most of the largest media players today, including Brightcove and Ooyala.

For devices or platforms that do not currently have SDK support (or even if they do), you can implement the Media Collection API, through which you make RESTful API calls directly from the device/platform to the Media Analytics backend. 

The table below provides a list of the devices that are currently supported through our Media SDK implementation and Media Collection API implementation. To download the most recent version of the SDK, see [Download SDKs.](sdk-implement/download-sdks.md) If there is a device that is not listed which you are seeking measurement against, please contact customer care or your solution consultant for the status of that device. 

| &nbsp;&nbsp;&nbsp;&nbsp; | Media SDK | Media Collection API |
|---|:---:|:---:|
| **JavaScript Browser**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **iOS Devices**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **Android Devices**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **Unified Windows Platforms (UWP)**  | | ![](assets/icon-blue-check.png) |
| **Blackberry**  | | ![](assets/icon-blue-check.png) |
| **Apple TV (new/legacy)**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **ROKU (JS)**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **ROKU (Native app)**  | | ![](assets/icon-blue-check.png) |
| **OSX**  | | ![](assets/icon-blue-check.png) |
| **Fire TV**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **Android TV**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **Chromecast**  | ![](assets/icon-blue-check.png)  | ![](assets/icon-blue-check.png) |
| **Xbox One/360**  | | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4**  | | ![](assets/icon-blue-check.png) |
| **(Other/New Connected Devices)**  | | ![](assets/icon-blue-check.png) |

For Media SDK, also see [Minimum Platform Version Support](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**TLS Notice --** Adobe has security compliance standards that require the end-of-life of older security protocols. To continue to meet the evolving security protocol standards, Adobe is moving toward the use of TLS 1.2, in order to have the most up-to-date and secure version in use. From February 20th, 2019, Adobe will support only TLS 1.1 or later. With this change, Adobe will no longer collect data from end users with older devices or web browsers deploying TLS 1.0. Migrating to TLS 1.2 provides improved security. It is important that you go through the specifics and plan out the changes for a smooth transition.

>[!NOTE]
>
>TLS is currently the most-widely deployed security protocol used in web browsers and other applications that require data to be securely exchanged over a network. 
