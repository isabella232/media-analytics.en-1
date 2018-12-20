---
seo-title: 1.x for Android
title: 1.x for Android
uuid: e86fbf06-275d-4a40-8575-db9515b7a034
index: y
internal: n
snippet: y
---

# Android 1.x{#x-for-android}

The Android sample code helps you implement the Video Heartbeat Library for Nielsen, implement `NielsenPluginDelegate`, and configure opt-in/opt-out for Nielsen data collection.

## Configure the Video Heartbeat Library {#section_9526C0C0771C4FE19E7ADEC28103096C}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

For detailed instructions, see [Configure the Video Heartbeat Library](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/vhl-dev-guide-v15_android.pdf)

## Create the AdobeNielsenAPI {#section_129D10D357DE4320AF8277DA387CA411}

>[!TIP]
>
>The `AdobeNielsenAPI` should be created as early as possible, typically on app launch.

To create the `AdobeNielsenAPI`:

```java
// Create AdobeNielsenAPI 
Map<String, Object> appInfo = new HashMap<String, Object>(); 
appInfo.put("appId", <APP_ID>); 
appInfo.put("appVersion", <APP_VERSION>); 
appInfo.put("appName", <APP_NAME>); 
appInfo.put("sfcode", <SF_CODE>); 
  
Context context = <android-application-context>; 
AdobeNielsenAPI.configure(context, appInfo);
```

For more information about `AppInfo`, see *NielsenAppInfo* in [Variables and metadata](../dcr-vars-metadata.md).

## Instantiate and Configure the Video Heartbeat Components {#section_DFDF33ACC9D347F99F4315DD11381641}

To instantiate and configure the video heartbeat components for Nielsen:

```java
// Adobe Nielsen plugin 
SampleNielsenPluginDelegate nielsenPluginDelegate =  
  new CustomNielsenPluginDelegate(); 
nielsenPlugin =  
  new AdobeNielsenPlugin(nielsenPluginDelegate); 
AdobeNielsenPluginConfig nielsenPluginConfig =  
  new AdobeNielsenPluginConfig(); 
nielsenPluginConfig.configKey =  
  <CONFIG_KEY>; // Get this key from Adobe Representative 
nielsenPluginConfig.debugLogging =  
  true; // set this to false for production apps. 
 
// Add nielsen plugin to plugins array  
// list before configuring Heartbeat 
... 
 
// Heartbeat 
HeartbeatDelegate heartbeatDelegate =  
  new CustomHeartbeatDelegate(); 
Heartbeat heartbeat =  
  new Heartbeat(heartbeatDelegate, plugins); 
HeartbeatConfig heartbeatConfig =  
  new HeartbeatConfig(); 
heartbeatConfig.debugLogging =  
  true; // set this to false for production apps. 
heartbeat.configure(heartbeatConfig);
```

>[!IMPORTANT]
>
>You must get the `nielsenPluginConfig.configKey` key from your Adobe representative.

## Implement the NielsenPluginDelegate {#section_C2126992F4E84EBBA98F79120DBAE9B0}

The `NielsenPluginDelegate` is used by the video heartbeat library to enable Nielsen tracking.

Here is an example of a `NielsenPluginDelegate` implementation on Android:

```java
public class SampleNielsenPluginDelegate extends AdobeNielsenPluginDelegate { 
    public Map<String, Object> getMetadataInfo() { 
        HashMap<String, Object> metadata = new HashMap<String, Object>(); 
        //Required 
        metadata.put("type"          : "content"); 
        metadata.put("assetid"       : "vid-123"); 
        metadata.put("program"       : "MyProgram"); 
        metadata.put("title"         : "S2, E1"); 
        metadata.put("length"        : "574"); 
        metadata.put("isfullepisode" : "y"); 
        metadata.put("adloadtype"    : "2"); 
        metadata.put("airdate"       : "2015100100:00:00"); 
 
        //Recommended 
        metadata.put("segB"          : "CustomSegmentValueB"); 
        metadata.put("segC"          : "CustomSegmentValueC"); 
        metadata.put("crossId1"      : "Standard Episode ID"); 
 
        //Recommended only for distributors 
        metadata.put("crossId2"      : "Content Originator ID"); 
 
        //Needed when you override the values provided to appInfo  
        metadata.put("clientid"      : "us-XXXXXX"); 
        metadata.put("subbrand"      : "cXX"); 
 
        return metadata; 
    } 
 
    public Map<String, Object> getAdMetadataInfo() { 
        HashMap<String, Object> metadata = new HashMap<String, Object>(); 
        metadata.put("type", "preroll"); 
        metadata.put("assetid", "ad-ID"); 
 
        return metadata; 
    } 
 
    public Map<String, Object> getChannelInfo() { 
        HashMap<String, Object> metadata = new HashMap<String, Object>(); 
        metadata.put("channelName", "Adobe"); 
 
        return metadata; 
    } 
}
```

## MTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement MTVR in Android 1.6x, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR:

1. Update the Nielsen content metadata to include the following key/values:

   | Key | Value |
   | --- | --- |
   | `tv` | true |
   | `datasource` | ID3 |
   | `adloadtype` | <ul> <li>When linear ads are present (DTVR), the `adloadtype` = 1.  </li> <li>When DAI ads are present (DCR), the `adloadtype` = 2.  </li> </ul> |
   | `admodel` | <ul> <li>When linear ads are present (DTVR), the `admodel` = 1.  </li> <li>When DAI ads are present (DCR), the `admodel` = 2.  </li> </ul> | 

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [DTVR/MTVR implementation](../../nielsen-partnership/dcr-impl/dcr-dtvr.md).

   For example: 

   ```java
   //SampleNielsenPluginDelegate 
   public Map<String, Object> getMetadataInfo() { 
       HashMap<String, Object> nielsenContentMetadata =  
         NielsenMetadata.metadata; 
       if(isDTVRContent) { 
           nielsenContentMetadata.put("tv", true); 
           nielsenContentMetadata.put("datasource", "id3"); 
           nielsenContentMetadata.put("admodel", 1); 
       } 
       return nielsenContentMetadata; 
   }
   ```

   For more information, see [Variables and metadata](../dcr-vars-metadata.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the `VideoPlayerPlugin` (VHL) instance by using the `trackTimedMetadata` API.

   For example: 

   ```java
   void onTimedMetadata(String id3Tag) { 
       if(id3Tag.startsWith("/^www\\.nielsen\\.com/i")) { 
           MediaObject id3 =  
             MediaHeartbeat.createTimedMetadataObject(id3Tag); 
           _playerPlugin.trackTimedMetadata(id3Tag); 
       } 
   }
   ```

   All other implementation guidelines remain the same between DCR and MTVR.

