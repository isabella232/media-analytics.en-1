---
description: null
seo-description: null
seo-title: Track chapters
title: Track chapters
uuid: fa5f6914-a9a4-43d5-bdfe-4d5378cfde40
index: y
internal: n
snippet: y
translate: y
---

# Track chapters


>1. Identify when playback hits chapter start boundary. On chapter start create ` ADBMediaObject` instance using Chapter information.
>   Here is the ` ADBMediaObject`(Chapter Object) Reference: 

>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Chapter name  | Yes  |
>   |  ` position`  | Chapter position  | Yes  |
>   |  ` length`  | Chapter length  | Yes  |
>   |  ` startTime`  | Chapter start time  | Yes  |

>
>   ```
>   // Replace <CHAPTER_NAME> with the chapter name. 
>   // Replace <POSITION> with a valid chapter position value. 
>   // Replace <LENGTH> with the chapter length. 
>   // Replace <START_TIME> with the chapter start time. 
>    
>   id chapterObject = [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
>                                         position:[POSITION] 
>                                         length:[LENGTH] 
>                                         startTime:[START_TIME]];
>   ```
>
>1. Create Chapter context data dictionary if you intend to provide custom chapter metadata while tracking chapter.
>
>   ```
>   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
>   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
>   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
>   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"]; 
>   
>   ```
>
>1. Using track API, track ` ADBMediaHeartbeatEventChapterStart` event.
>
>   ```
>   - (void)onChapterStart:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
>                        mediaObject:chapterObject     
>                        data:chapterDictionary]; 
>   }
>   ```
>
>1. Identify if the playback hits a Chapter end boundary. On chapter complete, track the event using ` ADBMediaHeartbeatEventChapterComplete`.
>
>   ```
>   - (void)onChapterComplete:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
>                        mediaObject:nil  
>                        data:nil]; 
>   }
>   ```
>
>1. Optionally, identify if Chapter playback did not complete and was skipped.
>   If for example, the user seeks out of the chapter boundary, rack chapter skip event using ` ADBMediaHeartbeatEventChapterSkip`. 
>
>   ```
>   - (void)onChapterSkip:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
>                        mediaObject:nil  
>                        data:nil]; 
>   }
>   ```
>
>1. If there are any additional chapters, repeat Steps 1 through 5.
