---
description: null
keywords: Heartbeat Video;Video Analytics
seo-description: null
seo-title: Experience Cloud Enablement
solution: Analytics
title: Experience Cloud Enablement
topic: Developer and implementation
uuid: a9a5807a-cdab-48c5-96c7-91d7482cb6e4
index: y
internal: n
snippet: y
translate: y
---

# Experience Cloud Enablement


## Experience Cloud ID Overview {#section_206234AED0334DD6BE9D2C5BA39B900E}

As part of the requirements to implement the Video Heartbeat SDK, you need to implement the Experience Cloud ID Service (formerly known as Visitor ID Service).
The Experience Cloud ID service enables the common identification framework for the Experience Cloud Core Services, solutions, and customer attributes and audiences in the People core service. It works by assigning a unique, persistent ID to a site visitor. When your organization implements the ID service, this ID lets you identify the same site visitor and their data in different Experience Cloud solutions.
<a id="fig_E7648D1E230E4AA588C80C9092B662EA"></a> ![](graphics/mc_id_service_graphic.png) 
The ID service can also replace the different solution-specific IDs (for example, Analytics AID). Through the [Customer IDs and Authentication States](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html) functionality, the ID service lets you pass in your own customer IDs to the Experience Cloud. Keep in mind, however, that the ID service only works with the solutions to which you have already subscribed. If you are not signed up for access to other products, the ID service does not provide the access. 
Going forward, the ID service is an integral component of many current and future Experience Cloud features, enhancements, and services. Currently, the ID service supports [Analytics](http://www.adobe.com/marketing-cloud/web-analytics.html), [Audience Manager](http://www.adobe.com/marketing-cloud/data-management-platform.html), and [Target](http://www.adobe.com/marketing-cloud/testing-targeting.html). 

>[!IMPORTANT]
>
>To participate in the Adobe Experience Cloud Device Co-op, the Experience Cloud ID service required.

If you have not implemented the ID service, now is the time to start considering a migration strategy. For more information about the importance and role of the ID service, see [Why the Experience Cloud ID Service Should be on Your Radar](http://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/). 

>[!IMPORTANT]
>
>In the absence of any user ID information present on the video specific calls the default analytics[Fallback ID Methods](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_fallback.html) will apply. 

For more information about the Experience Cloud ID, see [Overview](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html). 

## Implementation Guides {#section_A64A8E2C7AF64AC48287B518590F8B0E}

For more information about implementing the Experience Cloud ID Service, see [Experience Cloud ID Service](https://marketing.adobe.com/resources/help/en_US/mcvid/). 
