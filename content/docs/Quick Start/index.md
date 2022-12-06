---
title: 'Quick Start Guide'
date: 2022-04-12T19:30:08+10:00
draft: false
weight: 3
summary: Quickly get started with Sprie from a CDN and your `Sprie api-key`.
---

## 10 seconds superfast Sprie integration 🔥🔥🔥

### Pre-requisites

1. Just have the apikey from sprie.
2. Make sure the SKUs for the products are in sync with Sprie as well.
3. Make sure your production url is configured properly with Sprie Settings (AllowList).
4. Have a simple index.html getting served from a file server/web server.

### Integrate

Copy paste this code in a html file

```html
<!-- STEP 1. Load Sprie CDN Script with api key (most preferred way to integrate )-->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest?apikey={apikey}"></script>

OR
<!-- STEP 1. Load Sprie CDN Script -->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-widget@latest"></script>

<!-- STEP 2. Intialize -->
<div id="sdk-widget" data-apikey="api-key"></div>

<!-- STEP 3. Trigger -->
<button onclick="SprieSDK.Load('product-sku');">Preview</button>
```

### Explanation

1. _Integrate SprieSDK from CDN_. Since its on CDN, Sprie will be cached in your browser and will work faster on subsequent page visits.
2. _Initialise SprieSDK with the apikey_ (from pre-requisites). Without this step, Sprie will throw error.
3. _Trigger Virtual Tryon Loader with SprieSDK `Load` method_. SprieSDK is exported globally through window object.

List of all the methods and events are described in detail in the following doc pages.
