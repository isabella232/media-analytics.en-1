---
title: Set User IDs
description: APIs for setting user IDs, which server as a unique customer identifier.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Media Analytics, API"
role: Business Practitioner, Administrator, Data Engineer
---
# Set user IDs{#set-user-ids}

The user ID is a unique custom visitor identifier defined by the application for a user.

Set and get the unique user ID on the ADBMobile SDK as follows:

* **Set:**

   * **Roku:** 
   
      ```    
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```
   
   * **Chromecast:** 
   
      ```    
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Get:**

   * **Roku:** 
   
      ```    
      vid = ADBMobile().userIdentifer()
      ```
   
   * **Chromecast:** 
   
      ```    
      vid = ADBMobile().config.getUserIdentifer();
      ```
