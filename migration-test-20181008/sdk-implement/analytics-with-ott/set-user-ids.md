---
description: null
seo-description: null
seo-title: Set User IDs
title: Set User IDs
uuid: f9e06d1d-93e0-41a7-9195-e094f83fbeee
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

