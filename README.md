
[![](https://jitpack.io/v/com.vuzix/licensing.svg)](https://jitpack.io/#com.vuzix/licensing)

![Vuzix Logo](https://apps.vuzix.com/images/vuzix-logo-old.png)
# Licensing SDK for Vuzix App Store

This library allows applications published to the Vuzix App Store to check for a valid
license.

## Installation
1. Add JitPack as a maven repository in settings.gradle or settings.gradle.kts at the top level of your Android Studio project:
```
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        ...
        maven { url "https://jitpack.io" } // if using settings.gradle
        maven ("https://jitpack.io")       // if using settings.gradle.kts
    }
}
```
2. Add licensing to your module's build.gradle or build.gradle.kts file. Replace VERSION below with the version of the SDK you wish to use.
```
dependencies {
    ...
    implementation 'com.vuzix:licensing:VERSION'   // if using build.gradle
    implementation ("com.vuzix:licensing:VERSION") // if using build.gradle.kts
    ...
}
```
The latest licensing version on JitPack is [![](https://jitpack.io/v/com.vuzix/licensing.svg)](https://jitpack.io/#com.vuzix/licensing).

## Documentation
For additional information, please refer to the [Licensing SDK for Vuzix App Store Javadocs](https://vuzix.github.io/licensing/javadoc/allclasses-index.html).

## Sample Application
Please refer to the [Licensing SDK for Vuzix App Store Sample](https://github.com/Vuzix/LicensingSample) to see basic usage.

## Key Concepts

Any application that wishes to perform license management using the Vuzix App Store should incorporate this
SDK to perform the licence checking.

### Application Secret Key
Each application listed in the Vuzix App Store with a paid one-time fee or a subscription will have a
secret key in the listing that identifies the subscription.

### License Validation
This licensing SDK will communicate with the Vuzix App Store whenever a call to validateSubscription() is performed.
The unique Serial Number of the device is used to ensure that the requested subscription is valid.

### License Result Cache
When a valid subscription is found, the result will be cached.

If the Vuzix App Store API endpoints
are unavailable for any reason, the cached result will be used until the cache expires, or communication
is to the App Store API is restored. The duration of the
cache is controlled via the validation request options, and may be disabled completely.

The cached result includes the end date of the subscription. If communication to the Vuzix App Store API is
interrupted, license validity will be reported according to the dates established at the time the device was
most recently able to communicate to the Vuzix App Store API.

It is possible (but unlikely) for an end user to validate an application once, then cancel the subscription
and demand a refund, and also disable access to the app store via their network configuration. The outdated cached
result will be returned until it expires, providing access to an unpaid application. For this reason
the cache duration should not be made excessively long.

The default cache
duration is 30 days. This allows the device to be powered-down for anything less than that duration, and upon
powering-up, if the server is temporarily down for maintenance, the app will function normally without
the user being made aware. Each successful check-in with the server extends the cache by the
configured duration.

If the cache is disabled, any device in the field that makes a check-in request during Vuzix App Store
maintenance windows will be unable to validate the license, and will prevent access to the software.

The cache is stored locally on the device and clearing the application data will remove the cache.

### Grace Period
If the application is found to be unlicensed, either by the Vuzix App Store actively reporting that
the license has been terminated, or by the cache expiring while unable to communicate with the Vuzix
App Store API, a configurable grace period begins. During that
time the user will be alerted that the license is expired, but the application will continue to
function normally. This acts as a warning to force the user to renew, but does not impact their critical
workflows while they deal with the issue.

The default grace period is 7 days. This allows adequate time for the user to use the software for any
critical tasks, and then contact their purchasing department or your technical support team to
resolve the issue.

## Legal
Use of the SDK is available to developers agreeing to the
[VUZIX® SOFTWARE DEVELOPMENT KIT LICENSE AND CONFIDENTIALITY AGREEMENT](https://www.vuzix.com/pages/vuzix%C2%AE-software-development-kit-license-and-confidentiality-agreement)
