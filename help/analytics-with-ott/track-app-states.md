---
description: null
seo-description: null
seo-title: Track App States (OTT apps)
title: Track App States (OTT apps)
uuid: cf5a2a42-12ca-440a-864c-7e45be74681d
index: y
internal: n
snippet: y
translate: y
---

# Track App States (OTT apps)

States are the different screens or views in your application. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the video details screen, you should send a ` trackState` call. 

` trackState` is typically called each time a new screen is loaded. 
* **Roku -** 
  ```
  ADBMobile().trackState("State Name", {})
  ```

* **Chromecast -** 
  ```
  ADBMobile.analytics.trackState("State Name",{});
  ```

The state name is reported in the ` View State` variable in Adobe Mobile services, and a view is recorded for each ` trackState` call. In other Analytics interfaces, ` View State` is reported as ` Page Name` and ` state views` is reported as ` page views`. 

In addition to the ` State Name`, you can send additional context data with each track action call: 
* **Roku -** 
  ```
  dictionary = { } 
  dictionary["myapp.login.LoginStatus"] = "logged in"  
  ADBMobile().trackState("Home Screen", dictionary)
  ```

* **Chromecast -** 
  ```
  var dictionary = { }; 
  dictionary["myapp.login.LoginStatus"] = "logged in"; 
  ADBMobile.analytics.trackState("Home Screen", dictionary); 
  
  ```




>[!NOTE]
>
>Context data values must be mapped to custom variables in Adobe Mobile services.



States are typically viewed by using a pathing report, so you can see how users navigate your app and which states are most commonly viewed. 
