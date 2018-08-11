---
description: null
seo-description: null
seo-title: Opt-Out and Privacy Settings
title: Opt-Out and Privacy Settings
uuid: 7e0e6a10-9070-4230-9885-068be3608121
index: y
internal: n
snippet: y
translate: y
---

# Opt-Out and Privacy Settings

You can control whether or not Analytics data is sent on a specific device using the following settings: 
* The ` privacyDefault` setting in the ` ADBMobileConfig` config. This setting controls the initial setting; it persists until it is changed in code. 

* The ` ADBMobile.config.setPrivacyStatus()` method. After the privacy setting is changed by using this method, the change is permanent until it is changed again using this method, or the app is completely uninstalled and reinstalled. 



>[!TIP]
>
>Media heartbeat tracking calls are also disabled if the privacy status is set to opt-out.

If the user wants to opt-in, set the privacy status to ` PRIVACY_STATUS_OPT_IN`: 
```
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
```


If the user wants to opt-out, set the privacy status to ` PRIVACY_STATUS_OPT_OUT`: 
```
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
```


This method will return the current value for privacy constant:


```
ADBMobile.config.getPrivacyStatus()
```

