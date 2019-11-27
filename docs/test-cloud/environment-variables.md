---
title: Environment variables
description: Environment variables in App Center Test
keywords: test cloud
author: jonstoneman
ms.author: jonsto
ms.date: 11/27/2019
ms.topic: article
ms.assetid: 51964205-c1d7-4fd7-8259-83485590c6e1
ms.service: vs-appcenter
ms.custom: test
---

# Environment variables

For most frameworks, useful environment variables are available within the test and/or application and you can set additional environment variables via the App Center CLI.

## Support by framework

It is unfortunately currently not possible to use environment variables within the application and test for each framework that App Center support.

The app environment variable are available in Calabash (iOS only), Xamarin UITest (iOS only) and Espresso.

The test environment variables are available in Appium, Calabash, Espresso and Xamarin UITest.

> [!NOTE]
> In Espresso tests and Android applications, variables are available in the `InstrumentationRegistry` since Android does not support environment variables.

## Environment variables available in your application

For frameworks for which App Center Test supports environment variables within the application, the following variables are provided:

| Environment Variable    | Description |
| ----------------------- | ----------- |
| `RUNNING_IN_APP_CENTER` | Set to `1` when the device is running in App Center Test

## Environment variables available in your tests

For frameworks for which App Center Test supports environment variables within the tests, the following variables are provided:

