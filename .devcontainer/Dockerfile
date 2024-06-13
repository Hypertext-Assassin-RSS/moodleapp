# Use the official Node.js 14 image as a parent image
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:14

# Set environment variables for Android SDK
ENV ANDROID_HOME=/usr/local/android-sdk-linux
ENV ANDROID_SDK_ROOT=$ANDROID_HOME
ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/emulator:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/build-tools/30.0.3

# Install required packages
RUN apt-get update && apt-get install -y \
    libsecret-1-dev \
    openjdk-11-jdk \
    gradle \
    unzip \
    wget \
    libsecret-1-dev

# Set JAVA_HOME environment variable
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

# Install Android SDK Command Line Tools
RUN mkdir -p $ANDROID_HOME/cmdline-tools && \
    cd $ANDROID_HOME/cmdline-tools && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-8512546_latest.zip -O commandlinetools.zip && \
    unzip commandlinetools.zip && \
    rm commandlinetools.zip && \
    mv cmdline-tools latest

# Accept Android SDK licenses
RUN yes | sdkmanager --licenses

# Install Android build tools 30.0.3
RUN sdkmanager "platform-tools" "build-tools;30.0.3"

# Set the working directory
WORKDIR /workspace

# Copy project files into the container
COPY . /workspace

# Install n to manage Node versions and set Node.js version to 14.15.0
RUN npm install -g n && n 14.15.0

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Verify installations
RUN java -version
RUN node -v
RUN npm -v
RUN gradle -v
RUN sdkmanager --version
