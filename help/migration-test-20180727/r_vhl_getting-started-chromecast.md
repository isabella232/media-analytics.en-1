---
description: You can use this information to help you get starting with the Chromecast SDK for Experience Cloud Solutions. This section assumes that you have configured a report suite through Adobe Mobile Services to collect app data.
seo-description: You can use this information to help you get starting with the Chromecast SDK for Experience Cloud Solutions. This section assumes that you have configured a report suite through Adobe Mobile Services to collect app data.
seo-title: Getting started
title: Getting started
uuid: bcc6a7d6-7e09-4c59-88c7-09c1afb48fb1
index: y
internal: n
snippet: y
translate: y
---

# Getting started


Adobe Mobile Services is the primary reporting interface for mobile app analytics and targeting. After you complete the configuration steps, you can download a configuration file that is preconfigured with your data collection server, report suite, and many other settings.

## Get the SDK {#section_DC5B6C26CD124C5087EA7BC7A67F7E16}

The ` [ AdobeMobileLibrary-Chromecast-2.0.2.zip ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases/download/chromecast-v2.0.2/AdobeMobileLibrary-Chromecast-2.0.2.zip)` download file consists of the following software components: 
* ` adbmobile-chromecast.min.js`: This library file will be included in your Chromecast app source folder.

* ` ADBMobileConfig` config This SDK configuration file is customized for your app.


Add the library file to your ` index.html` file, and create the ` ADBMobileConfig` global variable as follows: 

```
<script> 
var ADBMobileConfig = { 
    "marketingCloud": { 
        "org": "06074954519E38710A490D16@AdobeOrg" 
    }, 
    "target": { 
        "clientCode": "", 
        "timeout": 5 
    }, 
    "audienceManager": { 
        "server": "mobileservices.demdex.net" 
    }, 
    "analytics": { 
        "rsids": "mobile1figueroa-dev", 
        "server": "obumobile1.sc.omtrdc.net", 
        "ssl": false, 
        "offlineEnabled": true, 
        "charset": "UTF-8", 
        "lifecycleTimeout": 300, 
        "privacyDefault": "optedin", 
        "batchLimit": 0, 
        "timezone": "MDT", 
        "timezoneOffset": -360, 
        "referrerTimeout": 0, 
        "poi": [] 
    } 
}; 
</script> 
<script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script> 

```

