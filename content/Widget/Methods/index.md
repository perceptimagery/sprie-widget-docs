---
title: 'Methods'
date: 2025-02-17T15:14:39+10:00
weight: 5
draft: false
summary: Call specific `SprieSDK` Methods to manipulate the widget
---

## ✨ Summary

`SprieSDK` exposes certain methods through SprieSDK window object. All methods (except `Init`) are authenticated and need you to initialize Sprie with a valid `api-key` first.

## Methods

#### 1. Load (sku)

`SprieSDK.Load( 'your-product-sku' );`

Call when you want to load a new asset on Sprie AR. Only SKU should be provided.

**Events :** SprieEvent:onAssetLoading, SprieEvent:onAssetLoadOk, SprieEvent:onAssetLoadErr

#### 2. CheckSKU (sku)

`SprieSDK.CheckSKU( 'my-precious-sku' );`

_(optional)_ Can be called to check if the product is registered with Sprie or not. For bulk assets, refer to CheckSKUBatch. **Must** be used after authentication is done.

###### Response

`{<sku>:<boolean>}`

###### Response Example

```javascript
{ 'my-precious-sku': true };
```

`true` signifies that the product with SKU identifier `my-precious-sku` exists with Sprie and can safely be loaded.

#### 3. CheckSKUBatch (skuArray)

`SprieSDK.CheckSKUBatch( ['your-product-sku', 'your-product-sku2'] );`

_(optional)_: Can be called to check if an array of product SKUs is registered with Sprie or not. **Must** be used after authentication is done.

###### Response

`[{<sku>:<boolean>}]`

###### Response Example

```javascript
[
 { 'your-product-sku': true }, // this sku exists
 { 'your-product-sku2': false }, // this doesn't
];
```

#### 4. GetSprieLink (sku)

`SprieSDK.GetSprieLink (sku)`

Fetches the share link of the product (with the product page), typically to share it via an app, or show a QR code. this link appends `sprie-sku` query param with the given sku which helps Sprie Widget to open automatically.

#### 5. Unmount ( )

`SprieSDK.Unmount( );`

Removes current instance of SprieSDK from website. This action is stateless, which means, refreshing the page will re-mount it again.
