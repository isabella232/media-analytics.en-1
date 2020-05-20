---
title: Media Analytics SDK End of Support FAQs
description: This topic includes FAQs about the end of support for Media Analytics SDKs.

---

# Media Analytics SDK End of Support FAQs

With the end of support for Version 4 Mobile SDKs on August 31, 2021, Adobe will also end support for the Media Analytics SDKs for iOS and Android. After August 31, 2021, Adobe will not provide fixes, OS-related updates, or support for the Media Analytics SDK.  During the process of migrating to these new Experience Platform SDKs, please keep in mind that the [Media Analytics extensions](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) must be implemented to enable Adobe Analytics for Audio and Video.

## Top 5 Things to Know

1. Mobile v4 SDKs will no longer be supported after August 31, 2021. You should migrate to the Adobe Experience Platform (AEP) SDKs for iOS and Android.

1. Analytics for Audio and Video implementation requires the AEP SDK and use of the Analytics and Media Analytics extensions. Starting September 1, 2021, you should use the new AEP SDKs and extensions.  Media Analytics extensions are configured using Adobe Launch.  For additional information, see [Migrating from Stand-Alone Media SDK to Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Feature development has ended for the Media Analytics SDKs for iOS and Android.  New features that were introduced beginning Fall 2019 are enabled using the Media Analytics extensions and the Media Collection API.

1. The Roku and Chromecast SDKs remain available for Analytics for Audio and Video customers. The Roku and Chromecast SDKs will continue to be enhanced and supported as stand-alone SDKs.  If you use the JS SDK for Media Analytics, you can continue to use the stand-alone SDK or enable the Media Analytics extension using Adobe Launch.

1. Prior to September 1, 2021, Adobe may, at its sole discretion, develop new fixes for problems of high technical impact or business exposure. Based on the customer input, Adobe will determine the degree of impact and exposure and the consequent activities.

After the end of support date, customers should use the new AEP SDKs with the Media Analytics extensions to use the latest features.

Please reach out to your Adobe Customer Success Manager if you have any questions.

## FAQs

1. **Will support for Roku and Chromecast SDKs be impacted?​**

   No.  Roku and Chromecast SDKs will continue to be supported as stand-alone SDKs for the time- being.​
​
1. **Will Media Analytics JS SDK implementations be impacted by this change?​**

   No.  Customers who use the JS SDK for Media Analytics can continue to use the SDK or enable it via Adobe Launch.
​
1. **What is the level of effort to migrate to the Media Analytics extensions?​**

   LOE depends on each customer’s implementation, so it will vary.  After reviewing the migration documentation below, please engage consulting and/or customer care for additional support.

    [Media Analytics Extensions: Android migration](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics Extensions: iOS migration](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics Extensions: new implementations](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Do I need to have Launch as a tag management system? What if I don't want to use Launch?**

   For mobile, Launch is required to configure the Media Extensions such as the Mobile Services UI. In the mobile app use case, it is not used as a tag management system.

1. **Does this end of support impact the SDK for tvOS?**

   Yes, for tvOS (version 10+) the recommended implementation is to migrate to the Media Analytics Extensions.  AEP SDK support and Media Analytics Extension support is planned for June 2020.  For additional information, see [Migrating from the standalone Media SDK to Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Does this end of support impact the SDK for FireTV and AndroidTV?​**

   Yes, for FireTV and AndroidTV,  the recommended implementation is to migrate to the Media Analytics Extensions.  AEP SDK support and Media Analytics Extension support is planned for June 2020.  For additional information, see [Migrating from the standalone Media SDK to Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
