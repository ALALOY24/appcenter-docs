---
title: Handling User Consent
description: How to handle user consent with Analytics
keywords: GDPR, DSR, Privacy, EU
author: hamswan
ms.author: hamswan
ms.date: 06/06/2019 
ms.topic: article 
ms.assetid: 26C66069-05D6-4EC2-84DD-AB86AF50EB97
ms.service: vs-appcenter
---

# Handling User Consent

## Ask for the Users' Consent To Send Analytics logs

If you want to get your users' confirmation before sending any Analytics data to App Center, the App Center SDK exposes an API that you can leverage before sending any Analytics data to App Center.

Follow the steps below:
1. In your application code, build your own UI to ask for user consent.

2. You can display a message and two buttons in the dialog. An Example for this message - "This application has integrated App Center SDK to send data. Do you wish to send App usage data when using this application? Choose "Yes" to continue". The two Buttons can be used to get consent from users - "Yes" or "No". 

3. If the user chooses 'Yes', in your application code, you can call this App Center SDK API which enables sending of data to App Center backend. Make sure to pass the parameter as 'true' in the API.

You can read more about how to ask for the users' consent to send Analytics data per platform:

     -  [Android](https://docs.microsoft.com/en-us/appcenter/sdk/analytics/android#enable-or-disable-app-center-analytics-at-runtime)
     - [iOS](https://docs.microsoft.com/en-us/appcenter/sdk/analytics/ios#enable-or-disable-app-center-analytics-at-runtime)
     - [Xamarin](https://docs.microsoft.com/en-us/appcenter/sdk/analytics/xamarin#enable-or-disable-app-center-analytics-at-runtime)
    
4. If the user chooses 'No', in your application code, you can call this App Center SDK API which disables sending of data to App Center backend. Make sure to pass the parameter as 'false' in the API.

appcenter.setenabled(false);

You are done. Your app users should see this consent dialog box when they try to use the app. 
