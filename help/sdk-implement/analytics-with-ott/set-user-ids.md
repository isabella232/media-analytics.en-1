---
description: null
seo-description: null
seo-title: Set User IDs
title: Set User IDs
uuid: 0ae0c2a6-aef8-4d7f-9c76-dcfd25be771c
index: y
internal: n
snippet: y
translate: y
---

# Set User IDs

The user ID is a unique custom visitor identifier defined by the application for a user.

Set and get the unique user ID on the ADBMobile SDK as follows:

1. **Set:**

    * **Roku -** 
    
      ```    
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

    * **Chromecast -** 
    
      ```    
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

1. **Get:**

    * **Roku -** 
    
      ```    
      vid = ADBMobile().userIdentifer()
      ```

    * **Chromecast -** 
    
      ```    
      vid = ADBMobile().config.getUserIdentifer();
      ```

