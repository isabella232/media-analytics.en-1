---
description: null
seo-description: null
seo-title: One tracker for multiple sessions
title: One tracker for multiple sessions
uuid: 7b884107-9627-45f4-8b70-1d8634298106
index: y
internal: n
snippet: y
translate: y
---

# One tracker for multiple sessions


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](assets/multi-sessions-one-at-a-time.png) 

>
>* **Android - **To create two instances of ` MediaHeartbeat` for two video players, set up the following code:

>
>  ```
>  java>  public class VideoAnalyticsProvider implements MediaHeartbeatDelegate { 
>   
>      private VideoPlayer _player; 
>      private MediaHeartbeat _heartbeat; 
>   
>      public VideoAnalyticsProvider(VideoPlayer player) { 
>          if (player == null) { 
>              throw new IllegalArgumentException("Player reference cannot be null."); 
>          } 
>      } 
>   
>      _player = player;  
>      _player.addObserver(this); 
>   
>      // Media Heartbeat initialization 
>      MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
>   
>      config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
>      config.channel = HEARTBEAT_CHANNEL; 
>      config.appVersion = HEARTBEAT_SDK; 
>      config.ovp = HEARTBEAT_OVP; 
>      config.playerName = PLAYER_NAME; 
>      config.ssl = false; 
>      config.debugLogging = true;  
>      _heartbeat = new MediaHeartbeat(this, config); 
>  } 
>  
>  ```
>
>  ```
>  java>  @Override 
>  public MediaObject getQoSObject() { 
>      return MediaHeartbeat.createQoSObject(BITRATE, STARTUP_TIME, FPS, DROPPED_FRAMES); 
>  } 
>   
>  @Override 
>  public Double getCurrentPlaybackTime() { 
>      return _player.getCurrentPlaybackTime(); 
>  } 
>  
>  ```
>
>  ```
>  java>  @Override 
>  protected void onCreate(Bundle savedInstanceState) { 
>      super.onCreate(savedInstanceState); 
>      setContentView(R.layout.activity_main); 
>   
>      // Bootstrap the AppMeasurement library.  
>      Config.setContext(this.getApplicationContext()); 
>   
>      // Create the VideoPlayer instance.  
>      _player = new VideoPlayer(); 
>   
>      // Create the VideoAnalyticsProvider instance and 
>      // attach it to the VideoPlayer instance.  
>       _analyticsProvider = new VideoAnalyticsProvider(_player); 
>   
>      // Load the main video content.  
>       Uri uri = Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.video1);  
>       _player.loadContent(uri); 
>  } 
>  
>  ```


>  To display the first session by using the ` VideoAnalyticsProvider` (hence ` MediaHeartbeat`) instance in Android, set up the following code: >
>  ```
>  java>  // Set up mediaObject 
>  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>      Configuration.VIDEO_NAME,  
>      Configuration.VIDEO_ID,  
>      Configuration.VIDEO_LENGTH,  
>      MediaHeartbeat.StreamType.VOD 
>  ); 
>   
>  HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>  videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
>  videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
>   
>  // 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>  //    i.e., there is an intent to start playback.  
>  _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
>   
>  ...... 
>  ...... 
>   
>  // 2. Call trackPlay() when the playback actually starts, i.e., when the first  
>  //    frame of main content is rendered on the screen.  
>  _mediaHeartbeat.trackPlay(); 
>   
>  ....... 
>  ....... 
>   
>  // 3. Call trackComplete() when the playback reaches the end, i.e., when the 
>  //    video completes and finishes playing. 
>  _mediaHeartbeat.trackComplete(); 
>   
>  ........ 
>  ........ 
>   
>  // 4. Call trackSessionEnd() when the playback session is over. This method must  
>  //    be called even if the user does not watch the video to completion.  
>  _mediaHeartbeat.trackSessionEnd(); 
>   
>  ........ 
>  ........ 
>  
>  ```


>  To display the second session, you can use the same ` VideoAnalyticsProvider` ( ` MediaHeartbeat`) instance as the first session, but for a new session: >
>  ```
>  java>  // Set up mediaObject 
>  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>      Configuration.VIDEO_NAME,  
>      Configuration.VIDEO_ID,  
>      Configuration.VIDEO_LENGTH,  
>      MediaHeartbeat.StreamType.VOD 
>  ); 
>   
>  HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>  videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
>  videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
>   
>  // 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>  //    i.e., there is an intent to start playback.  
>  _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
>   
>  ...... 
>  ...... 
>   
>  // 2. Call trackPlay() when the playback actually starts, i.e., when the first  
>  //    frame of main content is rendered on the screen.  
>  _mediaHeartbeat.trackPlay(); 
>   
>  ....... 
>  ....... 
>   
>  // 3. Call trackComplete() when the playback reaches the end, i.e., when the  
>  //    video completes and finishes playing. 
>  _mediaHeartbeat.trackComplete(); 
>   
>  ........ 
>  ........ 
>   
>  // 4. Call trackSessionEnd() when the playback session is over. This method  
>  //    must be called even if the user does not watch the video to completion.  
>  _mediaHeartbeat.trackSessionEnd(); 
>   
>  ........ 
>  ........ 
>  
>  ```


