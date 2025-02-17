---
title: 'Quick Start Guide'
date: 2025-02-17T15:14:39+10:00
draft: false
weight: 3
summary: Quickly get started with `SprieEmbed` using a CDN script and your `Sprie api-key`.
---

## Basic Sprie Embed integration for quick start 🔥🔥🔥

### Pre-requisites  

1. Acquire the apikey from Sprie.
2. Make sure the SKUs for the products are in sync with Sprie as well.
3. Make sure your production url is configured properly with Sprie Settings (AllowList).
4. Have a simple index.html getting served from a file server/web server.

### Initialise

Get the CDN link - `https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest`.  
Get the APIKey from Sprie. Paste the following code in footer or a place that is non-blocking.

```HTML
<!-- Sprie -->
<!-- Inject `Sprie Embed` from CDN -->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest?apikey={apikey}"></script>
```

### Load 3d Previews

Declarative API helps you in organising the preview with more control and easier to use interface.  
`sprie-embed-element` is very critical and that is how Sprie identifies where to load the previews. the `data-sprie-sku` value is what is uses to send across Sprie Server to get information about the asset.

```HTML
<!-- Declare element with class `sprie-embed-element` and data-sprie-sku. This will get transformed after authentication -->
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
></div>
```
