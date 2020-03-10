---
title: Federated Analytics
description: The Federated Analytics service provides a system for sharing Adobe Media Analytics data (audio and video) between two partners. 
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab

---

# Federated Analytics{#federated-analytics}

The Federated Analytics service provides a system for sharing Adobe Media Analytics data (audio and video) between two partners. 
The standardized measurement data created by Media Analytics is the hallmark for Federated Analytics, allowing the same data to flow into a single report from multiple sources. 
Through the rules and logic governing Federated Analytics, data is easily controlled and individualized to meet the needs of each partnership. 
Federated Analytics makes audio and video measurement more efficient, streamlined, and actionable.

## Benefits {#benefits}

* **Transparent:** Strip away the black box of data creation by using the same logic across companies
* **Broad:** Understand the full reach and impact of audio and video consumption across partnerships, platforms, and devices
* **Secure:** Control server-side data sharing through rules and logic
* **Standardized:** Speak the same data language as your partners
* **Actionable:** Quantify audio and video data to benchmark players, monitor trends, and detect anomalies through Adobe Analytics
* **Centralized:** Collect audio and video measurement data in one Adobe location
* **Contractual:** Meet legal data sharing requirements easily
* **Timely:** Send and receive data in near real-time
* **Easy:** Tag players once with Adobe SDKs, share data to many partners

## Definitions {#definitions}

* **Sender:** Customer generating audio and video analytics data on owned players
* **Receiver:** Customer receiving audio and video analytics data from sender

## Requirements {#requirements}

* **Media Streams Contract:** Receiver and Sender must have contracted Adobe Analytics for Media Streams before gaining access to audio and video data within Adobe Analytics. Contact your account team for more details.
* **Federated Addendum:** Each Sender and Receiver must have a signed addendum in place with Adobe before sending or receiving data. One addendum per customer is required, not one addendum per partnership. Contact your account team for more details. 
* **Media Analytics Implementation:** The Sender must have Media Analytics implemented on all players that will be part of the federated data set. Only Media Analytics data is available for federation. See documentation: [Measuring audio and video in Adobe Analytics](/help/media-overview.md) 

* **Adobe Consulting Contract:** For initial set-up of federated rules between receiver and sender it is valuable to work with consulting services to review data and create the data sharing agreement.

## Download the Federated Analytics Form

Download the current version of this form here: [Federation Rules Agreement](https://github.com/AdobeDocs/media-analytics.en/blob/master/help/federated-analytics-form.pdf)

## Process {#process}

1. Sender and Receiver work together to complete the Federation Rules Agreement form. The Federated Rules Agreement form contains special fields for our engineering team and should ONLY be edited using Adobe Acrobat. [Download Acrobat for free.](https://get.adobe.com/reader/)
1. Consulting services provides a sample data file to Receiver with actual data from Sender players, to further confirm correct data sharing rules are defined, provided data files are available.
1. Sender and Receiver ensure the data sharing agreement will meet all contractual requirements between the two parties.
1. Consulting services sends the completed form to Adobe Engineering to set-up data sharing rules.
1. Data is shared to the development report suite where Receiver will review and validate data.
1. Once Receiver confirms data is correct, Adobe Engineering updates the rules to point to a production report suite.
1. Receiver will review and validate data in the production report suite.
1. If changes occur to the data set in the future, Sender or Receiver can submit a customer care ticket for support.

