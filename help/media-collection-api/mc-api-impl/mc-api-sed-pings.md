---
seo-title: Sending ping events
title: Sending ping events
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33

---

# Sending ping events{#sending-ping-events}

**For main content, you must fire ping events every 10 seconds, beginning after 10 seconds of playback, regardless of other API events that you have sent. For Ad tracking, you must fire ping events every 1 second -** This is literally the "heartbeat" of Video Analytics. The only required parameters for a ping call are `eventType: ping` along with the `playerTime` object (playhead position and timestamp). The following code snippet shows one way to implement a timed pinging mechanism for main content (10 second interval): 

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```

