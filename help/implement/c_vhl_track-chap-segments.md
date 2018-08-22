---
description: null
seo-description: null
seo-title: Track Chapters and Segments
title: Track Chapters and Segments
uuid: b4bc61c9-7ba7-4150-a475-1c2d094c67a8
index: y
internal: n
snippet: y
translate: y
---

# Track Chapters and Segments


>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here:[](../implement/download-sdks.md). 


## Overview {#section_42F6679178794FF5A923E5B3C71E9965}

Chapter and segment tracking is available for custom-defined video chapters or segments. Some common uses for chapter tracking are to define custom segments based on video content, such as baseball innings, or to define content segments between ad breaks. Chapter tracking is **not** required for core video heartbeat implementations. 

Chapter tracking includes chapter starts, chapter completes, and chapter skips. You can use the video player API with customized segmentation logic to identify chapter events and to populate the required and optional chapter variables. Here are the key elements of tracking chapter playback: 

**On chapter start**: 


* Create the chapter object instance for the chapter, ` chapterObject`
* Populate the chapter metadata, ` chapterCustomMetadata`
* Call ` trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`


**On chapter complete**: 


* Call ` trackEvent(MediaHeartbeat.Event.ChapterComplete);`


**On chapter skip**: 


* Call ` trackEvent(MediaHeartbeat.Event.ChapterSkip);`


## Implement {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}


1. Identify when the chapter start event occurs and create the ` ChapterObject` instance by using the chapter information. Here is the ` ChapterObject` chapter tracking reference: 
   >[!NOTE] {type="note"}
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


    * **Android:** 
      ```
      java      // Replace <CHAPTER_NAME> with the chapter name. 
      // Replace <POSITION> with a valid chapter position value. 
      // Replace <LENGTH> with the chapter length. 
      // Replace <START_TIME> with the chapter start time.  
      MediaObject chapterDataInfo =  
        MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                           <POSITION>,  
                                           <LENGTH>,  
                                           <START_TIME>);
      ```

    * **iOS:** 
      ```
      // Replace <CHAPTER_NAME> with the chapter name. 
      // Replace <POSITION> with a valid chapter position value. 
      // Replace <LENGTH> with the chapter length. 
      // Replace <START_TIME> with the chapter start time. 
       
      id chapterObject = [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                                            position:[POSITION] 
                                            length:[LENGTH] 
                                            startTime:[START_TIME]];
      ```

    * **JavaScript:** 
      ```
      js      ///Replace <CHAPTER_NAME> with the chapter name. 
      //Replace <POSITION> with a valid chapter position value. 
      //Replace <LENGTH> with the chapter length. 
      //Replace <START_TIME> with the chapter start time.  
       
      var chapterInfo = MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                                           <POSITION>,  
                                                           <LENGTH>,  
                                                           <START_TIME>);
      ```



1. If you include custom metadata for the chapter, create the context data variables for the metadata. 
    * **Android:** 
      ```
      java      HashMap<String, String> chapterMetadata =  
        new HashMap<String,String>(); 
      chapterMetadata.put("segmentType", "Sample Segment Type"); 
      chapterMetadata.put("segmentName", "Sample Segment Name"); 
      chapterMetadata.put("segmentInfo", "Sample Segment Info");
      ```

    * **iOS:** 
      ```
      NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
      [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
      [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
      [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
      ```

    * **JavaScript:** 
      ```
      js      var chapterCustomMetadata = { 
          segmentType: "Sample segment type",  
          segmentName: "Sample segment name",  
          segmentInfo: "Sample segment info" 
      };
      ```



1. To begin tracking the chapter playback, call the ` ChapterStart` event in the ` MediaHeartbeat` instance. 
    * **Android:** 
      ```
      java      public void onChapterStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                chapterDataInfo,  
                                chapterMetadata); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onChapterStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                           mediaObject:chapterObject     
                           data:chapterDictionary]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onChapterStart = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                          chapterObject,  
                                          chapterCustomMetadata); 
      };
      ```



1. When playback reaches the chapter end boundary, as defined by your custom code, call the ` ChapterComplete` event in the ` MediaHeartbeat` instance. 
    * **Android:** 
      ```
      java      public void onChapterComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onChapterComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onChapterComplete = function() { 
         this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
      };
      ```



1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the ` ChapterSkip` event in the MediaHeartbeat instance. 
    * **Android:** 
      ```
      java      public void onChapterSkip(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onChapterSkip:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onChapterSkip = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
      };
      ```



1. If there are any additional chapters, repeat steps 1 through 5.


The following sample code uses the JavaScript 2.x SDK for an HTML5 video player. You should use this code with the core video playback code. 
```
js/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 

```


## Validate {#section_07EC2811BE3249249494596BFE9BF869}

**Chapter Start ** 

On start of an individual chapter playback, one key calls are sent: 


* Heartbeat chapter start*****


*****This call contains additional chapter metadata variables. 

**Chapter Complete** 

At the chapter boundary end, a Heartbeat chapter complete call will be sent. 

**Chapter Skip** 

When a chapter is skipped, a Heartbeat chapter skip call will be sent. 
