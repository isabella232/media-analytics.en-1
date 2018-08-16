---
description: This information helps users determine whether they want to opt-in to or opt-out of Nielsen ratings.
seo-description: This information helps users determine whether they want to opt-in to or opt-out of Nielsen ratings.
seo-title: Android Opt-Out Settings
title: Android Opt-Out Settings
uuid: d781b3c5-2b2d-4033-9002-9b3c6a680165
index: y
internal: n
snippet: y
translate: y
---

# Android Opt-Out Settings

To allow users to opt-in to or opt-out of Nielsen ratings on Android devices: 

```
java// Create webview with Nielsen Opt-Out URL  
optOutUrl = AdobeNielsenAPI.optOutUrlString(); 
mWebView = (WebView) findViewById(R.id.webView); 
mWebView.getSettings().setJavaScriptEnabled(true); 
  
mWebView.setInitialScale(1); 
mWebView.getSettings().setBuiltInZoomControls(true); 
mWebView.getSettings().setSupportZoom(true); 
mWebView.getSettings().setDisplayZoomControls(false); 
mWebView.getSettings().setLoadWithOverviewMode(true); 
mWebView.getSettings().setUseWideViewPort(true); 
mWebView.getSettings().setLayoutAlgorithm(LayoutAlgorithm.SINGLE_COLUMN); 
mWebView.setWebViewClient(new MonitorWebView()); 
mWebView.setWebChromeClient(new WebChromeClient()); 
mWebView.loadUrl(optOutUrl); 
  
// Capture and forward user selection       
private class MonitorWebView extends WebViewClient { 
    public void onPageFinished(WebView view, String url) { 
        Log.d(TAG, "FINISHED LOADING: " + url); 
    }; 
  
    @Override 
    public boolean shouldOverrideUrlLoading(WebView view, String url) { 
        Log.d(TAG, "shouldOverrideUrlLoading: " + url); 
  
        if (url.indexOf("nielsen") == 0) { 
            AdobeNielsenAPI.userOptOut(url); 
            finish(); 
            return false; 
        } 
        else if (url.indexOf("http") == 0) { 
            view.loadUrl(url); 
        } 
        return true; 
    } 
}
```
