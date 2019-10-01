---
title: Windows Support
description: An overview of App Center's Windows support
keywords: crashes, diagnostics, errors, Windows, UWP, WinRT, WPF, Silverlight
author: winnieli1208
ms.author: yuli1
ms.date: 09/30/2019
ms.topic: article
ms.assetid: 8d48c68e-3fca-4dc4-b7d5-5f4474f8734f
ms.service: vs-appcenter
ms.custom: analytics
---

# Windows Support

App Center currently supports diagnostics for WPF and WinForms applications targeting .NET Framework or .NET Core 3, and UWP apps released through the Windows store. This page details the current level of support and the upcoming changes for UWP apps. For WPF and WinForms apps, refer to our [diagnostics features](~/diagnostics/features.md) and [WPF/WinForms SDK](~/sdk/crashes/wpf-winforms.md) pages for more information.

## Universal Windows Platform

App Center supports basic diagnostics features for UWP apps to help you fix your crashes. There are some known limitations and missing features compared to other supported platforms that we are actively addressing. You can learn more about these improvements in the transition section below. 

### Getting started

To enable App Center’s diagnostics for your UWP app, make sure you have the App Center SDK integrated for your app. Learn more about the UWP SDK in [App Center's UWP SDK documentation](~/sdk/crashes/uwp.md).

### Features Supported

#### Crash grouping

App Center groups your UWP crashes based on why and where the crash occurred. For each group, App Center displays the count, version and when the last crash in the group occurred, to help you prioritize and fix your crashes.

![App Center groups your crashes based on similarities](~/diagnostics/images/UWP-Crash-Groups.png)

#### Crash analytics

App Center displays a graph that indicates the number of crashes per day based on the selected time period.

![App Center shows you analytics on crashes](~/diagnostics/images/UWP-Analytics.png)

#### Crash group overview

Select a crash group to view the crash group stack trace and report details such as the most affected device and most affected OS. The full stack trace will only be displayed if you submit your app to the Windows store and upload the proper symbol files.

![App Center displays the stack trace and details of your crash group](~/diagnostics/images/UWP-Crash-Group-Overview.png)

#### Crash instance details

Select a crash report to view the crash stack trace and events. The full stack trace will only be displayed if you submit your app to the Windows store and upload the proper symbol files.

![App Center displays the stack trace and events of a crash instance](~/diagnostics/images/UWP-Crash-Instance.png)

### Known Limitations

App Center works with the Windows crash reporting service built into Windows devices to send and process crash logs. Because of this, there are some known limitations, we plan to address this year, unique to UWP apps.

- Crash reporting is enabled only on devices running Windows 10 Creators update or more recent (version 10.0.15063).
- Crash reporting on Windows requires the app to be distributed through the Microsoft Store.
- Crashes will only be sent if the device is plugged in to power, this includes phones.
- Some crashes might appear unsymbolicated (missing method names or file names or even class names) from applications that are associated with Microsoft Store
- UWP only supports starting Crashes with `AppCenter.Start` and none of the other API calls provided by the Crashes class are supported

You also might notice some features you see in other platforms are missing for your UWP apps. These include the following:

- A full symbolication experience that allows you to upload symbols in App Center. To upload symbols for your UWP crashes, you must submit your app to the Microsoft store and submit your symbols filed to Microsoft Dev Center.
- Number of users affected per crash group.
- Ability to add annotations and keep track of notes and other important information for your crash groups.
- Ability to mark crash groups as open, closed, or ignored.
- Ability to attach, view and download one binary and one text attachment to your crash reports.
- Crash report details per crash instance including when the app was launched, when it crashes, and what country, network, and language the device is in.
- Ability to download crash reports.

### Submitting your app to the Microsoft Store

To distribute your app through the Microsoft Store, you must create an app package file and [submit the package](https://docs.microsoft.com/windows/uwp/publish/upload-app-packages) to [Partner Center](https://partner.microsoft.com/dashboard). In creating your package file, you can include symbol files to upload to Partner Center. This will allow App Center to display symbolicated stack traces.

Follow the [Windows packaging documentation](https://docs.microsoft.com/windows/uwp/packaging/index) to package your app.

## Upcoming diagnostics updates for UWP apps

The App Center team is actively working on improving diagnostics support for UWP apps to address the limitations and gaps mentioned above. This section details the improvements you can expect to see in the upcoming weeks. 

### What improvements can I expect?

The new and improved diagnostics experience for UWP apps includes support for both Windows store and sideloaded apps. This includes the following additions:

- A full symbolication experience that allows you to upload symbols in App Center.
- Support for handled exceptions.
- Number of users affected per crash or error group.
- Ability to add annotations per crash or error group
- Ability to mark crash and error groups as open, closed, or ignored.
- Ability to attach, view and download one binary and one text attachment to your crash reports.
- Crash and error report details per crash instance including when the app was launched, when it crashes, and what country, network, and language the device is in.
- Ability to download crash and error reports.

You can learn more about each feature in the [App Center diagnostics documentation](~/diagnostics/features.md).

### What is the transition experience?

After you update to the App Center UWP SDK Version 2.5.0, you will see crashes and errors data coming into the App Center Diagnostics portal in a new and improved UI. All crashes from the old SDK will be displayed in a new section under Diagnostics, called "Legacy issues".

Your exsiting crashes data can still be viewed in the UI and returned via APIs listed under the [crashes section](https://openapi.appcenter.ms/#/crash).

For new crashes and errors data displayed in the new Diagnostics UI, you will need to use APIs listed under the [errors section](https://openapi.appcenter.ms/#/errors). Learn more about how the old crashes APIs map to the new errors APIs in the [API transition documentation](~/diagnostics/using-the-diagnostics-api#transitioning-to-the-new-apis.md). 

### What happens after the transition?

We will stop supporting the old legacy experience on January 20th, 2020. We encourage you to upgrade to the 2.5.0 SDK once it is released and start using the new errors APIs as soon as you can to ensure a smooth transition. If you need help or have questions about the transition, please reach out to our support team.

## WinRT, Silverlight, and Other Platforms

App Center doesn't currently support any other Windows platforms besides UWP, WPF, and WinForms. You can find more details about future Windows platform support in App Center in our [Windows Plan on Github](https://github.com/Microsoft/appcenter/blob/windows/specs/2019-04/Windows-Plan.md). If you have any feedback or feature requests, please leave your [feedback](../../../help.md).
