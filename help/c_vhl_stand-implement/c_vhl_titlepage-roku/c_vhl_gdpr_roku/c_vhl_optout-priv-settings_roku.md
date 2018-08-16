---
description: null
seo-description: null
seo-title: Opt-Out and Privacy Settings
title: Opt-Out and Privacy Settings
uuid: 65edaf10-55cb-473e-b545-663efb7a0285
index: y
internal: n
snippet: y
translate: y
---

# Opt-Out and Privacy Settings

You can control whether or not Analytics data is sent on a specific device using the following settings: 
* The ` privacyDefault` setting in the ` ADBMobile.json` config file. This setting controls the initial setting that persists until it is changed in code. 

* The ` ADBMobile().setPrivacyStatus()` method. After the privacy setting is changed by using this method, the change is permanent until it is changed again using this method, or the app is completely uninstalled and reinstalled. 



>[!TIP]
>
>Media heartbeat tracking calls are also disabled if the privacy status is set to opt-out.

If the user wants to opt-in or opt-out, set the privacy status to ` PRIVACY_STATUS_OPT_IN` or ` PRIVACY_STATUS_OPT_OUT` with this method. For example, if the user wants to opt out: 
```
ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
```



>[!IMPORTANT]
>
>When a user opts out of tracking, all of the persisted device data and IDs will be purged until the user opts back in.



This method will return the current value for the privacy constant ` (ADBMobile().PRIVACY_STATUS_OPT_IN` or ` ADBMobile().PRIVACY_STATUS_OPT_OUT)`: 


```
ADBMobile().getPrivacyStatus()
```

