---
title: UWP Symbolication
description: Help understanding symbolication for UWP diagnostics in App Center
keywords: crashes, errors, UWP, symbols, symbolication
author: winnieli1208
ms.author: yuli1
ms.date: 10/16/2019
ms.topic: article
ms.assetid: 84e46674-0558-4c95-8f33-b8f4cf8970d6
ms.service: vs-appcenter
ms.custom: analytics 
---

# UWP Symbolication


## Overview

UWP crash reports show the stack traces for all running threads of your app at the time a crash occurred. The stack traces only contain memory addresses and don’t show class names, methods, file names, and line numbers that are needed to read and understand the crashes.

## Uploading symbols
To get these memory addresses translated you need to upload a **.appxsym** file to App Center, which contains all information required for symbolication.

### Generate the Symbols

In order to obtain an **.appxsym** file, you must create an app bundle as described [here](https://docs.microsoft.com/en-us/windows/msix/package/packaging-uwp-apps). Once you have created the bundle, you'll find the symbols file as an **.appxsym** inside the app bundle folder.

### App Center Portal

1. Log into App Center and select your app
2. In the left menu, navigate to the **Diagnostics** section
3. Select **Symbols**
4. In the top-right corner, click **Upload symbols** and upload the **appxsym** file you generated previously
5. After the symbols file is indexed by App Center, new incoming crashes will be symbolicated for you


### App Center API

1. Trigger a `POST` request to the [symbol_uploads API](https://openapi.appcenter.ms/#/crash/symbolUploads_create). 
This call allocates space on our backend for your symbols and returns a `symbol_upload_id` and an `upload_url` property.
2. Using the `upload_url` property returned from the first step, make a `PUT` request with the header: `"x-ms-blob-type: BlockBlob"` and supply the location of your symbols on disk.  This call uploads the symbols to our backend storage accounts. Learn more about [PUT Blob request headers ](https://docs.microsoft.com/en-us/rest/api/storageservices/put-blob#request-headers-all-blob-types).
3. Make a `PATCH` request to  the [symbol_uploads API](https://openapi.appcenter.ms/#/crash/symbolUploads_complete) using the `symbol_upload_id` property returned from the first step. In the body of the request, specify whether you want to set the status of the upload to `committed` (successfully completed) the upload process, or `aborted` (unsuccessfully completed).

> [!NOTE]
> The symbol uploads API will not work for symbols files that are 256MB or larger in size. Please use the App Center CLI to upload these files. You can install the App Center CLI by following the instructions in our [App Center CLI repo](https://github.com/microsoft/appcenter-cli).
