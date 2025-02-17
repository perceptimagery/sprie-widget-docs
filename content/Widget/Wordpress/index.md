---
title: 'Wordpress'
date: 2025-02-17T15:14:39+10:00
weight: 6
summary: Integrate `SprieSDK` in Wordpress + WooCommerce Setup
---

A typical Wordpress + WooCommerce setup will consist of lots of php files and a server side theme based framework. All the activities in Sprie happen in front end. What we can do is break the typical Sprie Workflow into several .php files so that they all take care of specific actions on specific intents.

## Workflow

1. Initialise Sprie Widget at a common place
2. Translate skus from objects ids
3. Check if this item is registered with Sprie or not.
4. Add to Cart
5. Create a Button 'Try Now' on the product page & trigger 3D AR Preview

## Implementation

All the implementation work requires you to edit php files, right off the admin editor:

1. Go to your wp-admin page and login (`https://www.yourcompany.com/wp-admin/`)
2. Appearance > Theme File Editor
3. Edit/update/insert the code and click on `Update File`.

### Initialise Sprie Widget

We would want to Initialize Sprie Widget in a place where that particular part of html gets rendered on every single page.
'footer.php' is a very good way to start initializing the widget.
Insert the following code in `footer.php` file, after `<?php wp_footer(); ?>` :

```HTML
<!-- STEP 1. Load Sprie CDN Script with api key (most preferred way to integrate )-->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-widget@latest?apikey={apikey}"></script>
```

### Check Item sku registration with Sprie

From the above step, we get a sku for a specific product which we want to run through Sprie Check. Now Sprie authentication happens under the hood with the api key provided, and its a asynchronous task. Sprie exposes certain [events](https://docs.sprie.io/docs/events) to let the developers know when certain actions happen, and how to listen to them.  
In this case, we tap on to `onSDKReady` event to know when the authentication is done and Sprie is ready for use. Put the below code in the same `footer.php` file after the above step.

```HTML

<script>
 document.addEventListener("SprieEvent:onSDKReady", function(e){
  // Check product registration if inside product page
  if(productSku){
   SprieSDK.CheckSKU(productSku).then(checkResult=>{
    var event = new Event('SprieEvent:onCheckAssetSKU', { bubbles: true, cancelable: false });
    productSprieReady = checkResult[productSku];
    window.dispatchEvent(event);
   });
  }
 });
</script>

```

Here, what we are doing is listening to `onSDKReady` event, then checking of productSku is not null, and then using [Sprie Methods](https://docs.sprie.io/docs/methods) to check product registration with Sprie. Once the result is received, we create a custom client event and dispatch the result so that the event can be later on received and 'Try Now' Button can be showed.

### Handle Add to Cart

Sprie offers a Add to Cart CTA on the widget which dispatches an event with the specific product SKU. You can listen to the event and decide the action on the received event. The reason we do not provide any backend action is because Sprie doesn't interfere with the framework you are using and leaves it up to you to decide how you want to implement it.

As an example, in Wordpress + Woocommerce setup, you can add it to card in the following way :

```HTML
<script>

 document.addEventListener("SprieEvent:onAssetCart", (e)=>{
  const sku2id={'centena-bert-gunmetal':12, 'mattecentena-jarvis-mattetortoise': 14};
  var _nonce = "<?php echo wp_create_nonce( 'wc_store_api' ); ?>";
  jQuery.ajax({
   type: 'POST',
   url: '/wp-json/wc/store/cart/add-item',
   dataType: 'json',
   headers: {
    'X-WC-Store-API-Nonce': _nonce
   },
   data: {
    id : sku2id[e.detail.sku],
    quantity: 1
   },
  }).done(function() {
  console.log('Added : ',e.detail );
 });
</script>

```

This particular code uses `onAssetCart` event from Sprie to POST to `/wp-json/wc/store/cart/add-item` api from woo commerce to add the item to cart using jQuery's `ajax` method, which is by default installed in a wordpress setup.

### Create 'Try Now' button and trigger the VTO widget

in `functions.php`, put the code below :

```HTML
add_action( 'woocommerce_after_add_to_cart_button', 'add_custom_button', 10, 0 );
function add_custom_button() {
  ?>

<button style="display:none" id="sprie-try-single" type="button" class="btn-atc" onclick="SprieSDK.Load(productSku)" > Try Now</button>

<script>
 window.addEventListener("SprieEvent:onSKUCheck", function(e){
  const btn = document.querySelector('#sprie-try-single');
  if(productSprieReady){
   btn.style.display = "inline";
  }else{
   btn.style.display = "none";
  }
 });
</script>
<?php
};

```
