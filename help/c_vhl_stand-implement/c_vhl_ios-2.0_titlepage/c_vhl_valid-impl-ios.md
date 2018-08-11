---
description: To validate your Media Heartbeat implementation it will be required to use a HTTP Proxy tool to view the HTTP / HTTPS traffic between the Application and Heartbeats/Adobe Analytics.
seo-description: To validate your Media Heartbeat implementation it will be required to use a HTTP Proxy tool to view the HTTP / HTTPS traffic between the Application and Heartbeats/Adobe Analytics.
seo-title: Validate implementations
title: Validate implementations
uuid: 0804bfe3-f7a9-4c70-8e88-dde17f8f48a1
index: y
internal: n
snippet: y
translate: y
---

# Validate implementations

HTTP calls for video analytics tracking will be sent to 2 different tracking servers: 


* **Adobe Analytics: **Adobe Analytics hits are used to mark the initiate of a Video/Ad/Chapter. Tracking server example: ` &amp;lt;visitornamespace&amp;gt;.sc.omtrdc.net`
* **Heartbeats platform: **Heartbeat platform hits (also known as *heartbeats*) are sent throughout the video tracking session at 10 seconds intervals (out of band events might be sent outside of the 10 seconds cycle). Tracking server example: ` &amp;lt;visitornamespace&amp;gt;.hb.omtrdc.net`


All of the different parameters sent to the Adobe Analytics and Heartbeats tracking servers are presented here: [ Metrics and Metadata ](https://marketing-stage.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_metrics-and-metadata.html).

## Adobe Debug {#section_dyc_gx1_jbb}

Optionally, you can debug payloads (Heartbeat and Adobe Analytics) going out of Video Heartbeat Library using the Adobe Debug tool. This is a freely available tool from Adobe for Video Heartbeat customers. 

To use Adobe Debug, you need to contact your Adobe representative for the initial setup and registration. After you gain access to Adobe Debug, go to [ Adobe Debug help ](https://debug.adobe.com/login?next=/#/help/) for information. 
