---
seo-title: Overview
title: Overview
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
index: y
internal: n
snippet: y
---

# Overview{#overview}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs](../../sdk-implement/download-sdks.md).

Chapter and segment tracking is available for custom-defined video chapters or segments. Some common uses for chapter tracking are to define custom segments based on video content, such as baseball innings, or to define content segments between ad breaks. Chapter tracking is **not** required for core video heartbeat implementations.

Chapter tracking includes chapter starts, chapter completes, and chapter skips. You can use the video player API with customized segmentation logic to identify chapter events and to populate the required and optional chapter variables. Here are the key elements of tracking chapter playback:

**On chapter start**:

* Create the chapter object instance for the chapter, `chapterObject` 
* Populate the chapter metadata, `chapterCustomMetadata` 
* Call `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

**On chapter complete**:

* Call `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

**On chapter skip**:

* Call `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

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

1. If you include custom metadata for the chapter, create the context data variables for the metadata. 
1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance. 

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance. 

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance. 
1. If there are any additional chapters, repeat steps 1 through 5.

The following sample code uses the JavaScript 2.x SDK for an HTML5 video player. You should use this code with the core video playback code. 

```js
/* Call on chapter start */ 
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

* Heartbeat chapter start**&#42;**

**&#42;**This call contains additional chapter metadata variables.

**Chapter Complete**

At the chapter boundary end, a Heartbeat chapter complete call will be sent.

**Chapter Skip**

When a chapter is skipped, a Heartbeat chapter skip call will be sent. 
