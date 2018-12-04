---
seo-title: 1.x for JavaScript
title: 1.x for JavaScript
uuid: 415d219b-c3a7-42bf-8fba-70ef829e60eb
index: y
internal: n
snippet: y
---

# JavaScript 1.x{#x-for-javascript}

JavaScript sample code helps you implement the Video Heartbeat Library for Nielsen, implement `NielsenPluginDelegate`, and configure opt-in/opt-out for Nielsen data collection.

## Configure the Video Heartbeat Library {#section_A9B21BC13BA947729324BB41275688F3}

To instantiate and configure the video heartbeat components for Nielsen: 

```js
// Adobe Nielsen plugin 
var nielsenPluginConfig = new NielsenPluginConfig(); 
nielsenPluginConfig.debugLogging = true; // set this to false for production apps. 
nielsenPluginConfig.appInfo = { 
    apid : <APP_ID>, 
    appversion : <APP_VERSION>, 
    appname : <APP_NAME>, 
    sfcode : <SF_CODE>" 
}; //appinfo metadata 
nielsenPluginConfig.configKey = <CONFIG_KEY>; // Get this key from Adobe Representative 
  
this._nielsenPlugin.configure(nielsenPluginConfig); 
// Add nielsen plugin to plugins array list before configuring Heartbeat 
... 
 
// Heartbeat 
var heartbeatDelegate = new CustomHeartbeatDelegate(); 
var heartbeat = new Heartbeat(heartbeatDelegate, plugins); 
var heartbeatConfig = new HeartbeatConfig(); 
heartbeatConfig.debugLogging = true; // set this to false for production apps. 
heartbeat.configure(heartbeatConfig);
```

>[!IMPORTANT]
>
>You need to get the `nielsenPluginConfig.configKey` key from your Adobe representative.

For more information about AppInfo, see *NielsenAppInfo* in [Variables and metadata](../../nielsen-partnership/dcr-vars-metadata.md).

## Implement the NielsenPluginDelegate {#section_A9610928B87E49B3831B8C1A0BA9FEE6}

The `NielsenPluginDelegate` is used by the video heartbeat library to enable Nielsen tracking.

The following code is a sample `NielsenPluginDelegate` implementation for JavaScript:

```js
/* Sample NielsenPluginDelegate implementation */ 
var SampleNielsenPluginDelegate = ADB.va.plugins.nielsen.NielsenPluginDelegate; 
$.extend(SampleNielsenPluginDelegate.prototype, NielsenPluginDelegate.prototype); 
 
function SampleNielsenPluginDelegate() {} 
 
SampleVideoPlayerPluginDelegate.prototype.getMetadataInfo = function() { 
    return { 
        // Required 
        "type"          : "content", 
        "assetid"       : "vid-123", 
        "program"       : "MyProgram", 
        "title"         : "S2, E1", 
        "length"        : "574", 
        "isfullepisode" : "y", 
        "adloadtype"    : "2", 
        "airdate"       : "2015100100:00:00", 
 
        // Recommended 
        "segB"          : "CustomSegmentValueB", 
        "segC"          : "CustomSegmentValueC", 
        "crossId1"      : "Standard Episode ID", 
 
        // Recommended only for distributors 
        "crossId2"      : "Content Originator ID", 
 
        // Needed when you override the values provided to appInfo  
        "clientid"      : "us-XXXXXX", 
        "subbrand"      : "cXX" 
         
    }; 
}; 
  
SampleVideoPlayerPluginDelegate.prototype.getAdMetadataInfo = function() { 
    return { 
        "type"          : "preroll", 
        "assetid"       : "ad-ID" 
    }; 
}; 
  
SampleVideoPlayerPluginDelegate.prototype.getChannelInfo = function() { 
    return { 
        "channelName"   : "Adobe" 
    }; 
};
```

## DTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement DTVR in Javascript 1.x, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use DTVR:

1. Update the Nielsen content metadata to include the following key/values:

   <table id="table_FDBC2B510B534102B77DEFE2859F79B5"> 
    <thead> 
     <tr> 
      <th colname="col1" class="entry"> Key </th> 
      <th colname="col2" class="entry"> Value </th> 
     </tr> 
    </thead>
    <tbody> 
     <tr> 
      <td colname="col1"> <p> <span class="codeph"> tv </span> </p> </td> 
      <td colname="col2"> <p>true </p> </td> 
     </tr> 
     <tr> 
      <td colname="col1"> <p> <span class="codeph"> datasource </span> </p> </td> 
      <td colname="col2"> <p>ID3 </p> </td> 
     </tr> 
     <tr> 
      <td colname="col1"> <p> <span class="codeph"> adloadtype </span> </p> </td> 
      <td colname="col2"> <p> 
        <ul id="ul_E88C044C921B416DBCBB34DF29FC103D"> 
         <li id="li_C97E7E25532E40D48B109E61B09F1C67">When linear ads are present (DTVR), the <span class="codeph"> adloadtype </span> = 1. </li> 
         <li id="li_DC9FC0FC4F0B402884D2944886E3CF38">When DAI ads are present (DCR), the <span class="codeph"> adloadtype </span> = 2. </li> 
        </ul> </p> </td> 
     </tr> 
     <tr> 
      <td colname="col1"> <p> <span class="codeph"> admodel </span> </p> </td> 
      <td colname="col2"> <p> 
        <ul id="ul_1F101460C4794194B8663A51125ACD38"> 
         <li id="li_9C9779B2823C44BD81072092AE2556D0">When linear ads are present (DTVR), the <span class="codeph"> admodel </span> = 1. </li> 
         <li id="li_E17948EB7BDD45A489F124EA1AE84C29">When DAI ads are present (DCR), the <span class="codeph"> admodel </span> = 2. </li> 
        </ul> </p> </td> 
     </tr> 
    </tbody> 
   </table>

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [DTVR/MTVR implementation](../../nielsen-partnership/dcr-impl/dcr-dtvr.md).

   For example: 

   ```js
   SampleNielsenPluginDelegate.prototype.getMetadataInfo = function() { 
       if(dtvrContent){ 
           this._nielsenData.metadata["tv"] = true; 
           this._nielsenData.metadata["datasource"] = "id3"; 
           this._nielsenData.metadata["admodel"] = 1;         
           return this._nielsenData.metadata; 
       } 
   };
   ```

   For more information, see [Variables and metadata](../../nielsen-partnership/dcr-vars-metadata.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the `VideoPlayerPlugin` (VHL) instance by using the `trackTimedMetadata` API.

   For example: 

   ```js
   VideoAnalyticsProvider.prototype._onTimedMetadata = function(id3Tag) { 
       console.log('Player event: ON_TIMED_METADATA'); 
            
       if(id3tag && id3Tag.match(/^www\.nielsen\.com/i) !== null) { 
           this._playerPlugin.trackTimedMetadata(id3Tag + ""); 
       } 
   };
   ```

   All other implementation guidelines remain the same between DCR and DTVR.

