# Fingerly for Android

Device intelligence and fraud signals for Android apps. This repository holds
the installation notes and licence for the SDK. The SDK is distributed as a
compiled library from `https://maven.fingerly.io`, and no source is published.

Requires Android 5.0 (API 21) or newer.

## Install

```kotlin
repositories {
    maven { url = uri("https://maven.fingerly.io") }
}

dependencies {
    implementation("io.fingerly:fingerly:0.2.0")
}
```

See [INSTALL.md](INSTALL.md) for the details, including the optional
installed-app checks (`io.fingerly:fingerly-app-checks`), the optional Play
Integrity provider (`io.fingerly:fingerly-play-integrity`) and the answers for
Google Play's Data safety form.

## Use

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

## Documentation

Guides and the API reference are at <https://docs.fingerly.io/docs/sdks/android>.

## Support

Email <support@fingerly.io>.

## Licence

The SDK is proprietary. Its use is governed by the terms in [LICENSE](LICENSE).
