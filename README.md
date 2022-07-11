# vikas-ready-project

# Set Environment Variables
ENV SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip" \
    ANDROID_HOME="/usr/local/android-sdk" \
    ANDROID_VERSION=29

# Download Android SDK
RUN mkdir "$ANDROID_HOME" .android \
    && cd "$ANDROID_HOME" \
    && curl -o sdk.zip $SDK_URL \
    && unzip sdk.zip \
    && rm sdk.zip \
    && mkdir "$ANDROID_HOME/licenses" || true \
    && echo "24333f8a63b6825ea9c5514f83c2829b004d1fee" > "$ANDROID_HOME/licenses/android-sdk-license" \
    && yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses

# Install Android Build Tool and Libraries
RUN $ANDROID_HOME/tools/bin/sdkmanager --update
RUN $ANDROID_HOME/tools/bin/sdkmanager "build-tools;30.0.2" \
    "platforms;android-${ANDROID_VERSION}" \
    "platform-tools"
    
 SDK_URL="https://dl.google.com/android/repository/commandlinetools-linux-8512546_latest.zip"
ANDROID_HOME="/home/mindbowser/POC/firbase-email-password-login-Android-master/android-sdk"
sdk_root="/home/mindbowser/POC/firbase-email-password-login-Android-master/android-sdk"
ANDROID_VERSION=31
mkdir "$ANDROID_HOME" .android
cd "$ANDROID_HOME" \
&& curl -o sdk.zip $SDK_URL \
&& unzip sdk.zip \
&& rm sdk.zip
mkdir "$ANDROID_HOME/licenses" || true
echo "2ccbda4302db862a28ada25aa7425d99dce9462046003c1714b059b5c47970d8" > "$ANDROID_HOME/licenses/android-sdk-license"
yes | $ANDROID_HOME/cmdline-tools/bin/sdkmanager --sdk_root={ANDROID_HOME} --licenses
$ANDROID_HOME/cmdline-tools/bin/sdkmanager --sdk_root={ANDROID_HOME} --update
fastlane android build --env dev
