FROM ubuntu:20.04

RUN DEBIAN_FRONTEND=noninteractive apt update && apt install -y --no-install-recommends tzdata
RUN DEBIAN_FRONTEND=noninteractive apt install -y bash wget curl file git unzip xz-utils zip openjdk-8-jre-headless pkg-config clang cmake ninja-build libgtk-3-dev

# Android SDK
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip 
RUN mkdir android-sdk && unzip /sdk-tools-linux-4333796.zip -d android-sdk
RUN rm /sdk-tools-linux-4333796.zip
ENV ANDROID_HOME="/android-sdk"
ENV PATH="/android-sdk/tools/bin:/android-sdk/build-tools:/android-sdk/platform-tools:${PATH}"

# SDK manager
RUN yes | sdkmanager --licenses
RUN sdkmanager "platforms;android-29" "platform-tools" "build-tools;29.0.3" "cmdline-tools;latest"

# Flutter
RUN wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.0.5-stable.tar.xz
RUN tar xf flutter_linux_3.0.5-stable.tar.xz
RUN rm flutter_linux_3.0.5-stable.tar.xz
ENV PATH="/flutter/bin:${PATH}"

# next line counters issue: fatal: detected dubious ownership in repository at '/flutter'
RUN git config --global --add safe.directory /flutter

RUN flutter config --no-analytics
RUN flutter precache

# Set a useful default shell
ENV SHELL /bin/bash

