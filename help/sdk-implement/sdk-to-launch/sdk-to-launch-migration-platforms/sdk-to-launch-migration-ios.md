---
title: "Migrating from the Standalone Media SDK to Adobe Launch - iOS"
description: Learn how to migrate from the Media SDK to Launch for iOS.
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Migrating from the standalone Media SDK to Adobe Launch - iOS

>[!NOTE]
>Adobe Experience Platform Launch has been rebranded as a suite of data collection technologies in Experience Platform. Several terminology changes have rolled out across the product documentation as a result. Please refer to the following [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) for a consolidated reference of the terminology changes.

## Configuration

### Standalone Media SDK

In the standalone Media SDK, you configure the tracking configuration in the app,
and pass it to the SDK when you create the tracker.

```objective-c
ADBMediaHeartbeatConfig *config =
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### Launch Extension

1. In Experience Platform Launch, click the [!UICONTROL Extensions] tab for your mobile property
1. On the [!UICONTROL Catalog] tab, locate the Adobe Media Analytics for Audio and Video extension, and click [!UICONTROL Install].
1. In the extension settings page, configure the tracking parameters.
    The Media extension will use the configured parameters for tracking.

    ![](assets/launch_config_mobile.png)

[Configure the Media Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Tracker Creation

### Standalone Media SDK

In the standalone Media SDK you manually create the `ADBMediaHeartbeatConfig` object
and configure the tracking parameters. Implement the delegate interface exposing the
`getQoSObject()` and `getCurrentPlaybackTime()functions.`

Create a MediaHeartbeat instance for tracking:

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Launch Extension

[Media API reference - Create Media Tracker](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Before creating the tracker, register the media extension and dependent extensions with the mobile core.

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

Once the media extension is registered, tracker can be created using the following API.
The tracker automatically picks the configuration from the configured launch property.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## Updating Playhead and Quality of Experience values.

### Standalone Media SDK

In the standalone Media SDK, a delegate object that implements the
`ADBMediaHeartbeartDelegate` protocol is passed during tracker creation.
The implementation should return the latest QoE and playhead whenever the
tracker calls the `getQoSObject()` and `getCurrentPlaybackTime()` interface
methods.

### Launch Extension

The implementation should update the current player playhead by called the
`updateCurrentPlayhead` method exposed by the tracker. For accurate tracking
you should call this method at least once per second.

[Media API reference - Update Current Playhead](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

The implementation should update the QoE information by calling the
`updateQoEObject` method exposed by the tracker. You should call this method
whenever there is a change in the quality metrics.

[Media API reference - Update QoE Object](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Passing standard media / ad metadata

### Standalone Media SDK

* Standard Media Metadata:

   ```objective-c
   ADBMediaObject *mediaObject =
     [ADBMediaHeartbeat createMediaObjectWithName:@"media-name"
                        mediaId:@"media-id"
                        length:60
                        streamType:ADBMediaHeartbeatStreamTypeVod
                        mediaType:ADBMediaTypeVideo];

   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
   [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
   [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];

   //Attaching custom metadata
   NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];

   [tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standard Ad Metadata:

   ```objective-c
   ADBMediaObject* adObject =
     [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"]
                        adId:[adData objectForKey:@"id"]
                        position:[[adData objectForKey:@"position"] doubleValue]
                        length:[[adData objectForKey:@"length"] doubleValue]];

   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata =
     [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample Advertiser"
                     forKey:ADBAdMetadataKeyADVERTISER];
   [standardMetadata setObject:@"Sample Campaign"
                     forKey:ADBAdMetadataKeyCAMPAIGN_ID];
   [adObject setValue:standardMetadata
                     forKey:ADBMediaObjectKeyStandardAdMetadata];

   //Attaching custom metadata
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];

   [tracker trackEvent:ADBMediaHeartbeatEventAdStart
            mediaObject:adObject
            data:adDictionary];
   ```

### Launch Extension

* Standard Media Metadata:

   ```objective-c
   NSDictionary *mediaObject =
     [ACPMedia createMediaObjectWithName:@"media-name"
               mediaId:@"media-id"
               length:60
               streamType:ACPMediaStreamTypeVod
               mediaType:ACPMediaTypeVideo];

   NSMutableDictionary *mediaMetadata =
     [[NSMutableDictionary alloc] init];

   // Standard metadata keys provided by adobe.
   [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
   [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];

   // Custom metadata keys
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   [_tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standard Ad Metadata:

   ```objective-c
   NSDictionary* adObject =
     [ACPMedia createAdObjectWithName:@"ad-name"
               adId:@"ad-id"
               position:1
               length:15];

   NSMutableDictionary* adMetadata =
     [[NSMutableDictionary alloc] init];

   // Standard metadata keys provided by adobe.
   [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
   [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];

   // Custom metadata keys
   [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];

   [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
   ```
