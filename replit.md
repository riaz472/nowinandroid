# Now in Android (NiA)

## Overview

**Now in Android** is a fully functional Android app built entirely with Kotlin and Jetpack Compose. It is a reference project by Google demonstrating modern Android architecture, modularization, and best practices. The app lets users browse Android development news, follow topics, and receive content matching their interests.

This is a **native Android application** — it is built with the Android Gradle Plugin and runs on Android devices/emulators. It does **not** run as a web application in the browser preview.

## Tech Stack

- **Language:** Kotlin (100%)
- **UI Framework:** Jetpack Compose (Material 3)
- **Architecture:** Multi-layered (UI → Domain → Data) with Unidirectional Data Flow (UDF)
- **Async:** Kotlin Coroutines + Flow
- **Dependency Injection:** Hilt (Dagger-Hilt)
- **Local Storage:** Room Database + DataStore
- **Networking:** Retrofit + Kotlinx Serialization
- **Image Loading:** Coil
- **Background Sync:** WorkManager
- **Build System:** Gradle (Kotlin DSL) with convention plugins in `build-logic/`
- **Dependency Management:** Gradle Version Catalogs (`gradle/libs.versions.toml`)

## Project Structure

```
app/                    - Main application entry point
app-nia-catalog/        - Standalone design system catalog app
feature/                - Feature modules (foryou, bookmarks, interests, etc.)
  ├── <name>/api/       - Public interfaces for the feature
  └── <name>/impl/      - Internal implementation
core/                   - Shared infrastructure
  ├── data/             - Repositories and data sources
  ├── database/         - Room database
  ├── designsystem/     - Material 3 theme and reusable UI
  ├── model/            - Shared data models
  ├── network/          - Retrofit API clients
  └── common/           - Shared utilities
sync/                   - WorkManager background sync
benchmarks/             - Performance tests and Baseline Profiles
build-logic/            - Custom Gradle convention plugins
```

## Build Variants

- **`demoDebug`** / **`demoRelease`** — Use local/mock data; can be built without a backend server (recommended for development)
- **`prodRelease`** — Uses Google's backend; requires internal credentials (not publicly available)

## How to Build

Java (GraalVM 22.3) is installed. Use the **"Build Android App"** workflow or run manually:

```bash
export JAVA_HOME=/nix/store/c8hr2f0b0dm685yx1dkp6bw24bpx495n-graalvm19-ce-22.3.1
./gradlew :app:assembleDemoDebug --no-daemon
```

The built APK will be at: `app/build/outputs/apk/demo/debug/app-demo-debug.apk`

To build the design system catalog app:
```bash
./gradlew :app-nia-catalog:assembleDebug --no-daemon
```

## Running Tests

```bash
./gradlew test --no-daemon
```

## Development Notes

- The project requires Android SDK to compile. The Gradle wrapper will attempt to download dependencies on first build.
- Use **Android Studio** (latest stable) for the best development experience — import the project root directly.
- The `demoDebug` variant is the recommended target for local development as it doesn't require backend credentials.

## User Preferences

- Use `demoDebug` build variant for local development
