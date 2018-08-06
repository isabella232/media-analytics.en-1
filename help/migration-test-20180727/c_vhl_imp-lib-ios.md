---
description: After you download the iOS SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes, and so on.
seo-description: After you download the iOS SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes, and so on.
seo-title: Implement the iOS library
title: Implement the iOS library
uuid: c5c072a7-ffc7-42a5-8847-b034e97b975f
index: y
internal: n
snippet: y
translate: y
---

# Implement the iOS library


## Get the iOS SDK {#section_981B07C536984D4A9974BDC1DC79C348}


>[!IMPORTANT]
>
>Before you get the SDK, you must set up a mobile SDK and download the Video Heartbeat SDK. For more information, see[Getting started in iOS](r_vhl_getting-started-ios.md#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD). 


1. Expand the `VideoHeartbeatLibrary-ios-tvos-v2.*.zip`. For more information about downloading this file, see [Getting started in iOS](r_vhl_getting-started-ios.md#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD). 

1. Verify that the following software components exist in the `libs` directory: 
    * `ADBMediaHeartbeat.h`: The Objective-C header file that is used for iOS video heartbeat tracking APIs.
    * `ADBMediaHeartbeatConfig.h`: The Objective-C header file for the SDK configuration.
    * `VideoHeartbeat.a`: A bitcode-enabled fat binary that contains the library builds for iOS devices (armv7, armv7s, arm64) and simulators (i386 and x86_64). This binary should be linked when target is intended for an iOS app.

    * `VideoHeartbeat_TV.a`: A bitcode-enabled fat binary containing the library builds for new Apple TV devices (arm64) and simulator (x86_64). This binary should be linked when the target is intended for an Apple TV (tvOS) app.

   This library is used with iOS devices and simulators for video heartbeat tracking APIs.



## Add the SDK to your project {#section_DEFD46C0B505480B903B193C84D327B6}

To add the SDK to your project: 
1. Launch the Xcode IDE and open your app.
1. In ** `Project Navigator` **, drag the `libs` directory and drop it under your project.
1. Ensure that the ** `Copy Items if Needed` ** checkbox is selected, the ** `Create Groups` ** is selected, and none of the checkboxes in ** `Add to Target` ** are selected. <a id="fig_7D00471EC1C6429885025702767E2C10"></a> ![](graphics/choose-options_ios.png) 

1. Click ** `Finish` **.
1. In ** `Project Navigator` **, select your app and select your targets.
1. Link the required frameworks and libraries in the ** `Linked Frameworks` ** and ** `Libraries` ** section on the ** `General` ** tab: 
    * ** `iOS App Targets` ** <a id="fig_4CBCBA481EBB4D539412D33C43BD5AEC"></a> ![](graphics/proj_nav_ios-app.png) 

    * ** `Apple TV (tvOS) Target` **: <a id="fig_317077787FB24101A306482E39A80C7D"></a> ![](graphics/proj_nav_apple-tv.png) 
    
        * ** `AdobeMobileLibrary_TV.a` **
        * ** `VideoHeartbeat_TV.a` **
        * ** `libsqlite3.0.tbd` **
        * ** `SystemConfiguration.framework` **


1. Verify that your app builds without errors.

