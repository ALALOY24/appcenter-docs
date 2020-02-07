---
title: Publish an iOS package to the App Store (Production)
description: Learn how to release to App Store from App Center
keywords: distribute, stores, fastlane, app store
author: oddj0b
ms.author: vigimm
ms.date: 02/07/2020
ms.topic: article
ms.assetid: ede8ed54-baed-4e9d-be2b-6606e41adaa2
ms.service: vs-appcenter
---

# Publish an iOS package to the App Store (Production)

> [!TIP]
> [Build your app according to Apples guidelines](https://developer.apple.com/app-store/submissions/)

1. From the Stores home page select the “Production” store created above.
2. Click on **Publish to Store** in the upper-right corner.
3. At the first step of the wizard you must upload you ipa file and after the file have a been succesfully uploaded you'll se details like icon and version. Click **Next**.
4. Click on **Publish**. The status for this release on the store details page will show as **Submitted**. Submitted means that the ipa have been deivered to App Store Connect for evaulation.
5. Once App Center has completed the hand-over of the app to iTunes, the status of the app will change to **Published**. And the app is available to download through Apple's App Store.
6. In case of a failure while publishing by Apple, the status on the store details page will change to **Failed** with the appropriate error message.
   Review [Apple's app review process](https://developer.apple.com/support/app-review/).
