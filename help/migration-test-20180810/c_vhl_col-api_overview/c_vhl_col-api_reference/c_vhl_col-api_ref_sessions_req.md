---
description: null
seo-description: null
seo-title: Sessions Request
title: Sessions Request
uuid: d69d0cbd-9ca7-4ff5-a0e0-2177866260ee
index: y
internal: n
snippet: y
translate: y
---

# Sessions Request


<a id="section_tps_bqm_kcb"></a>


```
POST 
http://{uri}/api/v1/sessions
```


**URI Parameters - **None

**Request Body - **Must be JSON, must have the same structure as this sample request body: 
```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "VA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```



* ` playerTime` (Mandatory) 
    * ` playhead` - Must be in seconds, but it can be a float.
    * ` ts` - Timestamp; must be in milliseconds.

* ` eventType` (Mandatory)
* ` params` (Mandatory)
* ` customMetadata` (Optional)
* ` qoeData` (Optional)


**Valid ` eventType` value: ** 


* ` sessionStart`


**Response - **


```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

>[!NOTE]
>
>The ` /api/v1/` part of the Location header provides the API version. The part of the Location header after ` […]sessions/` is the Session ID. 





#### Response Codes
|  HTTP Response Code  | Description  |
|---|---|
|  201  | Session created  |
|  400  | Bad Request  |
|  500  | Server error  |

