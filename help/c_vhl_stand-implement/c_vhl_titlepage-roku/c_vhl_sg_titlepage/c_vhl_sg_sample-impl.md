---
description: null
seo-description: null
seo-title: Sample Implementation
title: Sample Implementation
uuid: 97f9a0b2-34c5-4f31-9b6a-e1ed697af836
index: y
internal: n
snippet: y
translate: y
---

# Sample Implementation


## Legacy SDK {#section_x4k_vny_1bb}

**Sample API calls on Legacy SDK**


```
'get an instance of SDK
m.adbmobile = ADBMobile()
  
'execute setter APIs
m.adbmobile.setDebugLogging(true)
  
'execute getter APIs
debugLogging = m.adbmobile.getDebugLogging()
```


## SceneGraph SDK {#section_d1f_vny_1bb}

**Sample API calls on SG SDK**


```
'create adbmobileTask instance
m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
  
'get an instance of SDK using task instance
m.adbmobile = 
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask)
m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
'execute setter APIs
m.adbmobile.setDebugLogging(true)
 
'execute getter APIs
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE, 
                              "onAdbmobileApiResponse")
m.adbmobile.getDebugLogging()
  
'listen for return data in registered callbacks
function onAdbmobileApiResponse() as void
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
 
        if responseObject <> invalid
            methodName = responseObject.apiName
            retVal = responseObject.returnValue
 
        if methodName = m.adbmobileConstants.DEBUG_LOGGING
            if retVal
                print "API Response: DEBUG LOGGING: " + "True"
            else
                print "API Response: DEBUG LOGGING: " + "False"
         endif
    endif
end function
```

