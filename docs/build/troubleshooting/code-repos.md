---
title: Code Repository Troubleshooting
description: Troubleshooting issues with code repositories in Build
keywords: build, troubleshooting
author: nrajpurkar
ms.author: nirajpur
ms.date: 09/12/2018
ms.topic: article
ms.assetid: 860b2438-d3e9-4f0c-bf92-cccb98fdd29b
ms.service: vs-appcenter
ms.custom: build
---

# Code Repository Troubleshooting

## <a name="not-listed"/>The repository I want to connect to is not listed in the Connect to Repository step

* Only Git repositories are supported at this point. If you're trying to link to another type of repositories (e.g. Mercurial, TFVC, etc), it will not show up in the repository list.
* If connecting to a repository that belongs to an organization on GitHub or team on Bitbucket, first request admin access to the repository.
  In order to use a repository for building apps with App Center, you must have admin rights to that repository. Admin rights are required because App Center will register a webhook on your repository coming from the appcenter.ms domain.
  For GitHub repositories, depending on your organization's configuration, the first time when a member requests App Center access to that organization, an organization member with owner privileges might need to approve that request. See the [GitHub-specific instructions on how to approve third party applications for your organization](https://help.github.com/articles/approving-third-party-applications-for-your-organization/). It can take up to a few minutes until repositories from that organization will show up in App Center.
* If connecting to a repository owned by a user, you must be the owner of the repository. If you are not the owner, you can still onboard the app to App Center build by inviting the repository owner as a collaborator to the app in App Center. Then, the owner can connect the repository as a source to the App Center build service.

## <a name="on-premises"/>Can I use on-premises repositories?

App Center currently supports cloud hosted git repositories on Azure DevOps (formerly known as Visual Studio Team Services (VSTS)), Bitbucket and Github, but does not support on-premises repositories.

## <a name="wrong-bitbucket"/>I have connected to the wrong Bitbucket account. How can I re-connect to the correct one?

Disconnect the connected Bitbucket account and [re-connect to the correct account](~/build/connect.md#bitbucket).

## <a name="reconnect-github"/>I have connected to the wrong GitHub account. How can I re-connect to the correct one?

Disconnect the connected GitHub account and [re-connect to the correct account](~/build/connect.md#github).

## <a name="wrong-VSTS"/>I have connected to the wrong Azure DevOps account. How can I re-connect to the correct one?

Disconnect the connected Azure DevOps (formerly VSTS) account and [re-connect to the correct account](~/build/connect.md#vsts).

## <a name="not-listed"/>When connecting a Azure DevOps repository, I see "No Projects Found"

It is possible when you first attempt to connect AppCenter to Azure DevOps (formerly VSTS), it's authorized under the wrong organization. Determine [which Azure DevOps accounts are associated with an organization](https://app.vsaex.visualstudio.com/me?mkt=en-US) and ensure yours is listed. When you attempt to complete the OAuth flow, verify the message reads **App requests the following permissions from name@org.com (org)**. You will need to [re-connect to the correct account](#wrong-VSTS) if you connected to the wrong account.

## <a name="git-sub"/>Are Git submodules supported?

For repositories hosted on GitHub and Azure DevOps, Git submodules over HTTPS are supported using the same authentication as the parent repository. 
For repositories hosted on Bitbucket, only un-authenticated Git submodules are supported for now.

## <a name="bitbucket-git"/>I'm connected to Bitbucket and my builds fail with Git error

If your builds fail with an error similar to

```Text
"fatal: reference is not a tree:..
##[error]Git checkout failed with exit code: 128",
```

do the following:

* Go to the Webhooks section of the connected Bitbucket account and look for any disabled Webhooks from **mobile.azure.com**
* Re-enable the Webhooks
* Commit a change to the affected repository/branch and try a new build

Reach out to [App Center support]((https://intercom.help/appcenter/getting-started/getting-help-with-app-center) if the issue persists.

## <a name="tfvc"/>What can I do if am using Team Foundation Version Control (TFVC)?

App Center Build only supports Git repositories. For projects using a TFVC repository, unless you want to [convert them to Git](https://docs.microsoft.com/vsts/git/import-from-tfvc), you can use Visual Studio Team Services for continuous integration, and take advantage of the [Hosted macOS Preview](https://docs.microsoft.com/vsts/build-release/apps/mobile/xcode-ios?tabs=vsts) agents as well as build tasks for App Center Distribution and Test.

## <a name="code-source-secure"/>Is my source code secure?

App Center uses virtual machines to build your code. There is a clean virtual machine provisioned especially for your build which gets discarded once the build finishes. The files uploaded for code signing and the password for the certificate are also stored securely on our servers.
