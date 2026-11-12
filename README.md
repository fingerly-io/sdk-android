<p align="center">
  <a href="https://fingerly.io">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/fingerly-io/.github/main/assets/logo-dark.svg">
      <img src="https://raw.githubusercontent.com/fingerly-io/.github/main/assets/logo-light.svg" alt="Fingerly" height="44">
    </picture>
  </a>
</p>

<p align="center"><b>Fingerly for Android</b><br>Device intelligence and fraud signals for Android apps, from a compiled library on Maven.</p>

<p align="center">
  <a href="https://maven.fingerly.io/io/fingerly/fingerly/maven-metadata.xml"><img src="https://img.shields.io/maven-metadata/v?metadataUrl=https%3A%2F%2Fmaven.fingerly.io%2Fio%2Ffingerly%2Ffingerly%2Fmaven-metadata.xml&amp;style=flat-square&amp;label=maven" alt="Latest version on Maven"></a>
  <img src="https://img.shields.io/badge/Android-5.0%20(API%2021)%2B-3DDC84?style=flat-square" alt="Android 5.0 (API 21) or newer">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-Proprietary-lightgrey?style=flat-square" alt="Licence: proprietary"></a>
  <a href="https://docs.fingerly.io/docs/sdks/android"><img src="https://img.shields.io/badge/docs-docs.fingerly.io-informational?style=flat-square" alt="Documentation"></a>
</p>

<p align="center"><img src="https://raw.githubusercontent.com/fingerly-io/.github/main/assets/banner.webp" alt="Fingerly" width="100%"></p>

## What is this

The Fingerly SDK for Android apps. It returns a request ID for each action you tag, such as a signup, a login or a checkout. Your backend uses that ID to read the result and decide. [Fingerly](https://fingerly.io) is a device intelligence API that helps you protect signups, logins and payments from fraud and abuse.

This repository holds the installation notes and licence for the SDK. The SDK is distributed as a compiled library from `https://maven.fingerly.io`, and no source is published.

## Getting started

1. **Get a key.** In the [Fingerly dashboard](https://dashboard.fingerly.io), open **Integration > SDK keys** and create a public key for your app. [How keys work](https://docs.fingerly.io/docs/api-keys).
2. **Add the dependency.**

   ```kotlin
   repositories {
       maven { url = uri("https://maven.fingerly.io") }
   }

   dependencies {
       implementation("io.fingerly:fingerly:0.2.0")
   }
   ```

   [INSTALL.md](INSTALL.md) has the details, including the optional installed-app checks (`io.fingerly:fingerly-app-checks`), the optional Play Integrity provider (`io.fingerly:fingerly-play-integrity`) and the answers for Google Play's Data safety form.

3. **Identify.**

   ```kotlin
   import io.fingerly.sdk.Fingerly
   import io.fingerly.sdk.core.ConsentState

   val fingerly = Fingerly.load(
       context,
       apiKey = "fly_pk_production_...",
       consent = ConsentState.GRANTED, // only once you have consent or another lawful basis
   )
   val result = fingerly.identify(tag = "checkout")

   // Send result.requestId to your backend and decide there.
   ```

Use a publishable SDK key from the dashboard. Secret keys are refused.

## Requirements

Android 5.0 (API 21) or newer.

## Documentation

Guides and the API reference are at <https://docs.fingerly.io/docs/sdks/android>.

## Help

Open an issue on this repository, or write to <support@fingerly.io>. Security issues: <security@fingerly.io>.

## Licence

The SDK is proprietary. Its use is governed by the terms in [LICENSE](LICENSE).
