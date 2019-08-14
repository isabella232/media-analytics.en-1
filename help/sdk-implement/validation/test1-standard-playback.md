---
seo-title: Test 1  Standard playback
title: Test 1  Standard playback
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2

---

# Test 1: Standard playback{#test-standard-playback}

This test case validates general playback and sequencing. It is required as part of the Certification Request Form. 

**Download the certification request form here: ==>**&nbsp; [Certification Request Form.](cert_req_form.docx) 

Media implementations are composed of the following types of tracking calls:
* Media and Ad Start calls are sent directly to the AppMeasurement (Adobe Analytics) server. 
* Media Analytics heartbeat calls are sent on start and every ten seconds (for content) or one second (for ads) to the Media Analytics tracking server.

>[!NOTE]
>Media tracking behaves the same across all platforms.

You must complete and record these actions in the following order:

1. **Load the page or app**

    **Tracking Servers** (For all website and mobile apps):

    * **AppMeasurement (Adobe Analytics) -** An RDC tracking server or CNAME that resolves to an RDC tracking server is required for the Experience Cloud Visitor ID service. The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.     
    
    * **Media Analytics (Heartbeats) -** This server always has the format "`[namespace].hb.omtrdc.net`", where `[namespace]` specifies your company name. This name is provided by Adobe.

    You need to validate certain key variables that are universal across all tracking calls:

    **Adobe Visitor ID (`mid`):** The `mid` variable is used to capture the value set in the AMCV cookie. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. It is found in both AppMeasurement and Media Analytics calls.

    * **Media Analytics Play Call**

       |  Parameter | Value (sample) |
       |---|---|
       | `s:event:type` | play |
       | `s:user:mid` | 30250035503789876473484580554595324209 |
  
    * **Media Analytics Start Call**
  
       |  Parameter | Value (sample) |
       |---|---|
       | `pev2` | ms_s |
       | `mid` | 30250035503789876473484580554595324209 |
  
    * **Website Page Call**
  
       |  Parameter | Value (sample) |
       |---|---|
       | `mid` | 30250035503789876473484580554595324209 |
  
    * **Lifecycle Call**
  
       |  Parameter | Value (sample) |
       |---|---|
       | `pev2` | ADBINTERNAL:Lifecycle |
       | `mid` | 30250035503789876473484580554595324209 |
  
    * **Heartbeat Start Call**
  
       |  Parameter | Value (sample) |
       |---|---|
       | `s:event:type` | start |
  
    * **VA Start Call**
  
       >[!NOTE]
       >
       >On VA Start Calls (`s:event:type=start`) the `mid` values may not be present. This is OK. They may not appear until the VA Play Calls ( `s:event:type=play`).
  
       |  Parameter | Value (sample) |
       |---|---|
       | `pev2` | ms_s |

1. **Start the media player** 

    When the media player starts, the key calls are sent in the following order:

    1. Media analytics start
    1. Heartbeat start
    1. Heartbeat analytics start
 
    The first two calls above contain additional metadata and variables. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **View ad break if available**

    * **Ad Start**

    When the media ad starts, the following key calls are sent in the following order:

    1. Media ad analytics start
    1. Heartbeat ad start
    1. Heartbeat ad analytics start

    The first two calls contain additional metadata and variables. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

    * **Ad Play**

       During ad playback, Heartbeat calls are sent to the Heartbeat server every second. 
    
    * **Ad Complete**

       At the 100% point on a media ad, a Heartbeat complete call will be sent.

1. **Pause ad playback for 30 seconds, if available.**&nbsp; **Ad Pause**

    During ad pause, Heartbeat calls are sent to the Heartbeat server every second.

    >[!NOTE]
    >
    >The playhead value should remain constant during the pause.

1. **Play main content media for 10 minutes uninterrupted.**&nbsp; **Content Play**

    During main content playback, heartbeat calls are sent to the Media Analytics server every ten seconds.
 
    Notes:
 
     * The playhead position should increment by 10 with every play call.
     * The `l:event:duration` value represents the number of milliseconds since the last tracking call and should be roughly the same value on each 10 second call.
 
       For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **Pause during playback for at least 30 seconds.** On pause of the media player, pause event calls will be sent every 10 seconds. After pause ends the play events should resume. 

1. **Seek/scrub media.** On scrubbing of media playhead, no special tracking calls are sent, however, when media playback resumes after scrubbing the playhead value should reflect the new position within the main content. 

1. **Replay media (VOD only).** When media is replayed, a new set of media start calls should be sent, as if this is a fresh media view. 

1. **View next media in playlist.** On media start of the next media in a playlist, a new set of media start calls should be sent. 

1. **Switch media or stream.** When switching live streams, a Heartbeat complete call for the first stream should not be sent. The media start calls and media play calls should begin with the new show and stream name and with the correct playhead and duration values for the new show.

