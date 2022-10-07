---
title: "SprieEmbed"
date: 2022-10-07T10:40:39+05:30
draft: false
weight: 9
summary: Embed Sprie Preview anywhere
---


## What is Sprie Embed?
`Sprie Embed` is a plugin extension for `SprieSDK` which can be used to show 3d previews directly inline on your page. Works same way as normal sdk. All you need to do is get the cdn link and attach an `apiKey` to the same cdn script. 

## Summary
- [What is Sprie Embed?](#what-is-sprie-embed)
- [Summary](#summary)
- [Implementation](#implementation)
  - [Pre-requisites](#pre-requisites)
  - [Initialise](#initialise)
  - [Load 3d Previews](#load-3d-previews)
- [Customisation](#customisation)
- [Full Code](#full-code)



## Implementation

### Pre-requisites  
1. Just have the apikey from sprie. 
2. Make sure the SKUs for the products are in sync with Sprie as well.
3. Make sure your production url is configured properly with Sprie Settings (AllowList).
4. Have a simple index.html getting served from a file server/web server.

### Initialise
Get the CDN link from `https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest`.  
Get the APIKey from Sprie. Paste the following code in footer or a place that is non-blocking.

```HTML
<!-- Sprie -->
<!-- Inject `Sprie Embed` from CDN -->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest?apikey={apikey}"></script>
```

### Load 3d Previews
Declarative API helps you in organising the preview with more control and easier to use interface.  
`sprie-embed-element` is very critical and that is how Sprie identifies where to load the previews. the `data-sku` value is what is uses to send across Sprie Server to get information about the asset. 
```HTML
<!-- Declare element with class `sprie-embed-element` and data-sku. This will get transformed after authentication -->
<div
    class="sprie-embed-element"
    data-sku="{sku}"
></div>
```

## Customisation
You can inject classes dynamically to the underlying content with `data-class` attribute.  
You can also customise how the preview looks by providing customisation options in `data-model-optionos` attribute. 


Currently, only transparent background is supported, but we will be adding more options in future. 
```HTML
<div
    class="sprie-embed-element"
    data-sku="{sku}"
    data-class="custom-element-class"
    data-model-options="transparent=0"
></div>

```


## Full Code
```HTML
<div
    class="sprie-embed-element"
    data-sku="{sku}"
></div>

<br />

<div
    class="sprie-embed-element"
    data-sku="{sku}"
    data-class="custom-element-class"
    data-model-options="transparent=0"
></div>

<footer>
    <script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest?apikey={apikey}"> </script>
</footer>


```