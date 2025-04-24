FROM ubuntu:jammy

# --------- ENV + ARG Definitions ---------
ENV ANDROID_SDK_ROOT=/usr/lib/android-sdk
ENV FLUTTER_SDK_ROOT=/home/dev/flutter
ENV DEBIAN_FRONTEND=noninteractive

ARG FLUTTER_VERSION=stable
ARG ANDROID_API_LEVEL=34
ARG BUILD_TOOLS_VERSION=34.0.0

ENV PATH="${PATH}:${FLUTTER_SDK_ROOT}/bin:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools"

# --------- Install OS Dependencies ---------
RUN apt-get update && apt-get install -y \
    curl git unzip xz-utils zip libglu1-mesa openjdk-17-jdk wget \
    clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev \
    && rm -rf /var/lib/apt/lists/*

# --------- Download Android SDK Tools ---------
RUN mkdir -p ${ANDROID_SDK_ROOT}/cmdline-tools && \
    wget -O commandlinetools.zip "https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip" && \
    unzip commandlinetools.zip -d ${ANDROID_SDK_ROOT}/cmdline-tools && \
    mv ${ANDROID_SDK_ROOT}/cmdline-tools/cmdline-tools ${ANDROID_SDK_ROOT}/cmdline-tools/latest && \
    rm commandlinetools.zip

# --------- Install Android SDK Components ---------
RUN yes | ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager --licenses > /dev/null && \
    ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager \
    "platform-tools" \
    "platforms;android-${ANDROID_API_LEVEL}" \
    "build-tools;${BUILD_TOOLS_VERSION}" \
    --verbose

# --------- Install Flutter ---------
RUN git clone https://github.com/flutter/flutter.git $FLUTTER_SDK_ROOT --depth 1 --branch ${FLUTTER_VERSION} && \
    flutter config --no-analytics && \
    flutter precache && \
    flutter doctor

SHELL ["/bin/bash", "-c"]
