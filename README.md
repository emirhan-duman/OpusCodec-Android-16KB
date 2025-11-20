# OpusCodec-Android – 16KB Page-Size Compatible
Modern, fully rebuilt Opus Codec library for Android 15+ (Google Play 2025 requirement)

This project provides a fully 16KB page-aligned Opus Codec build for modern Android devices.
Google Play will reject 4KB-aligned native libraries starting from November 1, 2025.
This repository delivers a drop-in replacement for developers who need a working,
up-to-date, Android-friendly Opus implementation.

# It includes:

Modern CMake

Gradle 8+

AGP 8.5+

Xiph Opus 1.5.x source code

JNI wrapper (easyopus.cpp)

16KB-aligned .so binaries

Ready-to-use .aar output

# Features

✔ 16KB page-size aligned (Google Play 2025+)

✔ Built from official Xiph Opus source

✔ Modern Android Studio / Gradle / CMake

✔ JNI glue layer (easyopus.cpp, CodecOpus.cpp, SamplesConverter.cpp)

✔ Produces a standalone AAR

✔ Supports arm64-v8a

✔ Works on API 21+

✔ Plug-and-play: drop into any Android project

# Why This Exists

Google announced that:

Apps targeting Android 15+ must ship 16KB-aligned native libraries.
4KB-aligned .so files will be rejected on Google Play.

Almost all existing Opus libraries on GitHub and Maven Central are compiled for 4KB,
so they no longer pass Play Store requirements.

This repository provides a clean, modern, compliant solution.

# Project Structure
opuscodec/
 ├── src/main/
 │    ├── cpp/
 │    │    ├── easyopus.cpp
 │    │    ├── CodecOpus.cpp
 │    │    ├── SamplesConverter.cpp
 │    │    └── opus/      ← Xiph Opus source
 │    │
 │    ├── java/com/emirhan/opus/Opus.java
 │    └── AndroidManifest.xml
 ├── build.gradle
 ├── CMakeLists.txt
 └── settings.gradle

# Building the AAR

Clone the project:

git clone https://github.com/<your_user>/OpusCodec-Android-16KB.git
cd OpusCodec-Android-16KB


# Build the library:

./gradlew :opuscodec:assembleRelease


# Output:

opuscodec/build/outputs/aar/opuscodec-release.aar

# How to Use in Your App

## Copy AAR into:

app/libs/opuscodec-release.aar


## Add to app build.gradle:

implementation files('libs/opuscodec-release.aar')


## Use it:

val opus = Opus()
opus.encoderInit(48000, 1, 2048)

## 16KB Page-Size Check

To confirm alignment:

Build → Analyze APK → libeasyopus.so → LOAD → align: 0x4000

If you see 0x4000 (16384), alignment is correct.

# License

MIT License.
Free for personal and commercial use.
