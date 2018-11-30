---
seo-title: Track chapters and segments on JavaScript
title: Track chapters and segments on JavaScript
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
index: y
internal: n
snippet: y
---

# Track chapters and segments on JavaScript{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [](../../sdk-implement/download-sdks.md).

1. Identify when the chapter start event occurs and create the `ChapterObject` instance by using the chapter information.

   Here is the `ChapterObject` chapter tracking reference:  

   >[!NOTE]
   >
   >These variables are only required if you are planning to track chapters.

<table id="table_840ABDA54A4A436996464D59D04ABB4D"> 
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
   <td colname="col2"> <p>Chapter name </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> position </span> </td> 
   <td colname="col2"> <p>Chapter position </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> length </span> </td> 
   <td colname="col2"> <p>Chapter length </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> startTime </span> </td> 
   <td colname="col2"> <p>Chapter start time </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
 </tbody> 
</table>

   **Chapter object:** 

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. If you include custom metadata for the chapter, create the context data variables for the metadata: 

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance: 

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance: 

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance: 

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. If there are any additional chapters, repeat steps 1 through 5.

