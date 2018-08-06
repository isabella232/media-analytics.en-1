---
description: null
seo-description: null
seo-title: One tracker for multiple sessions
title: One tracker for multiple sessions
uuid: 63aeae9b-5c20-4f85-baf8-cbc07a5cb160
index: y
internal: n
snippet: y
translate: y
---

# One tracker for multiple sessions


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/multi-sessions-one-at-a-time.png) 
>To create two instances of ` MediaHeartbeat` for two video players, set up the following code:
>
>```
>java>public class VideoAnalyticsProvider implements MediaHeartbeatDelegate { 
> 
>    private VideoPlayer _player; 
>    private MediaHeartbeat _heartbeat; 
> 
>    public VideoAnalyticsProvider(VideoPlayer player) { 
>        if (player == null) { 
>            throw new IllegalArgumentException("Player reference cannot be null."); 
>        } 
>    } 
> 
>    _player = player;  
>    _player.addObserver(this); 
> 
>    // Media Heartbeat initialization 
>    MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
> 
>    config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
>    config.channel = HEARTBEAT_CHANNEL; 
>    config.appVersion = HEARTBEAT_SDK; 
>    config.ovp = HEARTBEAT_OVP; 
>    config.playerName = PLAYER_NAME; 
>    config.ssl = false; 
>    config.debugLogging = true;  
>    _heartbeat = new MediaHeartbeat(this, config); 
>} 
>
>```
>
>```
>java>@Override 
>public MediaObject getQoSObject() { 
>    return MediaHeartbeat.createQoSObject(BITRATE, STARTUP_TIME, FPS, DROPPED_FRAMES); 
>} 
> 
>@Override 
>public Double getCurrentPlaybackTime() { 
>    return _player.getCurrentPlaybackTime(); 
>} 
>
>```
>
>```
>java>@Override 
>protected void onCreate(Bundle savedInstanceState) { 
>    super.onCreate(savedInstanceState); 
>    setContentView(R.layout.activity_main); 
> 
>    // Bootstrap the AppMeasurement library.  
>    Config.setContext(this.getApplicationContext()); 
> 
>    // Create the VideoPlayer instance.  
>    _player = new VideoPlayer(); 
> 
>    // Create the VideoAnalyticsProvider instance and 
>    // attach it to the VideoPlayer instance.  
>     _analyticsProvider = new VideoAnalyticsProvider(_player); 
> 
>    // Load the main video content.  
>     Uri uri = Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.video1);  
>     _player.loadContent(uri); 
>} 
>
>```

>To display the first session by using the ` VideoAnalyticsProvider` (hence ` MediaHeartbeat`) instance in Android, set up the following code: >
>```
>java>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
>); 
> 
>HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
>videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
> 
>// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback.  
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
>//    frame of main content is rendered on the screen.  
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 3. Call trackComplete() when the playback reaches the end, i.e., when the 
>//    video completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 4. Call trackSessionEnd() when the playback session is over. This method must  
>//    be called even if the user does not watch the video to completion.  
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

>To display the second session, you can use the same ` VideoAnalyticsProvider` ( ` MediaHeartbeat`) instance as the first session, but for a new session: >
>```
>java>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
>); 
> 
>HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
>videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
> 
>// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback.  
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
>//    frame of main content is rendered on the screen.  
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 3. Call trackComplete() when the playback reaches the end, i.e., when the  
>//    video completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 4. Call trackSessionEnd() when the playback session is over. This method  
>//    must be called even if the user does not watch the video to completion.  
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

