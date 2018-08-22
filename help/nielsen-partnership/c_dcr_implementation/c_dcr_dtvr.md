---
description: Digital Television Ratings (DTVR) and Mobile Television Ratings (MTVR) are Nielsen products that measure live TV viewing up to seven days of broadcasting without a change in national ads.
seo-description: Digital Television Ratings (DTVR) and Mobile Television Ratings (MTVR) are Nielsen products that measure live TV viewing up to seven days of broadcasting without a change in national ads.
seo-title: DTVR/MTVR Implementation
title: DTVR/MTVR Implementation
uuid: 28b5e3ce-623a-4187-ac8b-3816c2a07dfc
index: y
internal: n
snippet: y
translate: y
---

# DTVR/MTVR Implementation

To implement DTVR, make the following changes to the Nielsen plug-in in the Adobe VA SDK: 

>[!TIP]
>
>The process is the same for Desktop, iOS, and Android.


## Set up {#section_4818BF40EA914BB79074FFFF8112C7A5}

Verify that your VA config key for the Nielsen integration includes DTVR support. If your config key does not include DTVR support, contact your Adobe representative to obtain a new config key that is specific to DTVR. 

In addition to having your config key enabled for DTVR support, ensure you have a Nielsen appID for DTVR measurement. If you do not have or are unsure what appID's are assigned for the DTVR integration, contact your Technical Account Manager. 

>[!NOTE] {type="note"}
>
>Use Charles to capture the DTVR logs.


## Development {#section_27A14B87CE954BB38D5CABC13339EA62}

To implement DTVR, see the following information for your platform: 


* [](c_dcr_impl-2.x-n.md)
* [](../../nielsen-partnership/c_dcr_implementation/c_dcr_impl-1.5-1.6/c_dcr_impl-1.5-1.6.md)


## Testing {#section_40F0C6EF84BC48268A920EB1EF218944}

Although you can use Adobe Debug to validate your Adobe and Nielsen calls, the tool is not yet optimized for DTVR because Adobe-collected data is not used by Nielsen for DTVR. You can only use the data that is collected directly by Nielsen from the combined SDK for DTVR. 

**Adobe validation** 

Here is some information to remember for Adobe validations: 


* For validating DTVR-related Video Analytics heartbeat data, ensure that the ` adload` flag is set to ` 1`. This value ensures that the Adobe data is not sent to Nielsen for DCR crediting. 

* Validate that VA heartbeat data is tracking as expected for live/linear video measurement to Adobe.


**Nielsen validation** 


* Validating Nielsen calls includes using an [ ID3 variable](#concept_CE553265019A45C58B234EF6F37DB12B/section_555F58E071C6409BBBB4EFF74290D714) (a long string of encoded text). This string does not include the typical DCR Nielsen variables. 

* Video Summary comparisons are not included in DTVR for the following reasons: 
    * Adobe data is not used.
    * Nielsen variables are tied to ID3, which is not yet decoded in the Debug tool.



**Standard Video Playback (DTVR) Example** 


1. Enable a packet monitoring program on the same network as the device that is running the DTVR application. You can use, for example, Charles/Fiddler. 

1. Load the page or app.
1. Start the video player.
1. Press the play button to play video content.
1. When the video is loaded, verify that ` trackVideoLoad()` is called.
1. After the content starts playing: 
    * Verify that ` trackPlay()` is called.
    * Verify that ` trackTimedMetadata()` is called. When timed metadata objects are received with a PRIV key, the value of the key is sent to the ` trackTimedMetadata()` API. 



1. On completion of video playback, verify that ` trackComplete()` is called.
1. Verify that measurement pings are sent properly.


## ID3 Example {#section_555F58E071C6409BBBB4EFF74290D714}

ID3 tags have a payload of approximately 249 characters and start with ` www.nielsen.com`. 

See [ www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/X100zdCIGeIlgZnkYj6UvQ==/AAAB2Jz2_k74GXSzx4npHuI_JwJd3QSUpW30rDkGTcbHEzIMWleCzM-uvNOP9fzJcQMWQLJqzXMCAxParOb5sGijSV9dNM3QiBniJYGZ5GI-lL1fXTTN0IgZ4iWBmeRiPpS9AAAAAAAAAAAAAAAAAAAAAFJWFM5SVhTONNU=/00000/00000/00](http://id3.org) for comprehensive information on ID3 tags.
