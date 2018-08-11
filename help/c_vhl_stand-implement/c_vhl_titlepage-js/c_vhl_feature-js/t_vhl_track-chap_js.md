---
description: null
seo-description: null
seo-title: Track chapters on JavaScript
title: Track chapters on JavaScript
uuid: 15c2af91-23b2-4e78-af7b-a2ecf58a67f6
index: y
internal: n
snippet: y
translate: y
---

# Track chapters on JavaScript

Here is the ` MediaHeartbeat.Event` chapter tracking constants reference: 

|  Constant Name  | Description  |
|---|---|
|  ` ChapterStart`  | Constant for tracking Chapter Start event  |
|  ` ChapterComplete`  | Constant for tracking Chapter Complete event  |
|  ` ChapterSkip`  | Constant for tracking Chapter Skip event  |


>1. Identify when playback hits chapter start boundary, and when the chapter starts, create the ` ChapterObject` instance using the chapter information.
>   Here is the ` MediaHeartbeat.Event` chapter tracking reference: 

>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Chapter name  | Yes  |
>   |  ` position`  | Chapter position  | Yes  |
>   |  ` length`  | Chapter length  | Yes  |
>   |  ` startTime`  | Chapter start time  | Yes  |

>
>   ```
>   js>   ///Replace <CHAPTER_NAME> with the chapter name. 
>   //Replace <POSITION> with a valid chapter position value. 
>   //Replace <LENGTH> with the chapter length. 
>   //Replace <START_TIME> with the chapter start time.  
>    
>   var chapterInfo = MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
>                                                        <POSITION>,  
>                                                        <LENGTH>,  
>                                                        <START_TIME>);
>   ```
>
>1. Create the chapter context data dictionary if you intend to provide custom chapter metadata while tracking chapters.
>
>   ```
>   js>   var chapterCustomMetadata = { 
>        segmentType: "Sample segment type",  
>        segmentName: "Sample segment name",  
>        segmentInfo: "Sample segment info" 
>   }; 
>   
>   ```
>
>1. Using the track API, track the ` MediaHeartbeat.Event` chapter events.
>
>   ```
>   js>   _onChapterStart = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
>                                       chapterObject,  
>                                       chapterCustomMetadata); 
>   };
>   ```
>
>1. Identify if the playback hits the ` ChapterBreak` end boundary, and on ` ChapterBreak` complete, track the event using ` MediaHeartbeat.Event.ChapterComplete`.
>
>   ```
>   js>   _onChapterComplete = function() { 
>      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
>   };
>   ```
>
>1. Optionally, identify if chapter playback did not complete and was skipped (for example, if the user seeks out of the chapter boundary), and track the chapter skip event using ` MediaHeartbeat.Event.ChapterSkip`.
>
>   ```
>   js>   _onChapterSkip = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
>   };
>   ```
>
>1. If there are any additional chapters, repeat steps 1 through 5.
