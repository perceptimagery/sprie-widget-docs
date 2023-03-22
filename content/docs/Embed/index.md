---
title: "SprieEmbed"
date: 2023-03-22T10:40:39+05:30
draft: false
weight: 9
summary: Embed Sprie Preview anywhere
---


## What is Sprie Embed?
`Sprie Embed` is a plugin extension for `SprieSDK` which can be used to show 3d previews directly inline on your page. Works same way as normal sdk. All you need to do is get the cdn link and attach an `apiKey` to the same cdn script. 

## Summary
- [What is Sprie Embed?](#what-is-sprie-embed)
- [Summary](#summary)
- [Changes](#changes)
    - [Features](#features)
    - [Breaking Changes](#breaking-changes)
- [Implementation](#implementation)
  - [Pre-requisites](#pre-requisites)
  - [Initialise](#initialise)
  - [Load 3d Previews](#load-3d-previews)
  - [Universal barcode](#universal-barcode)
- [Customisation](#customisation)
- [Full Code](#full-code)
- [Troubleshoot](#troubleshoot)
  - [Nothing is visible](#nothing-is-visible)
  - [Loader is throughout the whole page](#loader-is-throughout-the-whole-page)
  - [More issues](#more-issues)

## Changes
Version : 0.0.3100

#### Features
1. namespaced sku loader `data-sprie-sku`
2. new barcode attribute `data-sprie-barcode`
3. style issues fixed


#### Breaking Changes
1. `data-sku` is being deprecated in favour of `data-sprie-sku`.  
This is being done in order to avoid attribute pollution in DOM. Please update your embed code to follow latest guidelines. `data-sku` will still be supported for 45 days to give time to users to make the changes.  
`data-sku` attribute will be removed on 31st May 2023.


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
`sprie-embed-element` is very critical and that is how Sprie identifies where to load the previews. the `data-sprie-sku` value is what is uses to send across Sprie Server to get information about the asset. 
```HTML
<!-- Declare element with class `sprie-embed-element` and data-sprie-sku. This will get transformed after authentication -->
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
></div>
```

### Universal barcode
You can also add barcode id to `data-sprie-barcode` attribute. Please make sure either one of barcode or sku is present as attribute.



## Customisation
You can inject classes dynamically to the underlying content with `data-class` attribute.  
You can also customise how the preview looks by providing customisation options in `data-model-options` attribute. 


Currently, only transparent background is supported, but we will be adding more options in future. 
```HTML
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
    data-class="custom-element-class"
    data-model-options="transparent=0"
></div>

```


## Full Code
```HTML
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
></div>

<br />

<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
    data-class="custom-element-class"
    data-model-options="transparent=0"
></div>

<footer>
    <script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest?apikey={apikey}"> </script>
</footer>


```

## Troubleshoot
### Nothing is visible

1. Check apikey (check in network tab > authentication)
2. check sku / barcode

### Loader is throughout the whole page
 add css to the `sprie-embed-element` class 
 ```CSS
    .sprie-embed-element{
        position: relative;
        height: max-content;
        width: max-content;
    }
 ```

 ### More issues 
 Please file issues at <a href="mailto:tech@perceptimagery.com?subject=Sprie%20Embed%20issue&body=Issue%20regarding%20Sprie%20Embed%3A%0A">Sprie Help</a>