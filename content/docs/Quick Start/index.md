---
title: 'Quick Start Guide'
date: 2022-03-10T19:30:08+10:00
draft: false
weight: 3
summary: Quickly get started with Sprie from a CDN and your `Sprie api-key`.
---

## 1 minute Sprie integration 🔥🔥🔥 

### Pre-requisites
1. Just have the apikey from sprie. 
2. Make sure the SKUs for the products are in sync with Sprie as well.
3. Make sure your production url is configured properly with Sprie Settings (AllowList).
4. Have a simple index.html getting served from a file server/web server.

### Integrate
Copy paste this code in a html file

```html

<!-- STEP 1. Load React CDN Scripts -->
<script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
<script 
  src="https://cdnjs.cloudflare.com/ajax/libs/prop-types/15.8.0/prop-types.min.js" 
  integrity="sha512-M1OTu9xD1JPdXo2cOeJI+Z/f8P6E/pqK9ug3G8PRNLw1caUePewEmpFYKSYh4LEz483qnyB/UTlgX1Q4VCEsKg==" 
  crossorigin="anonymous" referrerpolicy="no-referrer">
</script>

<!-- STEP 2. Load Sprie SDK -->
<script src="https://cdn.jsdelivr.net/npm/react-sprie-sdk@latest"> </script>

<!-- STEP 3. Intialize -->
<script>
  SprieSDK.Loader.Init({ apiKey:"<your api-key>" });
</script>

<!-- STEP 6. Trigger -->
<button onclick="SprieSDK.Loader.Load('product-sku');"> Preview </button>

```

### Explanation
1. _Integrate `React` runtime to run `SprieSDK`._ SprieSDK is built with React and hence these runtime libraries are needed to run Sprie.  
2. _Integrate SprieSDK from CDN_. Since its on CDN, Sprie will be cached in your browser and will work faster on subsequent page visits.  
3. _Initialise SprieSDK with the apikey_ (from pre-requisites). Without this step, Sprie will throw error.  
4. _Trigger Virtual Tryon Loader with SprieSDK `Loader` method_. SprieSDK is exported globally through window object.
   
List of all the methods and events are described in detail in the following doc pages.  