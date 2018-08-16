---
description: null
seo-description: null
seo-title: Implement the SceneGraph AdobeMobile SDK
title: Implement the SceneGraph AdobeMobile SDK
uuid: bdfeeb23-35f6-4921-9b2d-0fcd64ae255f
index: y
internal: n
snippet: y
translate: y
---

# Implement the SceneGraph AdobeMobile SDK

This is a step by step guide to help you with implementing AdobeMobile SDK with SceneGraph support in your application.

>1. **Download the Roku Library**
>   Download the latest Roku library from [ https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases).
>
>1. **Set Up Your Development Environment**
>
>   >1. Copy [!DNL  adbmobile.brs] (AdobeMobileLibrary) into your [!DNL  pkg:/source/] directory.
>   >1. For Scene Graph support, copy [!DNL  adbmobileTask.brs] and [!DNL  adbMobileTask.xml] into your [!DNL  pkg:/components/] directory.
>1. **Initialize**
>   >1. Import [!DNL  adbmobile.brs] into your Scene.
>   >
>   >   ```
>   >   &amp;lt;script&amp;nbsp;type="text/brightscript"&amp;nbsp;uri="pkg:/source/adbmobile.brs"&amp;nbsp;/&amp;gt;
>   >   ```

>   >
>   >1. Create an instance of ` adbmobileTask` node into your Scene.
>   >
>   >   ```
>   >   m.adbmobileTask&amp;nbsp;=&amp;nbsp;createObject("roSGNode",&amp;nbsp;"adbmobileTask")
>   >   ```
>   >
>   >1. Get an instance of ` adbmobile` connector for SceneGraph using the ` adbmobileTask` instance.
>   >
>   >   ```
>   >   m.adbmobile&amp;nbsp;=&amp;nbsp;ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
>   >   ```
>   >
>   >1. Get ` adbmobile` SG constants.
>   >
>   >   ```
>   >   m.adbmobileConstants&amp;nbsp;=&amp;nbsp;m.adbmobile.sceneGraphConstants()
>   >   ```
>   >
>   >1. Register a callback for receiving response object for all ` AdbMobile` API calls.
>   >
>   >   ```
>   >   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
>   >                                "onAdbmobileApiResponse") 
>   >      
>   >   ' Sample implementation of the callback 
>   >   ' Listen for all the constants for which API calls are made on the SDK 
>   >   function onAdbmobileApiResponse() as void 
>   >       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
>   >     
>   >       if responseObject <> invalid 
>   >           methodName = responseObject.apiName 
>   >           retVal = responseObject.returnValue 
>   >    
>   >           if methodName = m.adbmobileConstants.DEBUG_LOGGING 
>   >               if retVal 
>   >                   print "API Response: DEBUG LOGGING: " + "True" 
>   >               else 
>   >                   print "API Response: DEBUG LOGGING: " + "False" 
>   >               endif 
>   >           else if methodName = m.adbmobileConstants.PRIVACY_STATUS 
>   >               print "API Response: PRIVACY STATUS: " + retVal 
>   >           else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER 
>   >               if retVal <> invalid 
>   >                   print "API Response: TRACKING IDENTIFIER: " + retVal 
>   >               else 
>   >                   print "API Response: TRACKING IDENTIFIER: " + "invalid" 
>   >               endif 
>   >           else if methodName = m.adbmobileConstants.USER_IDENTIFIER 
>   >               if retVal <> invalid 
>   >                   print "API Response: USER IDENTIFIER: " + retVal 
>   >               else 
>   >                   print "API Response: USER IDENTIFIER: " + "invalid" 
>   >               endif 
>   >           else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID 
>   >               if retVal <> invalid 
>   >                   print "API Response: MCID: " + retVal 
>   >               else 
>   >                   print "API Response: MCID: " + "invalid" 
>   >               endif 
>   >           else if methodName = m.adbmobileConstants.AUDIENCE_DPID 
>   >               if retVal <> invalid 
>   >                   print "API Response: AUDIENCE DPID: " + retVal 
>   >               else 
>   >                   print "API Response: AUDIENCE DPID: " + "invalid" 
>   >               endif 
>   >           else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID 
>   >               if retVal <> invalid 
>   >                   print "API Response: AUDIENCE DPUUID: " + retVal 
>   >               else 
>   >                   print "API Response: AUDIENCE DPUUID: " + "invalid" 
>   >               endif 
>   >           else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE 
>   >               if retVal <> invalid 
>   >                   print "API Response: AUDIENCE VISITOR PROFILE: Valid Object" 
>   >               else 
>   >                   print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid" 
>   >               endif 
>   >           endif 
>   >       endif 
>   >   end function 
>   >   
>   >   ```
>   >
