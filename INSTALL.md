# Installing Fingerly for Android

## Add the repository

If your project declares repositories centrally, add this to
`settings.gradle.kts`:

```kotlin
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url = uri("https://maven.fingerly.io") }
    }
}
```

Otherwise add the `maven` line to the `repositories` block of your module's
`build.gradle.kts`.

## Add the dependency

```kotlin
dependencies {
    implementation("io.fingerly:fingerly:0.2.0")
}
```

The SDK needs Android 5.0 (API 21) or newer, and its one transitive dependency
is `kotlinx-coroutines-android`.

By default the SDK declares no other app in your manifest and asks about none.

## Optional: installed-app checks

The checks for well-known root managers, hooking-framework managers and app
cloners are a separate artifact, because Google Play treats the list of
installed apps as personal and sensitive data and asks your app to justify the
package visibility it declares. Add it only if your app can:

```kotlin
dependencies {
    implementation("io.fingerly:fingerly:0.2.0")
    implementation("io.fingerly:fingerly-app-checks:0.2.0")
}
```

It has no code: it adds a `<queries>` block naming seventeen packages and a
flag that turns the checks on. Keep both artifacts on the same version; Gradle
refuses to mix them. If you add it, declare "App activity: Installed apps" in
your Data safety form.

## Optional: Play Integrity

The core SDK takes nothing from Google Play services. To add Google's Play
Integrity verdicts to your Fingerly events, add the provider and pass it to
`load` with your app's Google Cloud project number:

```kotlin
dependencies {
    implementation("io.fingerly:fingerly:0.2.0")
    implementation("io.fingerly:fingerly-play-integrity:0.2.0")
}
```

```kotlin
val fingerly = Fingerly.load(
    context,
    apiKey = "fly_pk_production_…",
    integrityTokenProvider = PlayIntegrityTokenProvider(context, cloudProjectNumber = 123456789012L),
)
```

It needs Android 6.0 (API 23) or newer. Upload your Cloud project's service
account key to your Fingerly project's platform credentials; until then the
server never asks for a token and the provider does nothing. Keep both
artifacts on the same version; Gradle refuses to mix them. From React Native,
Flutter or Lynx, add the artifact to the app's Android module and pass
`playIntegrityCloudProjectNumber` to the bridge's `load`.

## Google Play Data safety

What this SDK collects, for your app's Data safety form. Every purpose is
"Fraud prevention, security, and compliance", and nothing is shared.

| Data type | Collected | What it is |
|---|---|---|
| Location: Approximate location | Yes | Coarse location derived from the IP address on the server |
| Device or other IDs | Yes | A random install ID and the key attestation certificate chain |
| App activity: App interactions | Yes | Launch count, install age |
| App activity: Installed apps | Only with `fingerly-app-checks` | Three yes/no values: a root manager, a hooking-framework manager, an app cloner is installed |
| App info and performance: Diagnostics | Yes | Device model and OS build, hardware class, display, battery, free-storage share, network transport, VPN and proxy, whether any accessibility service is on (yes or no), boot and mount state, hashes of library and thread names |

- **Encrypted in transit:** yes. The SDK sends only over HTTPS.
- **Deletion requests:** yes, through your app: `Fingerly.deleteStoredIdentity`
  on the device, and the management API's "Erase a visitor" from your backend.
  Do not claim automatic deletion within 90 days: an identity is kept up to 180
  days after it was last seen.
- **Not shared:** Fingerly processes the data as your service provider, only
  for your organisation and on your instructions, with no store that crosses
  customers. If you combine Fingerly results across several of your own apps
  or clients, answer that for yourself.

## Shrinking

The R8 rules the SDK needs ship inside the library, so your app adds none of
its own.

## Upgrading

Change the version number, of both artifacts if you use the installed-app
checks. Every published version stays available, and a published version never
changes.

Versions after 0.1.0 no longer put the `<queries>` block in the core artifact.
To keep the installed-app checks, add `fingerly-app-checks`.

## Next

Follow the guide at <https://docs.fingerly.io/docs/sdks/android> to make your
first identification.
