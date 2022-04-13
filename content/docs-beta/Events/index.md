---
title: 'Events'
date: 2022-03-10T19:27:37+10:00
weight: 4
draft: false
summary: Listen to `SprieEvent` events and integrate `Sprie` seamlessly with your app.
---

##  ✨ Summary
`SprieSDK` dispatches certain events to the document in the browser which can be listened for to get certain hooks/results and changing the default experience of Sprie.  
All Sprie Events are prefixed with `SprieEvent:` to avoid conflict with other events dispatched globally in the DOM window by other libraries.

## Events Reference
All Events are based on `CustomEvent` or `Event`. You can find the respective data for particular event by standard event.detail.[field].

1. Auth
   1. SprieEvent:onAuthLoading ({isLoading: boolean}) 
   2. SprieEvent:onAuthOk () 
   3. SprieEvent:onAuthErr ({err: string}) 
   4. SprieEvent:onSDKReady () 
   5. SprieEvent:onSDKErr ({err: string})
2. IO
   1. SprieEvent:onCameraAllowed ( )
   2. SprieEvent:onCameraDenied ( )
   3. SprieEvent:onCameraError ({err: string})
3. Assets
   1. SprieEvent:onAssetCart ({sku: string})
   2. SprieEvent:onAssetWishlist ({sku : string})
   3. SprieEvent:onAssetLoading ({sku: string, isLoading: boolean})
   4. SprieEvent:onAssetLoadOk ({sku: string})
   5. SprieEvent:onAssetLoadErr ({sku: string, err: string}) 
   6. SprieEvent:onCheckAssetSKU ({sku: boolean}). e.g. Response : {'your-product-sku':true} // if it already exists
   7. SprieEvent:onCheckAssetSKUBatch ({sku: boolean, … }). e.g. Response : {'your-product-sku':true, 'sku-2':false}


## Examples
### 📷 Simple Events Example
Considering the previous getting started example, write this code in a script tag below it or, add it to a separate file and import it in the `index.html` file.  
```javascript
// app.js
// Listen when Add to Cart button is pressed on Sprie Widget
document.addEventListener("SprieEvent:onAssetCart", function (e) {
    // e.g. send async/ajax request to an endpoint to add to cart
    alert("Added to cart " + e.detail.sku);
});

// Check if Camera permission was denied
document.addEventListener("SprieEvent:onCameraDenied", function (e) {
    alert("Camera Denied!");
});

// Check if Camera device is present or not.
document.addEventListener("SprieEvent:onCameraError", function (e) {
    alert("Camera Error : " + e.detail.err);
});

```
Line 5-8: Listen for SprieEvent:onAssetCart event which gets triggered on user clicking Add To Cart button.

Line 11-13: Listen for SprieEvent:onCameraDenied event which gets triggered in case the user denies camera permission in the browser.

Line 16-18: Listen for SprieEvent:onCameraError event which gets triggered in case of invalid/no camera is found.



### 🎁 Check SKU registration Example

You might have some products displayed on your website that might not be registered with Sprie. 
To disable the Preview button for such scenarios on a template based environment (Wordpress), you can check beforehand if the sku exists with Sprie or not and set the Preview Button visibility accordingly.  
_NOTE_: This method must be called only after successful authentication of Sprie with apiKey otherwise the request gets rejected due to invalid auth token. *All requests from SprieSDK internally sends an auth token that is received from authentication request, and is handled and managed internally.*

```javascript
// app.js
const sku = 'my-precious-sku'; 
var showPreviewButton = false;

var onAuthDoneHandler = function (){
    SprieSDK.CheckSKU(sku);
}

var onCheckSKUHandler = function (e){
    const result = e.detail; // {'my-precious-sku':true}
    if(result && Object.keys(result)[0]===sku){
        showPreviewButton = result[sku];
    }
}

document.addEventListener("SprieEvent:onAuthOk", onAuthDoneHandler);
document.addEventListener("SprieEvent:onCheckAssetSKU", onCheckSKUHandler);

```


### 🎁💐💝 Check Muyltiple SKUs registration Example

To handle multiple SKUs, SprieSDK exposes a batch method `CheckSKUBatch`. You can send an array of SKUs and it can respond with all the SKUs with boolean data to signify if it exists with Sprie. You can easily use it in a product list page.

*NOTE*: To maintain sanity of page load time, and requests timeouts, you can send at-most 50 SKUs in a single batch request but we recommend sending 20 SKUs for better performance and relay the rest on pagination/lazy loading techniques.

```javascript
var skuArray = ['my-precious-sku','my-secondary-sku']; 
var validSkus = [];

const onAuthDone = function (){
    SprieSDK.CheckSKUBatch(skuArray);
}

const onCheckSKUBatch = function (e){
    const result = e.detail; // [{ 'my-precious-sku':true, 'my-secondary-sku':false }]
    validSkus = Object.keys(result).map(x=>x).filter(x=>result[x]).map(x=>x); // validSkus=['my-precious-sku'];
}

document.addEventListener("SprieEvent:onAuthOk", onAuthDone);
document.addEventListener("SprieEvent:onCheckAssetSKUBatch", onCheckSKUBatch);

```