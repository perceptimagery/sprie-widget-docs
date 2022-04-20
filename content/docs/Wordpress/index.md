---
title: 'Wordpress'
date: 2022-04-20T19:27:37+10:00
weight: 6
summary: Integrate `SprieSDK` in Wordpress + WooCommerce Setup
---

## Demo
Demo Link : `https://demo-wordpress.sprie.io/`   
Wordpress Plugin : Comming soon!

A typical wordpress + wooCommerce setup will consist of lots of php files and a server side theme based framework. All the activities in Sprie happen in front end. What we can do is break the typical Sprie Workflow into several .php files so that they all take care of specific actions on specific intents.

## Workflow
1. Initialise Sprie Widget at a common place
2. Translate skus from objects ids
3. Check if this item is registered with Sprie or not.
4. Add to Cart
5. Create a Button 'Try Now' on the product page & trrigger 3D AR Preview



## Implementation
All the implementation work requires you to edit php files, right off the admin editor:
1. Go to your wp-admin page and login (`https://www.yourcompany.com/wp-admin/`)
2. Appearance > Theme File Editor
3. Edit/update/insert the code and click on `Update File`.


### Initialise Sprie Widget
We would want to initialise Sprie Widget in a place where that particular part of html gets rendered on every single page.
'footer.php' is a very good way to start initialising the widget. 
Insert the follwing code in `footer.php` file, after `<?php wp_footer(); ?>` : 
```HTML
<!-- Sprie -->
<script src="https://cdn.jsdelivr.net/npm/@perceptimagery/sprie-widget@latest"></script>
<div id="sdk-widget" data-apikey="<your api key>"></div>
```

### Write SKU Translater
We need a way to send the skus to the `Load` method of the widget to show it properly. Most often times, the SKUs are pre-registered during asset onboard process with Sprie. To acquire the proper skus:
1. Either it can be generated uniquely and sent over to Sprie in a CSV,  
2. or, just use the url param of a current item in a PDP ( Product Display Page).

To use thr url-param as sku, we would need to translate the `url` into an `sku`. Write the following code in `footer.php` file after you have initialised Sprie Widget : 

```HTML
<script>
	// Fetch Product Specific Data
	const urlPath = window.location.pathname;
	const productSku = urlPath.indexOf('product/')>=0 ? urlPath.replace('product','').replaceAll('/','').trim() : '';
	var productSprieReady = false;
</script>

```
What we are essentially doing here is stripping the url param path and just taking the url id and storing it as `productSku` so that when we reach a PDP, `productSprieReady` automatically gets set to true, and we can continue to show the widget.


### Check Item sku registration with Sprie
From the above step, we get a sku for a specific product which we want to run through Sprie Check. Now Sprie authentication happens under the hood with the api key provided, and its a asynchronous task. Sprie exposes certain [events](../Events/index.md) to let the developers know when certain actions happen, and how to listen to them.  
In this case, we tap on to `onSDKReady` event to know when the authentication is done and Sprie is ready for use. Put the below code in the same `footer.php` file after the above step.

```HTML

<script>
	document.addEventListener("SprieEvent:onSDKReady", function(e){
		// Check product registration if inside product page
		if(productSku){
			SprieSDK.CheckSKU(productSku).then(checkResult=>{
				var event = new Event('SprieClient:onSKUCheck', { bubbles: true, cancelable: false });
				productSprieReady = checkResult[productSku];				
				window.dispatchEvent(event);
			});
		}
    }); 
</script>

```

Here, what we are doing is listening to `onSDKReady` event, then checking of productSku is not null, and then using [Sprie Methods](../Methods/index.md) to check product registration with Sprie. Once the result is received, we create a custom client event and dispatch the result so that the event can be lateron recevied and 'Try Now' Button can be showed.


### Handle Add to Cart
Sprie offers a Add to Cart CTA on the widget which raises an event with the specific product SKU. You can listen to the event and decide what to do with the Event itself. The reason we do not provide any backend action is because Sprie simply doesn't depende/ bother the frameowkr you are working on and leaves it upto you to decide how you want to implement it.
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

This particular code uses `onAssetCart` event from Sprie to POST to `/wp-json/wc/store/cart/add-item` api from woo commerce to add the item to cart usig jQuery's `ajax` method, which is by default installed in a wordpress setup.


### Create 'Try Now' Button and Trigger Preview

in `functions.php`, put the code below :
```HTML
add_action( 'woocommerce_after_add_to_cart_button', 'add_custom_button', 10, 0 );
function add_custom_button() { 
  ?>

<button style="display:none" id="sprie-try-single" type="button" class="btn-atc" onclick="SprieSDK.Load(productSku)" > Try Now</button>

<script>
    window.addEventListener("SprieClient:onSKUCheck", function(e){
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


### After this
We are in the process of creatign a plugin which will do all these on your behalf. Once we have completely tested the code, we will announce it and let you know.