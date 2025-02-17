---
title: 'Quick Start Guide'
date: 2025-02-17T15:14:39+10:00
draft: false
weight: 3
summary: Quickly get started with Sprie from a CDN and your `Sprie api-key`.
---

## Guide for 30-seconds Sprie integration 🔥🔥🔥

### Pre-requisites

1. Acquire the apikey from Sprie.
2. Make sure the SKUs for the products are in sync with Sprie.
3. Make sure your development or production urls are configured properly with Sprie (AllowList).
4. Have a simple index.html getting served from a file server / web server.

### Integrate

Copy paste this code in a html file

```html
<!-- STEP 1. Load Sprie CDN Script with api key (most preferred way to integrate )-->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-widget@latest?apikey={apikey}"></script>

<!-- STEP 2. Trigger the Virtual Try On-->
<button onclick="SprieSDK.Load('product-sku');">Try On</button>
```

Remember to replace the `{apikey}` with a valid apikey that you received from Sprie.

### Explanation

1. _Integrate SprieSDK from CDN_. Since its on CDN, Sprie will be cached in your browser and will work faster on subsequent page visits.
2. _Initialise SprieSDK with the apikey_ (from pre-requisites). Without this step, Sprie will throw error.
3. _Trigger Virtual Tryon Loader with SprieSDK `Load` method_. SprieSDK is exported globally through window object.
