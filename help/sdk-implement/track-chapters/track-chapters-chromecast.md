---
title: Learn How to Track Chapters and Segments on Chromecast
description: Learn about implementing chapter and segment tracking using the Media SDK on Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Track chapters and segments on Chromecast{#track-chapters-and-segments-on-chromecast}

The following instructions provide guidance for implementation using 2.x SDKs.

>[!IMPORTANT]
>
> If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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

    Chapter object: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

    ```js
    chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
    ```

1. If you include custom metadata for the chapter, create the context data variables for the metadata:

    ```js
    var chapterContextData = {
        segmentType: "Sample segment type"
    };
    ```

1. To begin tracking the chapter playback, track the `ChapterStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

    ```js
    ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData);
    ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

    ```js
    ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
    ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), track the `ChapterSkip` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

    ```js
    ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
    ```

1. If there are any additional chapters, repeat steps 1 through 5.
