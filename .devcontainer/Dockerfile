# Use the official Node.js 18 image as a parent image
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:18

# Set environment variables for Android SDK
ENV ANDROID_SDK_ROOT=/usr/local/android-sdk-linux
ENV PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/emulator:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/tools:$ANDROID_SDK_ROOT/tools/bin

# Install required packages
RUN apt-get update && apt-get install -y \
    openjdk-17-jdk \
    gradle \
    unzip \
    wget

# Set JAVA_HOME environment variable
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64

# Install Android SDK Command Line Tools
RUN mkdir -p $ANDROID_SDK_ROOT/cmdline-tools && \
    cd $ANDROID_SDK_ROOT/cmdline-tools && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-8512546_latest.zip -O commandlinetools.zip && \
    unzip commandlinetools.zip && \
    rm commandlinetools.zip && \
    mv cmdline-tools latest

# Accept Android SDK licenses
RUN yes | sdkmanager --licenses

# Set the working directory
WORKDIR /workspace

# Copy project files into the container
COPY . /workspace

# Install n to manage Node versions and set Node.js version to 18.18.2
RUN npm install -g n && n 18.18.2

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Set Node.js version
RUN n use 18.18.2

# Verify installations
RUN java -version
RUN node -v
RUN npm -v
RUN gradle -v
RUN sdkmanager --version
