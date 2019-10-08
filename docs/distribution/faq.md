---
title: Distribution FAQ
description: Frequently asked questions about Distribution service
author: jeom
ms.author: jeom
ms.date: 10/08/2019
ms.topic: article
ms.assetid: 28011d49-082d-41e4-b3bb-2d51dbeb1192
ms.service: vs-appcenter
---

# Distribution FAQ

In the following we collected a list of frequently asked questions for Distribution in App Center. If you are missing anything please [reach out](~/general/support-center.md) to us.

## Frequently asked questions

### Can I distribute using an App Store Provisioning Profile?
The answer to your question is no.  You can use an Ad Hoc profile or an Enterprise certificate.  But Apple does not allow using App Store Provisioning profiles outside of the store. You can learn more about distribution service at [https://docs.microsoft.com/en-us/appcenter/distribution/auto-provisioning](https://docs.microsoft.com/en-us/appcenter/distribution/auto-provisioning). 

### How do I add an iOS device for testing?

1. Invite a tester to a distribution group using their email address. If you don't have an existing distribution group, you'll first need to create one. The tester will be notified that they have been invited to test your app.
2. Distribute a new release to the group.
3. The tester will be notified that a new release is available. The user will try to install and will not be able to download. 
4. Navigate to Distribute > Groups > Select the Group > Devices.
5. See the user in the list and click on three bullet points on the right to see "Copy UDID".
6. Then follow the process of adding the UDID to your provisioning profile as described in the documents linked in the docs. 

You can learn more about device registration at [https://docs.microsoft.com/en-us/appcenter/distribution/auto-provisioning](https://docs.microsoft.com/en-us/appcenter/distribution/auto-provisioning). 

### How to inspect iOS console log

If you are the developer of the app and can reproduce the problem on your device, please follow these steps.

1. Connect your iPhone, iPad, or iPod touch to your Mac
2. Open Xcode, then go to Window > Devices
3. Select your device in the left sidebar
4. Open the device log by clicking on the little triangle at the bottom of the window
 ![FAQ: how to inspect iOS console log](~/distribution/images/inspect_ios_console_log.png)
5. Start the installation of your app

During the installation, you should see one or more warning or error message. If you need help with those messages, please store the log into a .txt file and send it to customer support team.

