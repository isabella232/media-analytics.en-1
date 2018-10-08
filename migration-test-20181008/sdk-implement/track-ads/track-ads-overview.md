---
description: null
seo-description: null
seo-title: Overview
title: Overview
uuid: 5bf4f25e-0019-4718-ae08-5334a199f07b
index: y
internal: n
snippet: y
translate: y
---

# Overview

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using the 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

<a id="section_D4DE5643337B444D8CF2EE8C6C0AF0BE"></a>

Ad playback includes tracking ad breaks, ad starts, ad completes, and ad skips. You can use the media player's API to identify key player events and to populate the required and optional ad variables.

Here are the key elements you use to track ad playback:

**On ad break start, including pre-roll:**

* Create an `adBreak` object instance for the ad break. For example, `adBreakObject`. 

* Call `trackEvent` for the ad break start with your `adBreakObject`.

**On every ad asset start:**

* Create an ad object instance for the ad asset. For example, `adObject`. 
* Populate the ad metadata, `adCustomMetadata`. 
* Call `trackEvent` for the ad start.

**On every ad asset complete**

* Call `trackEvent` for the ad complete.

**On ad skip**

* Call `trackEvent` for the ad skip.

**On ad break complete**

* Call `trackEvent` for the ad break complete.

## Implement {#section_83E0F9406A7743E3B57405D4CDA66F68}

**Ad tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `AdBreakStart`  | Constant for tracking AdBreak Start event  |
|  `AdBreakComplete`  | Constant for tracking AdBreak Complete event  |
|  `AdStart`  | Constant for tracking Ad Start event  |
|  `AdComplete`  | Constant for tracking Ad Complete event  |
|  `AdSkip`  | Constant for tracking Ad Skip event  |

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information. 

   ** `AdBreakObject` reference:** 

<table id="table_AC3C9A0B8F544DE9BB4A80D22457438F"> 
 <thead> 
  <tr> 
   <th colname="col1" align="center" class="entry"> Variable Name </th> 
   <th colname="col2" align="center" class="entry"> Description </th> 
   <th colname="col3" align="center" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col2"> <p>Ad break name such as pre-roll, mid-roll, and post-roll. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> position </span> </td> 
   <td colname="col2"> <p>The number position of the ad break starting with 1. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> startTime </span> </td> 
   <td colname="col2"> <p>Playhead value at the start of the ad break. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
 </tbody> 
</table>

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break. 

1. Identify when the ad asset starts and create an `AdObject` instance using the ad information. 

   `AdObject` reference: 

<table id="table_2B208589ABAA4CF2A476934578D3BEF3"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Variable Name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col2"> <p>Friendly name of the ad asset. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adId </span> </td> 
   <td colname="col2"> <p>Unique identified for the ad asset. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> position </span> </td> 
   <td colname="col2"> <p>The number position of the asset in the ad break, starting with 1. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> length </span> </td> 
   <td colname="col2"> <p>Ad asset length </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
 </tbody> 
</table>

1. Optionally attach standard and/or ad metadata to the tracking session through context data variables.

    * **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform.
    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad asset.

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback. 

   Include a reference to your custom metadata variable (or an empty object) as the third parameter in the event call.

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event. 

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event. 
1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again. 
1. When the ad break is complete, use the `AdBreakComplete` event to track:

The following sample code utilizes the JavaScript 2.x SDK for an HTML5 video player. 

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 

```

## Validate {#section_5F1783F5FE2644F1B94B0101F73D57EB}

**Ad Start**

On start of an individual ad playback, three key calls are sent in the following order:

1. Video ad analytics start**&#42;**
1. Heartbeat ad start**&#42;**
1. Heartbeat analytics start

**&#42;**These calls contain additional metadata variables for both custom and standard.

**Ad Play**

During ad playback, Heartbeat ad play calls are sent to the Heartbeat server every second.

**Ad Complete**

At the 100% point of an ad, a Heartbeat ad complete call will be sent.

**Ad Skip**

When an ad is skipped, no events are sent, so the tracking calls will not include the ad information.

>[!TIP]
>
>No unique calls are sent on ad break start and ad break complete.

