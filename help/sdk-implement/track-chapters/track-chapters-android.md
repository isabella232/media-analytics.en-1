---
seo-title: Track chapters and segments on Android
title: Track chapters and segments on Android
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
index: y
internal: n
snippet: y
---

# Track chapters and segments on Android{#track-chapters-and-segments-on-android}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs](../../sdk-implement/download-sdks.md).

<a id="section_52221B3A9BFD46B3A22DA6BCE97CCD75"></a>

1. Identify when the chapter start event occurs and create the `ChapterObject` instance by using the chapter information.

   Here is the `ChapterObject` chapter tracking reference:  

   >[!NOTE]
   >
   >These variables are only required if you are planning to track chapters.

   | Variable Name | Description | Required |
   | --- | --- | --- |
   | `name` | Chapter name | Yes |
   | `position` | Chapter position | Yes |
   | `length` | Chapter length | Yes |
   | `startTime` | Chapter start time | Yes |

   **Chapter object:** 

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. If you include custom metadata for the chapter, create the context data variables for the metadata: 

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>(); 
   chapterMetadata.put("segmentType", "Sample Segment Type"); 
   chapterMetadata.put("segmentName", "Sample Segment Name"); 
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance: 

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata); 
   }
   ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance: 

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
   }
   ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance: 

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
   }
   ```

1. If there are any additional chapters, repeat steps 1 through 5.

