---
description: After you download the Android SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes, and so on.
seo-description: After you download the Android SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes, and so on.
seo-title: Implement the Android library
title: Implement the Android library
uuid: c49df822-f21a-4231-9a7e-0aaebcf7b92d
index: y
internal: n
snippet: y
translate: y
---

# Implement the Android library


## Get the Android SDK {#section_981B07C536984D4A9974BDC1DC79C348}

Before you begin implementing heartbeat tracking in your application, you must set up a mobile SDK, and download the Video Heartbeat SDK. For more information, see the prerequisites in [Getting started on Android](r_vhl_getting-started-android.md#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD). 

1. Expand the `VideoHeartbeatLibrary-android-v2.*.zip` file that you downloaded. For information about downloading this file, see [Getting started on Android](r_vhl_getting-started-android.md#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD). 

1. Verify that the `VideoHeartbeat.jar` file exists in the `libs/` directory: This library is used with Android devices and simulators for video heartbeat tracking APIs.


## Add the SDK to your project {#section_DEFD46C0B505480B903B193C84D327B6}

To add the SDK to your project using IntelliJ IDEA:

1. Right click your project in the ** `Project navigation` ** panel.
1. Select ** `Open Module Settings` **.
1. Under ** `Project Settings` **, select ** `Libraries` **.
1. Click ** `+` ** to add a new library.
1. Select ** `Java` ** and navigate to the `VideoHeartbeat.jar` file.
1. Select the modules in which you plan to use the mobile library.
1. Click ** `Apply` ** and then ** `OK` ** to close the Module Settings window.
To add the SDK to your project using Eclipse:

1. In the Eclipse IDE, right-click on the project name.
1. Click ** `Build Path` ** > ** `Add External Archives` **.
1. Select `VideoHeartbeat.jar`.
1. Click ** `Open` **.
1. Right-click the project again, and click ** `Build Path` ** > ** `Configure Build Path` **.
1. Click the ** `Order` ** and ** `Export` ** tabs.
1. Ensure that the `VideoHeartbeat.jar` file is selected.

## Adding app permissions {#section_F25C35A43C944F3CB593609847861761}

The VideoHeartbeat Library requires the following permissions to send data in tracking calls:

* `INTERNET`
* `ACCESS_NETWORK_STATE`
To add these permissions, add the following lines to your `AndroidManifest.xml` file in the application project directory: 

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`
