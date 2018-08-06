---
description: The following steps are to be performed in your Xcode project. This guide is written assuming your project has a target that is an Apple TV app targeting tvOS.
seo-description: The following steps are to be performed in your Xcode project. This guide is written assuming your project has a target that is an Apple TV app targeting tvOS.
seo-title: Configure a Native App for tvOS
title: Configure a Native App for tvOS
uuid: 984a011d-681d-4375-a8ec-80ec13d0312c
index: y
internal: n
snippet: y
translate: y
---

# Configure a Native App for tvOS

For more information about tvOS, see [tvOS Developer site](https://developer.apple.com/tvos/documentation/). 

>1. Drag the `VideoHeartbeat_TV.a` library file into your project’s lib folder.
>1. In the Build Phases tab of your tvOS app’s target, expand the ** `Link Binary with Libraries` ** section and add the following libraries:
>    
>    * `VideoHeartbeat_TV.a`
>    * `AdobeMobileLibrary_TV.a`
>    * `libsqlite3.0.tbd`
>    * `SystemConfiguration.framework`
>    