>* **iOS - **To create two instances of ` MediaHeartbeat` for two video players, enter the following: >
>  ```
>  @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
>   
>  @end    
>    
>  @implementation { 
>      VideoPlayer *_player; 
>  } 
>    
>  - (instancetype)initWithPlayer:(AVPlayer *)player { 
>      if (self = [super init]) { 
>          _player = player; 
>    
>          ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
>          config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
>          config.channel = HEARTBEAT_CHANNEL; 
>          config.appVersion = HEARTBEAT_SDK_VERSION; 
>          config.playerName = PLAYER_NAME; 
>          config.ssl = SSL_SETTING; 
>          config.debugLogging = DEBUG_SETTING; 
>    
>          ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];       
>          _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
>            
>          [self setupPlayerNotifications]; 
>      } 
>    
>      return self; 
>  } 
>    
>  - (ADBMediaObject *)getQoSInfo { 
>      return [ADBMediaHeartbeat createQoSObjectWithBitrate:CURRENT_BITRATE_VALUE  
>                                startupTime:CALCULATED_STARTED_TIME  
>                                fps:CALCULATED_FPS  
>                                droppedFrames:DROPPED_FRAMES_COUNT]; 
>  } 
>    
>  - (NSTimeInterval)getCurrentPlaybackTime { 
>      return CMTimeGetSeconds(_player.currentTime); 
>  } 
>    
>  @end 
>  
>  ```
>
>  ```
>  - (void)viewDidAppear:(BOOL)animated { 
>      [super viewDidAppear:animated]; 
>      [ADBMobile setDebugLogging:YES]; 
>    
>      // Setup the first video player 
>      NSURL *streamUrl = [NSURL URLWithString:CONTENT_URL]; 
>    
>      if (!self.videoPlayer) { 
>          self.videoPlayer = [[VideoPlayer alloc] initWithContentURL:streamUrl]; 
>          //setup player 
>      } 
>    
>      // Create the VideoAnalyticsProvider instance and attach it to the first  
>      // VideoPlayer instance. 
>      if (!self.videoAnalyticsProvider) { 
>          self.videoAnalyticsProvider =  
>            [[VideoAnalyticsProvider alloc] initWithPlayerDelegate:self.videoPlayer]; 
>      } 
>  } 
>  
>  ```


>  To display the first session by using the ` VideoAnalyticsProvider` (hence ` MediaHeartbeat`) instance in iOS, set up the following code: >
>  ```
>  // Set up mediaObject 
>  ADBMediaObject *mediaObject =  
>    [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                       length:VIDEO_LENGTH  
>                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>       
>  NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
>  [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>  [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>      
>  // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>  //    i.e., there's an intent to start playback. 
>  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>  ....... 
>  ....... 
>     
>  // 2. Call trackPlay when the playback actually starts, i.e., when the first  
>  //    frame of the main content is rendered on the screen. 
>  [_mediaHeartbeat trackPlay]; 
>  ....... 
>  ....... 
>     
>  // 3. Call trackComplete when the playback reaches the end, i.e., when the 
>  //    video completes and finishes playing. 
>  [_mediaHeartbeat trackComplete]; 
>  ....... 
>  ....... 
>      
>  // 4. Call trackSessionEnd when the playback session is over. This method  
>  //    must be called even if the user does not watch the video to completion. 
>  [_mediaHeartbeat trackSessionEnd]; 
>  ....... 
>  ....... 
>  
>  ```


>  To display the second session, you can use the same ` VideoAnalyticsProvider` ( ` MediaHeartbeat`) instance as the first session, but for a new session: >
>  ```
>  // Set up mediaObject 
>  ADBMediaObject *mediaObject =  
>    [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                       length:VIDEO_LENGTH  
>                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>       
>  NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
>  [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>  [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>      
>  // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>  //    i.e., there is an intent to start playback. 
>  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>  ....... 
>  ....... 
>     
>  // 2. Call trackPlay when the playback actually starts, i.e. when the first  
>  //    frame of the main content is rendered on the screen. 
>  [_mediaHeartbeat trackPlay]; 
>  ....... 
>  ....... 
>     
>  // 3. Call trackComplete when the playback reaches the end, i.e., when the 
>  //    video completes and finishes playing. 
>  [_mediaHeartbeat trackComplete]; 
>  ....... 
>  ....... 
>      
>  // 4. Call trackSessionEnd when the playback session is over. This method  
>  //    must be called even if the user does not watch the video to completion. 
>  [_mediaHeartbeat trackSessionEnd]; 
>  ....... 
>  ....... 
>  
>  ```


>* **JavaScript - **>
>  ```
>  js>  var MediaHeartbeat = ADB.va.MediaHeartbeat; 
>  var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
>  var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
>   
>  function VideoAnalyticsProvider(player) { 
>      if (!player) { 
>          throw new Error("Illegal argument. Player reference cannot be null.") 
>      }   
>      this._player = player; 
>   
>      // Media Heartbeat initialization 
>      var mediaConfig = new MediaHeartbeatConfig(); 
>      mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
>      mediaConfig.playerName = Configuration.PLAYER.NAME; 
>      mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
>      mediaConfig.debugLogging = true; 
>      mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
>      mediaConfig.ssl = false; 
>      mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
>   
>      var mediaDelegate = new MediaHeartbeatDelegate(); 
>   
>      mediaDelegate.getCurrentPlaybackTime = function() { 
>          return player.getCurrentPlaybackTime(); 
>      }; 
>   
>      mediaDelegate.prototype.getQoSObject = function() { 
>          return player.getQoSInfo(); 
>      }; 
>   
>      this._mediaHeartbeat =  
>        new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
>  } 
>  
>  ```
>
>  ```
>  js>  // Create the first VideoPlayer instance.  
>  var _player1 = new VideoPlayer(); 
>   
>  // Create the first VideoAnalyticsProvider instance and 
>  // attach it to the VideoPlayer instance.  
>  analyticsProvider1 = new VideoAnalyticsProvider(_player1); 
>   
>  // Load the main video content.  
>  _player1.loadContent(URL_TO_VIDEO_1);
>  ```



