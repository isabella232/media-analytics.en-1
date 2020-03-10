---
title: Track chapters and segments on Roku
description: This topic describes implementing chapter and segment tracking using the Media SDK on Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3

---

# Track chapters and segments on Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implemement standard ad metadata

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
    chapterInfo =  
      adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                 <POSITION>,  
                                 <LENGTH>,  
                                 <START_TIME>);)
    ```

1. If you include custom metadata for the chapter, create the context data variables for the metadata: 

    ```
    chapterContextData = {} 
    chapterContextData["seg_type"] = "seg_type" 
    chapterContextData["seg_name"] = "seg_name" 
    chapterContextData["seg_info"] = "seg_info"
    ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance: 

    ```
    ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
    ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance. 

    ```
    chapterContextData = {} 
    ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
    ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance.

    ```
    chapterContextData = {} 
    ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
    ```

1. If there are any additional chapters, repeat steps 1 through 5.

