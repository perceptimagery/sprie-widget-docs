---
title: 'Concepts'
date: 2025-02-17T15:14:39+10:00
weight: 2
summary: Understand basic concepts and terminology used in `SprieEmbed` environment.
---

`SprieEmbed` is designed to work on frontend javascript based apps / websites only. You do not need to call any specific external apis to communicate with Sprie servers as `SprieEmbed` SDK does it on your behalf ( for authentication, checking registry, downloading 3d files, etc) through an encrypted layer.

## 🥁 Terminology

| Term                 | Definition                                                                                                                                                                                                                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api-key`            | The encrypted api-key received from [Sprie](https://www.sprie.io) upon organization onboarding. Used for initializing `SprieSDK`. Can be revoked upon request. Expires automatically when contract ends.                                                                                               |
| `SKU`                | [Stock Keeping Unit](https://www.investopedia.com/terms/s/stock-keeping-unit-sku.asp). Uniquely identify a single product in the onboarded e-commerce platform. Used for sending/loading the product on AR. Can be any unique-id (url param, db id, UPC / EAN code, etc). Needs to be synced with Sprie servers.                                                                                                                                                                                                    |
|`Registered Product` | According to your plan, you can choose to either onboard all the products in your e-commerce, or just few. As a proper user experience, you should always check if a product is registered with Sprie or not before adding it to the `sprie-embed-element`.                                             |
| `3D Preview`          | The `SprieEmbed` element that is created on the webpage upon loading the page under designated `sprie-embed-element` div.                                                                                                                                                                                                                               |
