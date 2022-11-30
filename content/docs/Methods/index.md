---
title: 'Methods'
date: 2022-04-10T19:27:37+10:00
weight: 5
draft: false
summary: Call specific `Sprie` Methods to manipulate the widget
---

## ✨ Summary

`SprieSDK` exposes certain methods through SprieSDK window object. All methods (except `Init`) are authenticated and need you to initialize Sprie with a valid `api-key` first.

## Method Reference

🍩 Methods

1. Init({apiKey})
2. Load (sku)
3. CheckSKU (sku)
4. CheckSKUBatch (skuArray)
5. Unmount ()
6. GetSprieLink (sku)

## Methods

#### Init({apiKey})

`SprieSDK.Init( {apiKey:'xxx-xxx-xxx'} );`

Must be called only once for apiKey authentication.  
_NOTE_: Internally we cache the authentication and tokens and handle subsequent auths.

###### Params

**apiKey :** string - apiKey received from Sprie Cloud

###### Response

**Events:** SprieEvent:onAuthLoading, SprieEvent:onAuthDone, SprieEvent:onAuthErr, SprieEvent:onSDKReady, SprieEvent:onSDKErr

#### Load (sku)

`SprieSDK.Load( 'your-product-sku' );`

Call when you want to load a new asset on Sprie AR. Only SKU should be provided.

###### Response

**Events :** SprieEvent:onAssetLoading, SprieEvent:onAssetLoadOk, SprieEvent:onAssetLoadErr

#### CheckSKU (sku)

`SprieSDK.CheckSKU( 'your-product-sku' );`

_(optional)_ Can be called to check if the product is registered with Sprie or not. For bulk assets, refer to CheckSKUBatch. Should be used after authentication is done.

###### Response

`{<sku>:<boolean>}`

###### Response Example

`{"my-precious-product":true}`
`true` signifies `my-precious-product` exists with Sprie and can safely be loaded.

#### CheckSKUBatch (skuArray)

`SprieSDK.CheckSKUBatch( ['your-product-sku', 'your-product-sku2'] );`

_(optional)_: Can be called to check if an array of product SKUs is registered with Sprie or not. Should be used after authentication is done.

###### Response

`[{<sku>:<boolean>}]`

###### Response Example

```javascript
[
	{ 'your-product-sku': true }, // this sku exists
	{ 'your-product-sku2': false }, // this doesn't
];
```

#### Unmount ( )

`SprieSDK.Unmount( );`

Removes current instance of SprieSDK from website. This action is stateless, which means, refreshing the page will re-mount it again.

#### GetSprieLink (sku)

`SprieSDK.GetSprieLink (sku)`

Fetches the share link of the product (with the product page), typically to share it via an app, or show a QR code. this link appends `sprie-sku` query param with the given sku which helps Sprie Widget to open automatically.
