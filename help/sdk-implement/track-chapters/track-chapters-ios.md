---
title: Learn How to Track Chapters and Segments on iOS
description: Learn about implementing chapter and segment tracking using the Media SDK on iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
exl-id: ea8a1dd6-043f-41a4-9cef-845da92bfa32
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
---
# Track chapters and segments on iOS{#track-chapters-and-segments-on-ios}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. Identify when the chapter start event occurs and create the `ChapterObject` instance by using the chapter information.

    `ChapterObject` chapter tracking reference:  
 
    >[!NOTE]
    >
    >These variables are only required if you are planning to track chapters.
 
    | Variable Name | Description | Required |
    | --- | --- | :---: |
    | `name` | Chapter name | Yes |
    | `position` | Chapter position | Yes |
    | `length` | Chapter length | Yes |
    | `startTime` | Chapter start time | Yes |
 
    Chapter object: 
 
    ```
    id chapterObject =  
      [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                         position:[POSITION] 
                         length:[LENGTH] 
                         startTime:[START_TIME]];
    ```

1. If you include custom metadata for the chapter, create the context data variables for the metadata: 

    ```
    NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
    [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
    [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
    [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
    ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance: 

    ```
    - (void)onChapterStart:(NSNotification *)notification { 
        [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                         mediaObject:chapterObject     
                         data:chapterDictionary]; 
    }
    ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance: 

    ```
    - (void)onChapterComplete:(NSNotification *)notification { 
        [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                         mediaObject:nil  
                         data:nil]; 
    }
    ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance: 

    ```
    - (void)onChapterSkip:(NSNotification *)notification { 
        [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                         mediaObject:nil  
                         data:nil]; 
    }
    ```

1. If there are any additional chapters, repeat steps 1 through 5.
