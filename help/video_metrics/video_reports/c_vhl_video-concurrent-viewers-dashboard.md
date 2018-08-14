---
description: The Video Concurrent Viewers dashboard displays concurrent viewers during one day. The data can be filtered by content, device type, or country.
keywords: Heartbeat Video;Video Analytics
seo-description: The Video Concurrent Viewers dashboard displays concurrent viewers during one day. The data can be filtered by content, device type, or country.
seo-title: Video Concurrent Viewers
solution: Analytics
title: Video Concurrent Viewers
topic: Developer and implementation
uuid: 64fb3b18-902b-4e04-9d4d-7871b414f129
index: y
internal: n
snippet: y
translate: y
---

# Video Concurrent Viewers


>[!TIP]
>
>No data will be displayed if the selected interval is not an entire day.

<a id="fig_CA2026CFC8224164878573CEF4F61DE6"></a> ![](assets/video-concurrent-viewers.png) 

## Report features {#section_11F8BCB98042490DAD0EA0B7EDA80569}

Here are some features of this report: 
* This is not in real time. It will have normal Adobe Analytics latency.
* The report covers a 24 hour time frame. The x-axis is time of day based on the report suite time zone.
* This shows concurrent viewers at minute granularity.
* There is a *Video Concurrent Viewers Report* that shows how many viewers are watching across all video content.
* There is a Concurrent Viewers report within *Video Details* report that shows how many viewers are watching one specific video.
* The report will only work across one day.
* The customer can look at historical concurrent viewer reports (limited to a single day).


## Limitations {#section_F159BC0213134FE4A997E52EECC7BB9D}

Here are some limitations for this report: 

* You cannot export the data, such as ReportBuilder.
* You cannot present the data in a table format.
* You cannot send a report via email.
* Even if you do not track ads, you have to re-enable video tracking and select the Video Ad module.
* This functionality will provide accurate data when using a Video Heartbeat Library that has Pause tracking capabilities.
