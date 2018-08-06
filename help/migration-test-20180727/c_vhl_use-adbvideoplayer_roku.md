---
description: null
seo-description: null
seo-title: Using ADBVideoPlayer
title: Using ADBVideoPlayer
uuid: b903b79f-47a3-49dc-9812-dbc82291f144
index: y
internal: n
snippet: y
translate: y
---

# Using ADBVideoPlayer


>[!IMPORTANT]
>
>Roku is deprecating the ` roVideoScreen` component that is required for ADBVideoPlayer. As a result of this, Adobe has deprecated the ADBVideoPlayer function as well. ADBVideoPlayer will be removed from the Roku SDK in future releases. 

The media heartbeats module provides an extension of the standard native player that takes care of binding the native player events to media module tracking APIs. If the application is built using this standard media player (for example, ` roVideoScreen` on Roku) the developer should let the provided extension handle all incoming events from the player by passing all incoming events to the extension as is. The extension takes care of calling relevant media heartbeats APIs based on the event type. This saves the developers a lot of effort in handling individual player events themselves. This way of integration is also demonstrated in the demo player provided with the SDK. 
Custom media events, such as ` AD_START, CHAPTER_START` and so on, would still be handled separately and tracked explicitly by the application using ` ADBMobile().mediaTrackEvent()` APIs (see the second method below). The code snippet below shows how the application can listen to ` roVideoScreen` events and pass messages to ADBVideoPlayer. 
If you intend to use standard metadata via ADBVideoPlayer, you need to create a dictionary of standard metadata and set it on content. The following code snippet demonstrates the usage.
**ADBVideoPlayer sample:** 
```
Function showVideoContent(content As Object) 
 
    port = CreateObject("roMessagePort")  
    screen = CreateObject("roVideoScreen")  
    screen.SetMessagePort(port) 
 
    screen.SetPositionNotificationPeriod(1)  
    screen.SetContent(content)  
    screen.Show() 
     
    ''' Send the content object. This object must specify the ‘live’ property if  
    ''' the content is a live stream  
    videoContextData = { } 
    videoContextData ["videotype"] = "episode" 
 
    standaradMetadata = {} 
    standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show"  
    standaradMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
 
    content[ADBMobile().MEDIA_STANDARD_VIDEO_METADATA] = standaradMetadata  
    ADBVideoPlayer().setContent(content, videoContextData) 
 
    while true 
        msg = wait(100, port) 
 
        ''' Let ADBVideoPlayer handle the message first 
        ADBVideoPlayer().handleMessage(msg) 
 
        ''' Run the process messages handler for ADB Media 
        ADBMobile().processMediaMessages() 
 
        if type(msg) = "roVideoScreenEvent" then  
            if msg.isScreenClosed() 
                exit while 
            elseif msg.isRequestFailed()  
            elseif msg.isStatusMessage()  
            elseif msg.isButtonPressed() 
            elseif msg.isPlaybackPosition() then  
            end if 
        else 
            'print "Unexpected message class: "; type(msg)  
        end if 
    end while  
End Function 

```

