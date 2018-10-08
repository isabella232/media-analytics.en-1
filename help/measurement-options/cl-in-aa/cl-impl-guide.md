---
description: null
seo-description: null
seo-title: Custom Link Implementation Guide
title: Custom Link Implementation Guide
uuid: 3dde245a-1df9-4c00-8751-7843acbe8873
index: y
internal: n
snippet: y
translate: y
---

# Custom Link Implementation Guide

Custom Video Tracking utilizes custom link tracking to send data directly to the analytics server:

* Data is sent by using the `trackLink()` / `s.tl()` / `trackAction()` method within Analytics. [The s.tl() Function - Link Tracking](https://marketing.adobe.com/resources/help/en_US/sc/implement/function_tl.html)

* SDKs or through the Data Insertion API.
* Most often used on platforms and devices without Analytics SDKs

**Requirements:**

* Access to video player API events and data
* Ability to add scripts if using Analytics SDK
* Ability to add tracking beacons (custom scripting or hardcode) if using Data Insertion API

**Metadata:**

* Metadata can be added to any tracking call as part of the link data
* If using `s.tl()` remember to update the `linkTrackVars` and `linkTrackEvents` 

  ```
  /*Call on video complete*/ 
  if (e.type == "ended") {  
      s.linkTrackVars = 'events, 
                         prop10, 
                         eVar10, 
                         eVar12, 
                         eVar13, 
                         eVar14, 
                         eVar15’; 
      s.linkTrackEvents = 'event3'; 
      s.prop10 = mediaName; 
      s.eVar10 = mediaName; 
      s.eVar12 = "video"; 
      s.eVar13 = document.title; 
      s.eVar14 = "Sailor Dave"; 
      s.eVar15 = mediaPlayerName; 
      s.events = 'event3'; 
      s.tl(this,'o','Video Complete'); 
  };
  ```

**Why use Custom Link:**

* Minimal prerequisites are needed
* Works on any platform, including no-script
* Any calculations, such as time spent or quartiles, must be calculated in a custom script 
* Very straightforward with no hidden libraries or scripts
* Total control over every aspect of the video data

* [](http://video.marijka.com/manual/101-custom.html)

**Sample JavaScript**

```
<script type="text/javascript"> 
  myvideo = document.getElementById('movie'); 
  myvideo.addEventListener('play',myHandler,false); 
  myvideo.addEventListener('seeked',myHandler,false); 
  myvideo.addEventListener('seeking',myHandler,false); 
  myvideo.addEventListener('pause',myHandler,false); 
  myvideo.addEventListener('ended',myHandler,false); 
   
  function myHandler(e) { 
      var video = document.getElementsByTagName('video')[0]; 
      var mediaName="13502979:Sailing"; 
      var mediaLength = video.duration; 
      var mediaPlayerName = "HTML5 Player"; 
      /*Define video offset*/ 
      if (video.currentTime > 0) { 
          mediaOffset = Math.floor(video.currentTime); 
      } else { 
          mediaOffset = 0; 
      }; 
      /*Call on video start*/ 
      if (e.type == "play") { 
          if (mediaOffset == 0) { 
              console.log(mediaPlayerName +' -> start -> playhead: ' + Math.floor(video.currentTime)); 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar14,eVar15'; 
              s.linkTrackEvents='event2'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar14="Sailor Dave"; 
              s.eVar15=mediaPlayerName; 
              s.events='event2'; 
              s.tl(this,'o','Video Start'); 
          } 
      }; 
   
      /*Call on video pause*/ 
      if (e.type == "pause") { 
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime)); 
          if (video.currentTime != video.duration) { 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar14,eVar15'; 
              s.linkTrackEvents='event7'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar14="Sailor Dave"; 
              s.eVar15=mediaPlayerName; 
              s.events='event7'; 
              s.tl(this,'o','Video Pause'); 
          } 
      }; 
   
      /*Call on video complete*/ 
      if (e.type == "ended") { 
          console.log(mediaPlayerName + 
                      ' -> ended -> playhead: ' +  
                      Math.floor(video.currentTime)); 
          s.linkTrackVars = 'events, 
                             prop10, 
                             eVar10, 
                             eVar12, 
                             eVar13, 
                             eVar14, 
                             eVar15'; 
          s.linkTrackEvents = 'event3'; 
          s.prop10= m ediaName; 
          s.eVar10=mediaName; 
          s.eVar12="video"; 
          s.eVar13=document.title; 
          s.eVar14="Sailor Dave"; 
          s.eVar15=mediaPlayerName; 
          s.events='event3'; 
          s.tl(this,'o','Video Complete'); 
      }; 
  }; 
</script>
```

