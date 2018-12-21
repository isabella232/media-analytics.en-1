---
seo-title: DTVR/MTVR implementation
title: DTVR/MTVR implementation
uuid: eda6e89e-67e4-4196-9842-703b8a025ade

---

# DTVR/MTVR implementation{#dtvr-mtvr-implementation}

Digital Television Ratings (DTVR) and Mobile Television Ratings (MTVR) are Nielsen products that measure live TV viewing up to seven days of broadcasting without a change in national ads.

To implement DTVR, make the following changes to the Nielsen plug-in in the Adobe Media SDK:

>[!TIP]
>
>The process is the same for Desktop, iOS, and Android.

## Set up {#section_4818BF40EA914BB79074FFFF8112C7A5}

Verify that your VA config key for the Nielsen integration includes DTVR support. If your config key does not include DTVR support, contact your Adobe representative to obtain a new config key that is specific to DTVR.

In addition to having your config key enabled for DTVR support, ensure you have a Nielsen appID for DTVR measurement. If you do not have or are unsure what appID's are assigned for the DTVR integration, contact your Technical Account Manager.

>[!NOTE]
>
>Use Charles to capture the DTVR logs.

## Development {#section_27A14B87CE954BB38D5CABC13339EA62}

To implement DTVR, see the implementation guide for your platform and version.

## Testing {#section_40F0C6EF84BC48268A920EB1EF218944}

Although you can use Adobe Debug to validate your Adobe and Nielsen calls, the tool is not yet optimized for DTVR because Adobe-collected data is not used by Nielsen for DTVR. You can only use the data that is collected directly by Nielsen from the combined SDK for DTVR.

**Adobe validation**

Here is some information to remember for Adobe validations:

* For validating DTVR-related Video Analytics heartbeat data, ensure that the `adload` flag is set to `1`.

  This value ensures that the Adobe data is not sent to Nielsen for DCR crediting. 

* Validate that VA heartbeat data is tracking as expected for live/linear video measurement to Adobe.

**Nielsen validation**

* Validating Nielsen calls includes using an ID3 variable (see below) (a long string of encoded text).

  This string does not include the typical DCR Nielsen variables. 

* Video Summary comparisons are not included in DTVR for the following reasons:

    * Adobe data is not used. 
    * Nielsen variables are tied to ID3, which is not yet decoded in the Debug tool.

**Standard video playback (DTVR) example**

1. Enable a packet monitoring program on the same network as the device that is running the DTVR application.

   You can use, for example, Charles/Fiddler. 
1. Load the page or app. 
1. Start the video player. 
1. Press the play button to play video content. 
1. When the video is loaded, verify that `trackVideoLoad()` is called. 
1. After the content starts playing:

    * Verify that `trackPlay()` is called. 
    * Verify that `trackTimedMetadata()` is called.

      When timed metadata objects are received with a PRIV key, the value of the key is sent to the `trackTimedMetadata()` API.

1. On completion of video playback, verify that `trackComplete()` is called. 
1. Verify that measurement pings are sent properly.

## ID3 example {#section_555F58E071C6409BBBB4EFF74290D714}

ID3 tags have a payload of approximately 249 characters and start with `www.nielsen.com`.

See [https://id3.org](https://id3.org) for comprehensive information on ID3 tags.
