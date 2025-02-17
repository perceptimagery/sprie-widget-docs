---
title: 'Concepts'
date: 2025-02-17T15:14:39+10:00
draft: false
weight: 2
summary: Understand basic concepts and terminology used in `Sprie` environment.
---

## ✨ Features

You can do more with Sprie:

1. Allow customers to virtually try-on your products
2. Show them quick variations in the try-on widget itself.
3. Allow customers to directly add the product to your platform cart
4. Allow them to add a product to wishlist.
5. Let them share their picture with their friends and family, how they look with your product on them.
6. Gather critical insights and helpful analytics without compromising user privacy.

## ⛽️ Life Cycle

Sprie is meant to work on frontend javascript based apps only. You do not need to call any specific external URLs to communicate with Sprie Servers as `SprieSDK` does it on your behalf ( for authentication, checking registry, downloading 3d files) through an encrypted layer.

Sprie enabled Apps have very specific lifecycle :

1. Integrate SDK
2. Initializes with `api-key`
3. _(optional) Check if certain SKU or SKUs are registered with Sprie_
4. _(optional) on proper check result, set visibility of Trigger/Preview button_
5. Trigger the Virtual Try On
6. _(optional) Handle Events for specific use-cases (check of webcam permission, authentication result, etc)_
7. Customize Sprie

## 🥁 Terminology

| Term                 | Definition                                                                                                                                                                                                                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `SprieSDK`           | Global window object `SprieSDK`, used for communicating with `Sprie Servers`                                                                                                                                                                                                                           |
| `api-key`            | The encrypted api-key received from [Sprie](https://www.sprie.io) upon organization onboarding. Used for initializing `SprieSDK`. Can be revoked upon request. Expires automatically when contract ends.                                                                                               |
| `SKU`                | [Stock Keeping Unit](https://www.investopedia.com/terms/s/stock-keeping-unit-sku.asp). Uniquely identify a single product in the onboarded e-commerce platform. Used for sending/loading the product on AR. Can be any unique-id (url param, db id, etc). Can be updated on Sprie Servers accordingly. |
| `Trigger`            | Any Preview button that triggers the virtual try-on with a specific product SKU.                                                                                                                                                                                                                       |
| `Registered Product` | According to your plan, you can choose to either onboard all the products in your e-commerce, or just few. As a proper user experience, you should always check if a product is registered with Sprie or not before showing the `Trigger`/ Preview button.                                             |
| `Virtual Try-on`     | The `Sprie Widget` that opens up on the website upon triggering the SDK.                                                                                                                                                                                                                               |
