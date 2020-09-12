---
product: Media Analytics
audience: end-user
user-guide-title: Adobe Analytics for Audio and Video
breadcrumb-title: Media Analytics Guide
user-guide-description: Implement Analytics on audio or video sources. Includes the Media SDK and the Media Collection API.
product: adobe analytics
sub-product: media analytics
---

# Adobe Analytics for Audio and Video {#using}

+ [Measuring Audio and Video in Adobe Analytics](media-overview.md)
+ [Supported Devices and Platforms](measurement-options/supported-devices.md)
+ Introduction to Audio and Video Analytics {#intro-to-ava}  
    + [Prerequisites](intro-to-ava/prereqs.md)
    + Implementation Paths {#implementation-paths}
        + [Overview](intro-to-ava/implementation-paths/implementation-paths.md)
        + [Client-side](intro-to-ava/implementation-paths/client-side-path.md)
        + Other Implementation Paths {#other-paths}
            + Media Module Milestone Tracking {#mm-milestone-tracking}
                + [Milestone Overview](measurement-options/mm-milestone-tracking/milestone-overview.md)
                + [Migrate Milestone to Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
                + [Migrating from Milestone to Custom Link](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
            + Custom Link in Analytics {#cl-in-aa}
                + [Custom Link Implementation Guide](measurement-options/cl-in-aa/cl-impl-guide.md)
            + Primetime {#primetime}
                + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
            + [Audience Manager Enablement](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
    + [Media Analytics SDK End-of-Support FAQs](sdk-implement/end-of-support-faqs.md)
    + [Download SDKs](sdk-implement/download-sdks.md)
    + Set up and Configure {#setup}
        + [Overview](sdk-implement/setup/setup-overview.md)
        + [Set up Android](sdk-implement/setup/set-up-android.md)
        + [Set up iOS](sdk-implement/setup/set-up-ios.md)
        + Set up JavaScript {#setup-javascript}
            + [Set up JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
            + [Set up JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
        + [Set up Chromecast](sdk-implement/setup/set-up-chromecast.md)
        + [Set Up Roku](sdk-implement/setup/set-up-roku.md)
    + Track Audio and Video Playback {#track-av-playback}
        + [Overview](sdk-implement/track-av-playback/track-core-overview.md)
        + Track Core Audio and Video Playback {#track-core}
            + [Track Core Playback on Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
            + [Track Core Playback on iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
            + Track Core Playback on JavaScript {#track-core-javascript}
                + [Track Core Playback on JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
                + [Track Core Playback on JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
            + [Track Core Playback on Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
            + [Track Core Playback on Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
        + Track Buffering {#track-buffering}
            + [Track Buffering on Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
            + [Track Buffering on iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
            + Track Buffering on JavaScript {#track-buffering-js}
                + [Track Buffering on JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
                + [Track Buffering on JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
            + [Track Buffering on Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
            + [Track Buffering on Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
        + Track Seeking {#track-seeking}
            + [Track Seeking on Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
            + [Track Seeking on iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
            + Track Seeking on JavaScript {#track-seeking-js}
                + [Track Seeking on JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
                + [Track Seeking on JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
            + [Track Seeking on Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
            + [Track Seeking on Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
        + Implement Standard Metadata {#impl-std-metadata}
            + [Implement standard metadata on Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
            + [Implement standard metadata on iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
            + [iOS Metadata Keys](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
            + Implement Standard Metadata on JavaScript {#impl-std-md-js}
                + [Implement standard metadata on JavaScript 2.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
                + [Implement standard metadata on JavaScript 3.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
            + [Implement standard metadata on Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
            + [Standard Metadata Parameters - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
            + [Implement standard metadata on Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
            + [Standard Metadata Parameters - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
    + Track Ads {#track-ads}
        + [Overview](sdk-implement/track-ads/track-ads-overview.md)
        + [Track Ads on Android](sdk-implement/track-ads/track-ads-android.md)
        + [Track Ads on iOS](sdk-implement/track-ads/track-ads-ios.md)
        + Track Ads on JavaScript {#track-ads-js}
            + [Track Ads on JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
            + [Track Ads on JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
        + [Track Ads on Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
        + [Track Ads on Roku](sdk-implement/track-ads/track-ads-roku.md)
        + Implement Standard ad Metadata {#impl-std-ad-metadata}
            + [Implement standard ad metadata on Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Implement standard ad metadata on iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Implement Standard ad Metadata on JavaScript {#impl-std-ad-md-js}
                + [Implement standard ad metadata on JavaScript 2.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
                + [Implement standard ad metadata on JavaScript 3.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
            + [Implement standard ad metadata on Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
    + Track Chapters and Segments {#track-chapters}
        + [Overview](sdk-implement/track-chapters/track-chapters-overview.md)
        + [Track Chapters and Segments on Android](sdk-implement/track-chapters/track-chapters-android.md)
        + [Track Chapters and Segments on iOS](sdk-implement/track-chapters/track-chapters-ios.md)
        + Track Chapters and Segments on JavaScript {#track-chapters-js}
            + [Track Chapters and Segments on JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
            + [Track Chapters and Segments on JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
        + [Track Chapters and Segments on Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
        + [Track Chapters and Segments on Roku](sdk-implement/track-chapters/track-chapters-roku.md)
    + Track Quality of Experience {#track-qos}
        + [Overview](sdk-implement/track-qos/track-qos-overview.md)
        + [Track Quality of Experience on Android](sdk-implement/track-qos/track-qos-android.md)
        + [Track Quality of Experience on iOS](sdk-implement/track-qos/track-qos-ios.md)
        + Track Quality of Experience on JavaScript {#track-qos-js}
            + [Track Quality of Experience on JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
            + [Track Quality of Experience on JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
        + [Track Quality of Experience on Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
        + [Track Quality of Experience on Roku](sdk-implement/track-qos/track-qos-roku.md)
    + Track Errors {#track-errors}
        + [Overview](sdk-implement/track-errors/track-errors-overview.md)
        + [Track Errors on Android](sdk-implement/track-errors/track-errors-android.md)
        + [Track Errors on iOS](sdk-implement/track-errors/track-errors-ios.md)
        + Track Errors on JavaScript {#track-errors-js}
            + [Track Errors on JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
            + [Track Errors on JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
        + [Track Errors on Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
        + [Track Errors on Roku](sdk-implement/track-errors/track-errors-roku.md)
    + [Opt-out and Privacy](sdk-implement/opt-out-privacy.md)
    + Tracking Scenarios {#tracking-scenarios}
        + [VOD playback with no ads](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
        + [VOD playback with pre-roll ads](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
        + [VOD playback with skipped ads](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
        + [VOD playback with one chapter](sdk-implement/tracking-scenarios/vod-one-chapter.md)
        + [VOD playback with a skipped chapter](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
        + [VOD playback with seeking in the main content](sdk-implement/tracking-scenarios/vod-seeking.md)
        + [VOD playback with buffering](sdk-implement/tracking-scenarios/vod-buffering.md)
        + [VOD multiple trackers in parallel](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
        + [VOD one tracker for multiple sessions](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
        + [Live main content](sdk-implement/tracking-scenarios/live-main-content.md)
        + [Live main content with sequential tracking](sdk-implement/tracking-scenarios/live-sequential.md)
    + Validation {#validation}
        + [Validation Overview](sdk-implement/validation/validation-overview.md)
        + [Test 1: Standard Playback](sdk-implement/validation/test1-standard-playback.md)
        + [Test 2: Media Interruption](sdk-implement/validation/test2-media-interrupt.md)
        + [Test Call Details](sdk-implement/validation/test-call-details.md)
        + [Heartbeat Parameter Descriptions](sdk-implement/validation/heartbeat-params.md)
        + Debugging {#debugging}
            + [SDK Debugging](sdk-implement/validation/debugging/sdk-debugging.md)
            + [Configure Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
            + [Create a New Debug Report](sdk-implement/validation/debugging/create-new-debug-report.md)
            + [Debug Dashboards and Reports](sdk-implement/validation/debugging/debug-dash-repts.md)
    + Analytics in OTT Apps {#analytics-with-ott}
        + [Track App States](sdk-implement/analytics-with-ott/track-app-states.md)
        + [Track App Actions](sdk-implement/analytics-with-ott/track-app-actions.md)
        + [Set User IDs](sdk-implement/analytics-with-ott/set-user-ids.md)
        + [OTT and Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
        + [OTT and Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
    + Cookbook {#cookbook}
        + [SDK Cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
        + [Handling application interrupts during playback](sdk-implement/cookbook/app-interrupts.md)
        + [Resolving main:play appearing between ads](sdk-implement/cookbook/fix-ad-play-ad.md)
        + [Resuming Inactive Sessions](sdk-implement/cookbook/resuming-inactive.md)
        + [Tracking in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
    + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
        + [Migration Overview](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
        + [Code Comparison: 1.x to 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
        + [1.x to 2.x API Conversion](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
    + Media Analytics SDK to Launch Migration {#sdk-to-launch}
        + [SDK to Launch Migration](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
        + SDK to Launch Migration Platform Guides {#sdk-to-launch-migration-platforms}
            + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
            + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
            + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
    + [Overview](media-collection-api/mc-api-overview.md)
    + API Reference {#mc-api-ref}
        + [Sessions Request](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
        + [Events Request](media-collection-api/mc-api-ref/mc-api-events-req.md)
        + [Request Parameters](media-collection-api/mc-api-ref/mc-api-req-params.md)
        + [Event Types and Descriptions](media-collection-api/mc-api-ref/mc-api-event-types.md)
        + [JSON Validation Schemas](media-collection-api/mc-api-ref/mc-api-json-validation.md)
    + Implementing the API {#mc-api-impl}
        + [Quick Start](media-collection-api/mc-api-impl/mc-api-quick-start.md)
        + [Setting the HTTP Request Type in Your Player](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
        + [Obtaining a Session ID](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
        + [Implementing an Events Request](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
        + [Validating Event Requests](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
        + [Sending Ping Events](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
        + [Sending QoE Data](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
        + [Custom Metadata Support](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
        + [Timeout Conditions](media-collection-api/mc-api-impl/mc-api-timeout.md)
        + [Controlling the Order of Events](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
        + [Queueing Events When Sessions Response is Slow](media-collection-api/mc-api-impl/mc-api-queuing.md)
    + Media Tracking Timelines {#mc-api-timelines}
        + [Timeline 1 - View to end of content](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
        + [Timeline 2 - User abandons session](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
        + [Timeline 3 - Chapters](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Cookbook {#media-analytics-cookbook}
    + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
    + [Media Stream Attribution](media-analytics-cookbook/media-dimensions.md)
+ Metrics and Metadata {#metrics-and-metadata}
    + [Audio and Video Parameters](metrics-and-metadata/audio-video-parameters.md)
    + [Ad parameters](metrics-and-metadata/ad-parameters.md)
    + [Chapter Parameters](metrics-and-metadata/chapter-parameters.md)
    + [Player State Parameters](metrics-and-metadata/player-state-parameters.md)
    + [Quality Parameters](metrics-and-metadata/quality-parameters.md)
    + [Segments](metrics-and-metadata/segments.md)
    + [Calculated Metrics](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}  
    + [Media Reports Enablement](media-reports/media-reports-enable.md)
    + Media Default Reports {#media-default-reports}  
        + [Default Reports Overview](media-reports/media-default-reports/default-reports-overview.md)
        + [Media Overview](media-reports/media-default-reports/media-reports-overview.md)  
        + [Media Detail](media-reports/media-default-reports/media-reports-detail.md)  
        + [Media Daypart report](media-reports/media-default-reports/media-reports-daypart.md)  
        + [Media Concurrent Viewers report](media-reports/media-default-reports/media-concurrent-viewers.md)
    + Media Workspace Panels {#media-workspace-panels}  
        + [Media Concurrent Viewers panel](media-reports/media-workspace-panels/media-concurrent-viewers.md)
    + [Media Workspace Templates](media-reports/media-workspace-templates.md)
    + [Get Concurrent Viewers Data via API](media-reports/media-default-reports/get-concurrent-json20.md)
+ [Track Downloaded Content](media-collection-api/track-downloaded-content.md)
+ [Federated Analytics](federated-analytics.md)
+ Player State Tracking {#player-state-tracking}
    + [Overview](sdk-implement/player-state-tracking/player-state-overview.md)
    + [Standard and custom states](sdk-implement/player-state-tracking/standard-and-custom-states.md)
    + [Implementation and reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
    + [Player state tracking examples](sdk-implement/player-state-tracking/player-state-examples.md)
+ Additional resources {#additional-resources}
    + [Release Notes](additional-resources/doc-updates.md)
