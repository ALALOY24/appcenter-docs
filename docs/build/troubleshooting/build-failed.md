---
title: Failed Builds
description: How to find and interpret errors in App Center Build
author: king-of-spades
ms.author: kegr
ms.date: 02/28/2020
ms.topic: article 
ms.assetid: d092ec2d-5f61-4cc5-8aca-bb36bec34a10
ms.service: vs-appcenter 
ms.custom: build
---

# Failed builds
There are various reasons why your build could have failed that might be unique to your project. Usually an efficient way to diagnose build failures is comparing them to a working build. This process can minimize variables and identify relevant conditions for your scenario. 

## If building works locally but not in App Center
Usually this problem is because of uncommitted files, different tooling, or unrestored dependencies. To check, you can do a full git clone of your project into a new folder. Then compile with the same configuration as App Center for comparison. 

1. Open your terminal or command-line prompt then type in: `mkdir appcenter-test`
2. Then change directories: `cd appcenter-test`
3. Clone your repository with: `git clone -b <branch> <remote_repo>`
4. Launch the freshly cloned project in your local IDE or command line. 
5. Try comparing [the build command executed in App Center](https://intercom.help/appcenter/build/how-to-find-your-build-command-in-app-center) to the command executed locally. 
6. Compare the versions of the tools you're using locally with our [Cloud Build Machines](~/build/software.md)

### Files with modified filenames or locations are ignored
If the Build system fails due to ignoring or missing a key file that was recently moved or renamed; try selecting **Save** or **Save & Build** in the build configuration. With either option App Center performs an analysis to index your repository tree and update the build definition. 

Common triggers of this problem include [build scripts](~/build/custom/scripts/index.md) & [nuget.config files](https://docs.microsoft.com/nuget/reference/nuget-config-file). Other files might cause similar problems if they're critical to the build and had a name or location change. 

## Comparing different builds in App Center
### Some branches work while others fail
Try checking for differences in the build settings or committed code between branches. Also, if the build starts failing consistently after a certain commit on the same branch, it's worth checking what changes were made in the failing commit.

### Builds fail intermittently
A build can fail without any change in source code or build settings. For example:
- Different versions of packages restored
- External services not responding
- Individual tasks in the build timing out
- and so on

Try checking if the error for the build is consistent when the failures occur. 

## Isolating and interpreting error messages
### Automatic error highlighting
App Center Build automatically attempts to highlight common error messages or useful output to make it more visible. Often clues can be found in the primary error, the logging before, or the logging afterwards. This app is signed by both the project settings & build configuration. So the Android jarsigner logs an error:

![Screenshot of highlighted error](images/errorlog.png)

```console
jarsigner: unable to sign jar: java.util.zip.ZipException: invalid entry compressed size (expected 13274 but got 13651 bytes)
##[error]Error: /usr/bin/jarsigner failed with return code: 1
##[error]Return code: 1
```

### Digging deeper
If you don't find relevant error messages, then the next step is to download the build logs, which you can do from the main build page. Open the folder named `logs_n > Build` and you'll see a list of separate log files listed in numerical order. For example:

- 1_Intialize job.txt
- 2_Checkout.txt
- 3_Tag build.txt
- and so on 

Logs are numbered based on the major phases of your build. Most build failures cause phases to be skipped & the associated log to be omitted:

- (Steps 1-9)...
- 10_Pre Build Script.txt
- 11_Build Xamarin.Android project.txt
- 12_Sign APK.txt
- 15_Post Build Script.txt
- 20_Post-job Checkout.txt
- 21_Finalize Job.txt

Phase 13 was skipped first, so phase 12 is a good starting point. Later phases were skipped too, but they're less likely to be relevant.

## Next Steps
Here are a few options for researching your issue further:

- [Other Build troubleshooting docs](~/build/troubleshooting/index.md)
- [Intercom Help Center (Build)](https://intercom.help/appcenter/en/collections/206279-build)
- [StackOverflow (App Center)](https://stackoverflow.com/questions/tagged/visual-studio-app-center)
- Documentation for the development platform your app uses

## Contacting Support
Log into https://appcenter.ms/apps and click the chat icon in the lower right corner of the screen. For best results, it's a good idea to open the ticket with:

- A summary of your observations
- Details and citations of your research on the issue
- URLs to failing builds, including essential info like the app name & build ID
- URLs to passing builds to compare to the failures (if applicable)
