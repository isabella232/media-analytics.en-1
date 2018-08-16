---
description: null
seo-description: null
seo-title: Queueing Events When Sessions Response is Slow
title: Queueing Events When Sessions Response is Slow
uuid: d465bfe6-a2ed-4b9b-ab23-04ce544d4e34
index: y
internal: n
snippet: y
translate: y
---

# Queueing Events When Sessions Response is Slow


<a id="section_nk1_mnv_gcb"></a>

The Media Collection API is RESTful: i.e, you make an HTTP request and wait for the response. This is only important when you make a [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_sessions_req.md) to obtain a Session ID at the beginning of video playback. Your player may fire events before the ` sessions` response returns (with the Session ID parameter) from the backend. In this case your app must queue any tracking events that arrive between the [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_sessions_req.md) and its response. When the ` sessions` response arrives, you should first process any queued events, then you can start processing live events with the ` events` API. The [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_events_req.md)does not return data back to the client beyond an HTTP response code. Check the Reference Player in your distribution for one way to process events prior to receiving a Session ID. For example: 

```
jsvar eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```
**Process any queued events -** The reference player processes queued events as follows: 
```
js    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```


Continue to process tracking events as they occur.
