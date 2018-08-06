---
description: null
seo-description: null
seo-title: One tracker for multiple sessions
title: One tracker for multiple sessions
uuid: dfef2d1b-8e1e-4795-a35d-66bdf26ca0bc
index: y
internal: n
snippet: y
translate: y
---

# One tracker for multiple sessions


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/multi-sessions-one-at-a-time.png) 
>To create two instances of ` MediaHeartbeat` for two video players, enter the following: >
>```
>@interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
> 
>@end    
>  
>@implementation { 
>    VideoPlayer *_player; 
>} 
>  
>- (instancetype)initWithPlayer:(AVPlayer *)player { 
>    if (self = [super init]) { 
>        _player = player; 
>  
>        ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
>        config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
>        config.channel = HEARTBEAT_CHANNEL; 
>        config.appVersion = HEARTBEAT_SDK_VERSION; 
>        config.playerName = PLAYER_NAME; 
>        config.ssl = SSL_SETTING; 
>        config.debugLogging = DEBUG_SETTING; 
>  
>        ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];       
>        _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
>          
>        [self setupPlayerNotifications]; 
>    } 
>  
>    return self; 
>} 
>  
>- (ADBMediaObject *)getQoSInfo { 
>    return [ADBMediaHeartbeat createQoSObjectWithBitrate:CURRENT_BITRATE_VALUE  
>                              startupTime:CALCULATED_STARTED_TIME  
>                              fps:CALCULATED_FPS  
>                              droppedFrames:DROPPED_FRAMES_COUNT]; 
>} 
>  
>- (NSTimeInterval)getCurrentPlaybackTime { 
>    return CMTimeGetSeconds(_player.currentTime); 
>} 
>  
>@end 
>
>```
>
>```
>- (void)viewDidAppear:(BOOL)animated { 
>    [super viewDidAppear:animated]; 
>    [ADBMobile setDebugLogging:YES]; 
>  
>    // Setup the first video player 
>    NSURL *streamUrl = [NSURL URLWithString:CONTENT_URL]; 
>  
>    if (!self.videoPlayer) { 
>        self.videoPlayer = [[VideoPlayer alloc] initWithContentURL:streamUrl]; 
>        //setup player 
>    } 
>  
>    // Create the VideoAnalyticsProvider instance and attach it to the first  
>    // VideoPlayer instance. 
>    if (!self.videoAnalyticsProvider) { 
>        self.videoAnalyticsProvider =  
>          [[VideoAnalyticsProvider alloc] initWithPlayerDelegate:self.videoPlayer]; 
>    } 
>} 
>
>```

>To display the first session by using the ` VideoAnalyticsProvider` (hence ` MediaHeartbeat`) instance in iOS, set up the following code: >
>```
>// Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                     length:VIDEO_LENGTH  
>                     streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>     
>NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
>[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>    
>// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>//    i.e., there's an intent to start playback. 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>....... 
>....... 
>   
>// 2. Call trackPlay when the playback actually starts, i.e., when the first  
>//    frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>   
>// 3. Call trackComplete when the playback reaches the end, i.e., when the 
>//    video completes and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
>    
>// 4. Call trackSessionEnd when the playback session is over. This method  
>//    must be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

>To display the second session, you can use the same ` VideoAnalyticsProvider` ( ` MediaHeartbeat`) instance as the first session, but for a new session: >
>```
>// Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                     length:VIDEO_LENGTH  
>                     streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>     
>NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
>[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>    
>// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback. 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>....... 
>....... 
>   
>// 2. Call trackPlay when the playback actually starts, i.e. when the first  
>//    frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>   
>// 3. Call trackComplete when the playback reaches the end, i.e., when the 
>//    video completes and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
>    
>// 4. Call trackSessionEnd when the playback session is over. This method  
>//    must be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

