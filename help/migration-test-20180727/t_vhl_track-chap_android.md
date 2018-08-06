---
description: null
seo-description: null
seo-title: Track chapters
title: Track chapters
uuid: 2eeb3133-a234-43da-ada6-1c0371ffcd65
index: y
internal: n
snippet: y
translate: y
---

# Track chapters

Here is the ` MediaHeartbeat.Event` chapter tracking constants reference: 


|  Constant Name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.ChapterStart`  | Constant for tracking Chapter Start event  |
|  ` MediaHeartbeat.Event.ChapterComplete`  | Constant for tracking Chapter Complete event  |
|  ` MediaHeartbeat.Event.ChapterSkip`  | Constant for tracking Chapter Skip event  |


>1. Identify when playback hits a chapter start boundary, and when the chapter starts, create a ` MediaObject` instance using the chapter information.
>   Here is the ` MediaObject` (Chapter Object) reference: 


>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Chapter name  | Yes  |
>   |  ` position`  | Chapter position  | Yes  |
>   |  ` length`  | Chapter length  | Yes  |
>   |  ` startTime`  | Chapter start time  | Yes  |

>
>   ```
>   java>   // Replace <CHAPTER_NAME> with the chapter name. 
>   // Replace <POSITION> with a valid chapter position value. 
>   // Replace <LENGTH> with the chapter length. 
>   // Replace <START_TIME> with the chapter start time.  
>   MediaObject chapterDataInfo =  
>     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
>                                        <POSITION>,  
>                                        <LENGTH>,  
>                                        <START_TIME>);
>   ```
>
>1. Create the Chapter context data dictionary if you plan to provide custom chapter metadata while tracking chapters.
>
>   ```
>   java>   HashMap<String, String> chapterMetadata =  
>     new HashMap<String,String>(); 
>   chapterMetadata.put("segmentType", "Sample Segment Type"); 
>   chapterMetadata.put("segmentName", "Sample Segment Name"); 
>   chapterMetadata.put("segmentInfo", "Sample Segment Info"); 
>   
>   ```
>
>1. Using the track API, track the ` MediaHeartbeat.Event.ChapterStart` event.
>
>   ```
>   java>   public void onChapterStart(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
>                             chapterDataInfo,  
>                             chapterMetadata); 
>   }
>   ```
>
>1. Identify if the playback hits a chapter end boundary, and on ` AdBreak` complete, track the event using ` MediaHeartbeat.Event.ChapterComplete`.
>
>   ```
>   java>   public void onChapterComplete(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
>   }
>   ```
>
>1. Optionally, identify whether Chapter playback did not complete and was skipped.
>   For example, if the user seeks out of the chapter boundary, track the chapter skip event using ` MediaHeartbeat.Event.ChapterSkip`. 
>
>   ```
>   java>   public void onChapterSkip(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
>   }
>   ```
>
>1. If there are any additional chapters, repeat Steps 1 through 5.
