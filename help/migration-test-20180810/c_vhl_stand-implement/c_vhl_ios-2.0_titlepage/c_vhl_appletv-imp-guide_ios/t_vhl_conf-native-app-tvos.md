---
description: The following steps are to be performed in your Xcode project. This guide is written assuming your project has a target that is an Apple TV app targeting tvOS.
seo-description: The following steps are to be performed in your Xcode project. This guide is written assuming your project has a target that is an Apple TV app targeting tvOS.
seo-title: Configure a Native App for tvOS
title: Configure a Native App for tvOS
uuid: d3bc5503-58d4-48b5-923d-bd930bb27929
index: y
internal: n
snippet: y
translate: y
---

# Configure a Native App for tvOS

For more information about tvOS, see [ tvOS Developer site](https://developer.apple.com/tvos/documentation/). 

>1. Drag the [!DNL  VideoHeartbeat_TV.a] library file into your project’s lib folder.
>1. In the Build Phases tab of your tvOS app’s target, expand the ** [!UICONTROL  Link Binary with Libraries] ** section and add the following libraries:
>    
>    * [!DNL  VideoHeartbeat_TV.a]
>    * [!DNL  AdobeMobileLibrary_TV.a]
>    * [!DNL  libsqlite3.0.tbd]
>    * [!DNL  SystemConfiguration.framework]
>    