| Environment Variable | Description |
| -------------------- | ----------- |
| `APP_CENTER_TEST`    | Set to `1` when your tests run in App Center Test. |
| `XTC_APP_ENDPOINT`   | Address of a secure port on the device that allows other services to communicate with the application. Used by applications that embed their own HTTP servers in an application and need to interact with the app outside of the test framework. (Android Only).<br><br>Example: `http://devicehost151.prod:37777/proxy2/token-c059c5c6-37cc-4400-9038-96d1d342ed6e/` |
| `XTC_DEVICE`         | Combines the operating system name and the device name.<br><br>Example: `Google Pixel 2 XL (8.1.0)` |
| `XTC_DEVICE_INDEX`   | A string in the range of 0 to N-1, where N is the number of devices the test is run on. Used in situations where the same test is being run in parallel on multiple devices. `XTC_DEVICE_INDEX` is unique for each test run for each device. For additional discussion, see:  [Handling Concurrent Database Changes During Tests](https://intercom.help/appcenter/test/handling-concurrent-database-changes-during-tests). |
| `XTC_DEVICE_NAME`    | Name of the device running the test.<br><br>Example: `Google Pixel 2 XL` |
| `XTC_DEVICE_OS`      | Name of the operating system for the device running the test.<br><br>Example: `8.1.0` |
| `XTC_LANG`           | Language code used to run the test.<br><br>Example: `en` |
| `XTC_PLATFORM`       | Platform under test, either `android` or `ios`. |

## Setting additional environment variables

When you upload your tests to AppCenter with the appcenter CLI, you can request environment variables be set using the `--test-parameter` option. Environment variables can be set for test runner and for your application (the application under test or AUT).

> [!NOTE]
> See the *Support by framework* section for details of which frameworks support test and application variables in App Center Test.

### Environment variables for your tests

```shell
$ appcenter test run < > \
  < args > \
  --test-parameter "test_env=USERNAME=clever_user@example.com" \
  --test-parameter "test_env=PASSWORD=pa$$w0rd" \
  --test-parameter "test_env=TWO_FACTOR_URL=https://staging.example.com/test-2FA" \
  --test-parameter "test_env=UPGRADE_PURCHASED=0"
```

### Environment variables for your application

```shell
$ appcenter test run < > \
  < args > \
  --test-parameter "app_env=VERBOSE_LOGGING=1" \
  --test-parameter "app_env=CONTENT_SERVER=staging.example.com \
  --test-parameter "app_env=API_LEVEL=3.2" \
  --test-parameter "app_env=UPGRADE_PURCHASED=0"
```

## Using environment variables in your tests

### Sample Appium test code:

The following code snippet shows how to access environment variables in App Center Test using Appium

```java

String xamarintestcloud = System.getenv("XAMARIN_TEST_CLOUD");

String xtcappendpoint = System.getenv("XTC_APP_ENDPOINT");

String xtcdevice = System.getenv("XTC_DEVICE");

String xtcdeviceindex = System.getenv("XTC_DEVICE_INDEX");

String xtcdevicename = System.getenv("XTC_DEVICE_NAME");

String xtcdeviceos = System.getenv("XTC_DEVICE_OS");

String xtclang = System.getenv("XTC_LANG");

String xtcplatform = System.getenv("XTC_PLATFORM");
```

### Sample Calabash test code:

The following code snippet shows how to access environment variables in App Center Test using Calabash

```ruby

xamarintestcloud = ENV["XAMARIN_TEST_CLOUD"]

xtcappendpoint = ENV["XTC_APP_ENDPOINT"]

xtcdevice = ENV["XTC_DEVICE"]

xtcdeviceindex = ENV["XTC_DEVICE_INDEX"]

xtcdevicename = ENV["XTC_DEVICE_NAME"]

xtcdeviceos = ENV["XTC_DEVICE_OS"]

xtclang = ENV["XTC_LANG"]

xtcplatform = ENV["XTC_PLATFORM"]

```

### Sample Espresso test code

Since Android does not support environment variables, App Center Test sets `InstrumentationRegistry` values instead for Espresso. The following code snippet shows how to access the `InstrumentationRegistry` values.

```java

String xamarintestcloud = InstrumentationRegistry.getArguments().getString("XAMARIN_TEST_CLOUD");

String xtcappendpoint = InstrumentationRegistry.getArguments().getString("XTC_APP_ENDPOINT");

String xtcdevice = InstrumentationRegistry.getArguments().getString("XTC_DEVICE");

String xtcdeviceindex = InstrumentationRegistry.getArguments().getString("XTC_DEVICE_INDEX");

String xtcdevicename = InstrumentationRegistry.getArguments().getString("XTC_DEVICE_NAME");

String xtcdeviceos = InstrumentationRegistry.getArguments().getString("XTC_DEVICE_OS");

String xtclang = InstrumentationRegistry.getArguments().getString("XTC_LANG");

String xtcplatform = InstrumentationRegistry.getArguments().getString("XTC_PLATFORM");

```

### Sample Xamarin.UITest test code

The following code snippet shows how to access environment variables in App Center Test using Xamarin.UITest:

```csharp
string xamarintestcloud = Environment.GetEnvironmentVariable("XAMARIN_TEST_CLOUD");

string xtcappendpoint = Environment.GetEnvironmentVariable("XTC_APP_ENDPOINT");

string xtcdevice = Environment.GetEnvironmentVariable("XTC_DEVICE");

string xtcdeviceindex = Environment.GetEnvironmentVariable("XTC_DEVICE_INDEX");

string xtcdevicename = Environment.GetEnvironmentVariable("XTC_DEVICE_NAME");

string xtcdeviceos = Environment.GetEnvironmentVariable("XTC_DEVICE_OS");

string xtclang = Environment.GetEnvironmentVariable("XTC_LANG");

string xtcplatform = Environment.GetEnvironmentVariable("XTC_PLATFORM");
```

## Using environment variables in your application

### Sample native Android application code

> [!NOTE]
> See the *Support by framework* section for details of which frameworks support application variables in App Center Test.

Since Android does not support environment variables, App Center Test sets `InstrumentationRegistry` values instead. The following code snippet shows how to access the `InstrumentationRegistry` values.

```java

String xamarintestcloud = InstrumentationRegistry.getArguments().getString("XAMARIN_TEST_CLOUD");

String xtcappendpoint = InstrumentationRegistry.getArguments().getString("XTC_APP_ENDPOINT");

String xtcdevice = InstrumentationRegistry.getArguments().getString("XTC_DEVICE");

String xtcdeviceindex = InstrumentationRegistry.getArguments().getString("XTC_DEVICE_INDEX");

String xtcdevicename = InstrumentationRegistry.getArguments().getString("XTC_DEVICE_NAME");

String xtcdeviceos = InstrumentationRegistry.getArguments().getString("XTC_DEVICE_OS");

String xtclang = InstrumentationRegistry.getArguments().getString("XTC_LANG");

String xtcplatform = InstrumentationRegistry.getArguments().getString("XTC_PLATFORM");

```

### Sample native iOS application code

> [!NOTE]
> See the *Support by framework* section for details of which frameworks support application variables in App Center Test.

Native iOS applications access environment variables through the NSProcessInfo API.

```Objective-C
[[NSProcessInfo processInfo] environment]["XAMARIN_TEST_CLOUD"]
```

```swift
ProcessInfo.processInfo.environment["XAMARIN_TEST_CLOUD"]
```

## Getting help

You can always contact us through [the blue chat icon in the lower-right hand corner](https://intercom.help/appcenter/getting-started/getting-help-with-app-center). We don't provide 24/7 support, but will reply as soon as we can.

If you want help with a test run, navigate to the test run in question and copy the URL from your browser and paste it into the support conversation. A test run URL looks like something like https://appcenter.ms/orgs/OrgName/apps/App-Name/test/runs/77a1c67e-2cfb-4bbd-a75a-eb2b4fd0a747.
