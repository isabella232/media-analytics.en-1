---
title: Learn to Track Chapters and Segments Using JavaScript 3.x
description: Learn about implementing chapter and segment tracking using the Media SDK in browser apps (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Track chapters and segments using JavaScript 3.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 3.x SDKs. If you are implementing any previous versions of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. Identify when the chapter start event occurs and create the `ChapterObject` instance by using the chapter information.

    `ChapterObject` chapter tracking reference:

    >[!NOTE]
    >
    >These variables are only required if you are planning to track chapters.

    | Variable Name | Type | Description |
    | --- | --- | --- |
    | `name` | string | Non empty string denoting chapter name. |
    | `position` | number | The position of the chapter within the content, starting with 1. |
    | `length` | number | Positive number denoting length of the chapter. |
    | `startTime` | number | Playhead value at start of chapter. |

    Chapter object:

    ```js
    var chapterObject =
      ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                         <POSITION>,
                                         <LENGTH>,
                                         <START_TIME>);
    ```

1. If you include custom metadata for the chapter, create the context data variables for the metadata:

    ```js
    var chapterMetadata = {};
    chapterMetadata["segmentType"] = "Sample segment type";
    ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance:

    ```js
    _onChapterStart = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

    };
    ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance:

    ```js
    _onChapterComplete = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterComplete);
    };
    ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance:

    ```js
    _onChapterSkip = function() {
        tracker.trackEvent(ADB.Media.Event.ChapterSkip);
    };
    ```

1. If there are any additional chapters, repeat steps 1 through 5.
