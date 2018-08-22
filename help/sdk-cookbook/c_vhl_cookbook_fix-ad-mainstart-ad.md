---
description: null
seo-description: null
seo-title: Resolving main play appearing between ads
title: Resolving main play appearing between ads
uuid: 9f3461a6-55a9-4f9d-a811-69d400c03797
index: y
internal: n
snippet: y
translate: y
---

# Resolving main:play appearing between ads

**PROBLEM**

In some ad tracking scenarios, you could encounter ` main:play` calls occurring unexpectedly between the end of one ad and the start of the next ad. If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Video Analytics (VA) SDK will fall back to sending ` main:play` calls. If this fallback to ` main:play` occurs during a pre-roll ad break, the content start metric may be set early.

A gap between ads such as described above is interpreted by the VA SDK as main content, because there is no overlap there with any ad content. The VA SDK does not have any ad information set on it, and the player is in the playing state. If there is no Ad information, and the player state is playing, then the VA SDK credits the duration of the gap towards main content by default. It cannot credit playback duration toward null ad information.

**IDENTIFICATION**

While using Adobe Debug or a network packet sniffer such as Charles, if you see the following heartbeat calls in this order during a pre-roll ad break:


* Session Start: ` s:event:type=start &amp; s:asset:type=main`
* Ad Start: ` s:event:type=start &amp; s:asset:type=ad`
* Ad Play: ` s:event:type=play &amp; s:asset:type=ad`
* Ad Complete: ` s:event:type=complete &amp; s:asset:type=ad`
* Main Content Play: ` s:event:type=play &amp; s:asset:type=main` **(unexpected)**
* Ad Start: ` s:event:type=start &amp; s:asset:type=ad`
* Ad Play: ` s:event:type=play &amp; s:asset:type=ad`
* Ad Complete: ` s:event:type=complete &amp; s:asset:type=ad`
* Main Content Play: ` s:event:type=play &amp; s:asset:type=main` **(expected)**


**RESOLUTION**

***Delay triggering the Ad Complete call.***

Handle the gap from within the player by calling ` trackEvent:AdComplete` late for the first ad, followed immediately by ` trackEvent:AdStart` for the second ad. The app should hold off on calling the ` AdComplete` event after the first ad finishes. Make sure you call ` trackEvent:AdComplete` for the last ad in the ad break. If the player can identify that the current ad asset is the final one in the ad break, call ` trackEvent:AdComplete` immediately. This resolution will result in less than 1 second of additional ad time spent being attributed to the preceding ad unit.

**On ad break start, including pre-roll:**


* Create the ` adBreak` object instance for the ad break; for example, ` adBreakObject`.
* Call ` trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.


**On every ad asset start:**


* **Call ` trackEvent(MediaHeartbeat.Event.AdComplete);` (New!)** 
  >[!NOTE]
  >
  >Call this only if the previous ad wasn’t complete. Consider a Boolean value to maintain an " ` isinAd`" state for the previous ad. 


* Create the ad object instance for the ad asset: for example, ` adObject`.
* Populate the ad metadata, ` adCustomMetadata`.
* Call ` trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call ` trackPlay()` if this is the first ad in a pre-roll ad break.


**On every ad asset complete:**


* **Do not make a call (New!)** 
  >[!NOTE]
  >
  >If the application knows it is the last ad in the ad break, call ` trackEvent:AdComplete` here and skip setting ` trackEvent:AdComplete` in the ` trackEvent:AdBreakComplete` 




**On ad skip:**


* Call ` trackEvent(MediaHeartbeat.Event.AdSkip);`.


**On ad break complete:**

* **Call ` trackEvent(MediaHeartbeat.Event.AdComplete);` (New!) ** 
  >[!NOTE]
  >
  >If this step is already performed above as part of the last ` trackEvent:AdComplete` call then this can be skipped. 

* Call ` trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
