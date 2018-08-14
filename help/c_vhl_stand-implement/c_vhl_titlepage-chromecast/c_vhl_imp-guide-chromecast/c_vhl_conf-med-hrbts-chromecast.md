---
description: After the application has acquired the Adobe Mobile SDK, you need to configure the media heartbeats.
seo-description: After the application has acquired the Adobe Mobile SDK, you need to configure the media heartbeats.
seo-title: Configure MediaHeartbeat on Chromecast
title: Configure MediaHeartbeat on Chromecast
uuid: b7b09cde-d29e-4fa3-8784-842a28a70c4d
index: y
internal: n
snippet: y
translate: y
---

# Configure MediaHeartbeat on Chromecast

The global variable used to configure Adobe Mobile has an exclusive key for media heartbeats with the name "mediaHeartbeat". This is where the configuration parameters for the media heartbeats belong. An example below demonstrates it. 

A sample ` ADBMobileConfig` implementation is provided with the package (under [!DNL  samples]), Obtain the proper settings from an Adobe representative. 

For example: 
```
{
    "version":"1.0", 
    "analytics": {
        "rsids":"",
        "server":"",
        "charset":"UTF-8", 
        "ssl":false, 
        "offlineEnabled":false, 
        "lifecycleTimeout":30, 
        "batchLimit":50, 
        "privacyDefault":"optedin", 
        "poi":[
        ]
    },
    "marketingCloud":{
        "org":""
    },
    "target":{ 
        "clientCode":"", 
        "timeout":5
    },
    "audienceManager":{ 
        "server":""
    },
    "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
    },
    "mediaHeartbeat":{ 
        "server":"example.com", 
        "publisher":"sample-publisher", 
        "channel":"sample-channel", 
        "ssl":false,
        "ovp":"sample-ovp", 
        "sdkVersion":"sample-sdk", 
        "playerName":"chromecast"
    }
}

```




<table id="table_00A5AE3DE21546DC89F561BAFEC6E710"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Config Parameter </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> server</span></td> 
   <td colname="col2"> <p>String that represents the URL of the tracking endpoint on the backend. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> publisher</span></td> 
   <td colname="col2"> <p>String that represents the content publisher unique identifier. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> channel</span></td> 
   <td colname="col2"> <p>String that represents the name of the content distribution channel. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ssl</span></td> 
   <td colname="col2"> <p>Boolean that represents whether SSL should be used for tracking calls. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ovp</span></td> 
   <td colname="col2"> <p>String that represents the name of the video player provider. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> sdkversion</span></td> 
   <td colname="col2"> <p>String that represents the current version of the app/SDK. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> playerName</span></td> 
   <td colname="col2"> <p>String that represents the name of the player. </p> </td> 
  </tr> 
 </tbody> 
</table>


>[!IMPORTANT]
>
>If ` mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls. 

