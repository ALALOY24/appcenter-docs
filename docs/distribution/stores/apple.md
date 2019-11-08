---
title: Publish to iTunes
description: Simplify distribution of mobile applications to the App Store
keywords: distribution store
author: oddj0b
ms.author: vigimm
ms.date: 10/18/2019
ms.topic: article
ms.service: vs-appcenter
ms.custom: distribute
ms.assetid: 32d31a11-8c89-458b-9074-0da4a06384a1
---

# App Store and TestFlight Distribution

Publish iOS app upgrades to the App Store and TestFlight with Fastlane in App Center.

## Pre-requisites

* The first version of an iOS application must be published through the iTunes Connect portal.
* App should be ready for submission and pass the [App Store guidelines](https://developer.apple.com/app-store/review/guidelines/).
* An active [Apple Developer Program](https://developer.apple.com/programs/enroll/) account, or have your Apple ID added as an admin in your teams [iTunes Connect](https://itunesconnect.apple.com/login) account.

For more information, review the [Apple App Distribution Guide](https://help.apple.com/xcode/mac/current/#/dev8b4250b57).

## Set up the connection between App Center to iTunes and TestFlight

1. Select **Stores** under Distribution.
2. In the middle of the page, click on the **Connect to Store** button.
3. Select the store type as **iTunes Connect** from the panel that opens.
4. Click on **Next** in the lower-right corner.
5. Sign in with your Apple developer account (a onetime activity) and click **Connect**.
6. On successful sign in, if the Apple account is a member of multiple teams an option to select the team to associate the builds will be available. If the Apple account is a member of only a single team, then the selection is defaulted to the single one available.
7. Now a list of apps for the team selected will be available for selection.
8. Select to app to be upgraded.
9. Store connections for the selected app will be automatically set up
   * An App Store connection named **Production**.
   * A [TestFlight](https://developer.apple.com/testflight/) connection for internal testers named **iTunes Connect users**.
   * External tester groups connections based on the external groups created in the iTunes Connect console.

10. Setting up this connection is a one time process for an app in App Center.

**Select destination in dropdown menu for upload instructions**

> [!div  class="op_single_selector"]
> * [App Store](apple/app_store.md)
> * [TestFlight Internal Testers](apple/testflight_internal.md)
> * [TestFlight External Testers](apple/testflight_external.md)

> [!NOTE]
> When submitting the deliver file to App Store Connect, App Center defaults to:
> ```js
>  add_id_info_uses_idfa: false
>  export_compliance_uses_encryption: false
>  export_compliance_encryption_updated: false
>  ```

## Adding Two-factor authentication

If your Apple account has two-factor authentication enabled, App Store Connect requires an app-specific password as security. You can add an App-specific password to your account by navigating to [Developer accounts in your Account settings](https://appcenter.ms/settings/accounts).

> [!TIP]
> Only App Store and TestFlight require an app-specific password.
> Only Apple IDs with two-factor authentication enabled can select **Update app-specific password**.

1. Hover over an item in the **Accounts** list.
2. Click the three vertical dots on the right side of the list
3. Select **Update app-specific password**.
4. Generate an app-specific password using the [Apple ID portal](https://appleid.apple.com/).
    * The name is for you to remember which service or app is using the app-specific password.
5. Copy the generated app-specific password and paste it into the dialogue.
6. Save by clicking **Update**.

## Publishing through the CLI
Using the CLI is an easy way to integrate the App Center's store connection as part of your CI/CD setup like Jenkins or Go CI.

Before you can use the CLI, you will need to establish a connection to a destination, i.e., Google Play, App Store, or Intune in the App Center. And compile a binary that complies with your destination.

You can list your stores by using the list command like this:
```
appcenter distribute stores list \
--app {app_owner}/{app_name} \
--output json
```

You will get a result like this:

```
[["Production","apple","production"],["App Store Connect Users","apple","testflight-internal"]]
```
And it's the Store column we will be using in the final step.

The final step is to publish your app by running:
```
appcenter distribute stores publish \
--file /path/to/file.ipa \
--store Production \
--app {app_owner}/{app_name} \
--release-notes "Some note."
```

You will need to fill in the blanks like the list command. Instead of having a static release note, it's possible to use the `--release-notes-file` instead. A release note file is plain text file encoded with UTF-8.

## Debugging a failed release

If a release fails to publish, you can debug the release by downloading the Fastlane logs that provides more verbose logs than the App Center portal.
You find the Fastlane logs on the detailed release page by clicking **Download Fastlane logs**  under the **Status** section.
