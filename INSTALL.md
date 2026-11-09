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
    implementation("io.fingerly:fingerly:0.1.0")
}
```

The SDK needs Android 5.0 (API 21) or newer, and its one transitive dependency
is `kotlinx-coroutines-android`.

## Shrinking

The R8 rules the SDK needs ship inside the library, so your app adds none of
its own.

## Upgrading

Change the version number. Every published version stays available, and a
published version never changes.

## Next

Follow the guide at <https://docs.fingerly.io/docs/sdks/android> to make your
first identification.
