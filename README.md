# Android Template for Termux

[🇧🇷](README_BR.md)

This GitHub template simplifies the process of setting up an Android development environment directly inside **Termux**. It automatically installs the Android SDK when you run `./gradlew`, allowing you to build and manage Android apps on your device with ease.


## Prerequisites

Before using the template, make sure to update your packages and install the necessary dependencies in Termux:

```bash
pkg update
pkg upgrade # optional
pkg install openjdk-17 aapt2
```

*Ensure you have enough storage space and a stable internet connection for downloading components.*


## Running the Project

To set up the SDK and dependencies automatically, simply run:

```bash
./gradlew
```

On the first run, Gradle will download the Android SDK and required build tools based on the configuration defined in `gradle.properties`.


### How to Build the APK

Once the dependencies are set up, you can build the APK using the following command:

```bash
./gradlew assembleDebug
```

The APK file will be generated at:

```
app/build/outputs/apk/debug/app-debug.apk
```

To install it on your device:

1. Copy the APK to your Downloads folder:

   ```bash
   cp app/build/outputs/apk/debug/app-debug.apk /sdcard/Download/
   ```
2. Open a file manager on your phone.
3. Navigate to the **Download** folder.
4. Tap on the APK file to install it (make sure unknown sources are allowed).


## Configuration via `gradle.properties`

The core project settings and Android dependencies are configured in the `gradle.properties` file:

```properties
# App Information
APP_PACKAGE=com.example.myapp
APP_VERSION=1.0
APP_VERSION_CODE=1
APP_MIN_SDK_VERSION=21
APP_TARGET_SDK_VERSION=33

# Android Dependencies
ANDROID_COMPILE_SDK_VERSION=33
ANDROID_BUILD_TOOLS_VERSION=33.0.2
ANDROID_GRADLE_PLUGIN_VERSION=8.3.0

# aapt2 binary path for Termux
android.aapt2FromMavenOverride=/data/data/com.termux/files/usr/bin/aapt2
# org.gradle.jvmargs=-Xmx512m -XX:MaxPermSize=256m
```

These variables are injected into your Gradle configuration automatically, making it easy to customize without touching the build files directly.


## Java Configuration

Java version compatibility is set in `app/build.gradle`:

```groovy
compileOptions {
    sourceCompatibility JavaVersion.VERSION_17
    targetCompatibility JavaVersion.VERSION_17
}
```

This ensures compatibility with modern libraries and uses the OpenJDK 17 installed via Termux.


## Tip: Limit Gradle Memory Usage

Running Gradle on mobile devices can be memory-intensive and may cause freezes or crashes. To reduce this risk, you can limit memory usage by adding the following to your `gradle.properties`:

```properties
org.gradle.jvmargs=-Xmx512m -XX:MaxPermSize=256m
```

Adjust the values according to your device’s available RAM (e.g., `-Xmx256m` for low-memory devices).


## Contributing

Feel free to fork, customize, and contribute to this template. It’s designed for developers who want to build Android apps directly on their phones without heavy IDEs.
