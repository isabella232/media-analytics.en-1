---
description: null
seo-description: null
seo-title: Set User IDs (OTT apps)
title: Set User IDs (OTT apps)
uuid: 4cde4745-9b04-428b-bd0e-572c39766c2d
index: y
internal: n
snippet: y
translate: y
---

# Set User IDs (OTT apps)

The user ID is a unique custom visitor identifier defined by the application for a user.

Set and get the unique user ID on the ADBMobile SDK as follows:


1. Set - 
    * Roku -     
      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

    * Chromecast -     
      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```


1. Get - 
    * Roku -     
      ```
      vid = ADBMobile().userIdentifer()
      ```

    * Chromecast -     
      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```



