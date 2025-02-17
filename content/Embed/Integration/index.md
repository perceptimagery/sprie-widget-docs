---
title: 'Integration'
date: 2025-02-17T15:14:39+10:00
weight: 4
summary: Advanced integration guide for `SprieEmbed`.
---

## Changing the product in 3D Preview

You can change the product on the fly by simply changing the product identifier in `data-sprie-sku` attribute.

## Customising the 3D Preview

You can inject classes dynamically to the underlying content with `data-class` attribute. Please note that `sprie-embed-element` class is required to be applied to the div. The customisations will be applied from `your-custom-class`. You can name your data-class as per your requirement.

```HTML
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
    data-class="your-custom-class"
></div>

```

## Supported Options

You can also customise how the preview looks by providing customisation options in `data-model-options` attribute. Currently, only transparent background and autostart is supported, but we will be adding more options in future.

**1. transparent** - Removes the background and makes it transparent. Default is `0`. (Note - The shadows will not be visible if set to 1. It can also affect the colours of the product depending on the background colour and the product's transparency, so use it with caution.)

**2. autostart** - Automatically loads the 3d preview. Default is `1`. (Note - A user input is required to load the 3D preview if set to 0. An image will be shown as a placeholder until the user clicks on the 3D preview.)

```HTML
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
    data-class="custom-element-class"
    data-model-options="transparent=1&autostart=0"
></div>

```

## Full Reference Code

```HTML
<!-- 1. Basic Integration -->
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
></div>

<!-- 2. Integration with Customisation -->
<div
    class="sprie-embed-element"
    data-sprie-sku="{sku}"
    data-class="your-custom-class"
    data-model-options="autostart=1"
></div>

<footer>
    <script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-embed@latest?apikey={apikey}"> </script>
</footer>
```
