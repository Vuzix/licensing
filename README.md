
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

## Legal
Use of the SDK is available to developers agreeing to the
[VUZIX® SOFTWARE DEVELOPMENT KIT LICENSE AND CONFIDENTIALITY AGREEMENT](https://www.vuzix.com/pages/vuzix%C2%AE-software-development-kit-license-and-confidentiality-agreement)
