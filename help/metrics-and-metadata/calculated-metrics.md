---
title: Streaming Media Calculated Metrics
description: Learn about Adobe Streaming Media calculated metrics and metric formulas.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Calculated metrics{#calculated-metrics}

Calculated metrics for streaming media are custom metrics that allow you to obtain targeted streaming media data such as average ad time spent or average ads per media stream.

For information about Adobe Analytics calculated metrics, see [Calculated and Advanced Calculated (Derived) Metrics](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=en) in the Adobe Analytics Components Guide.

>[!NOTE]
>
>These calculated metrics were introduced on 9/13/18.

|  Metric | Description | Formula |
|---|---|---|
|  Avg. Ads per Media Stream | Ad Starts per Media Starts | `Ad Starts / Media Starts` |
|  Avg. Chapters per Media Stream | Chapter Starts per Media Starts | `Chapter Start / Media Starts` |
|  Avg. Media Time Spent | Total Time Spent per Media Starts (HH:MM:SS) | `Media Time Spent / Media Starts` |
|  Avg. Content Time Spent | Content Time Spent per Content Starts (HH:MM:SS) | `Content Time Spent / Content Start` |
|  Avg. Ad Time Spent | Ad time spent per Ad Starts (HH:MM:SS) | `Ad Time Spent / Ad Start` |
|  Avg. Chapter Time Spent | Chapter Time Spent per Chapter Starts (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
|  Media Completion Rate | Rate of Content Completed vs Media Initiated (%) | `Content Completes/ Media Starts` |
|  Content Completion Rate | Rate of Content Completed vs Content Starts (%) | `Content Completes / Content Starts` |
|  Ad Completion Rate | Rate of Ad Completes vs Ad Starts (%) | `Ad Completes / Ad Starts` |
|  Chapter Completion Rate | Rate of Chapter Completes vs Chapter Starts (%) | `Chapter Completes / Chapter Starts` |
|  Drop Before Start Rate | Rate of Drops before Starts vs Media Starts (%) | `Drops before Starts / Media Starts` |
|  Content Pause Duration Rate | Rate of Total Pause Duration vs Content Time Spent (%) | `Total Pause Duration / Content Time Spent` |
|  Content Buffer Duration Rate | Rate of Total Buffer Duration vs Content Time Spent (% ) | `Total Buffer Duration / Content Time Spent` |
|  Content Time to Start Rate | Rate of Time to Start vs Content Time Spent (%) | `Time to Start / Content Time Spent` |
|  Ad Time Spent Rate | Rate of Ad Time Spent vs Content Time Spent (%) | `Ad Time Spent / Content Time Spent` |
