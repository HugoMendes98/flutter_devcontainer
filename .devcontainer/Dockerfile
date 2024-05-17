# https://github.com/instrumentisto/flutter-docker-image
FROM instrumentisto/flutter:3.22

# Add some utilities
RUN apt-get update && \
    apt-get install -y vim bash-completion

# Remove git config from parent image
RUN git config --global --unset user.name && git config --global --unset user.email

# Also inspired from https://github.com/budtmo/docker-android

RUN /opt/android-sdk-linux/cmdline-tools/latest/bin/sdkmanager --licenses && \
    /opt/android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "emulator"

# Install android 34 (Same as the sdk from the docker image)
RUN /opt/android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "system-images;android-34;default;x86_64"
# Device 30 = Pixel 7 pro
RUN echo no | /opt/android-sdk-linux/cmdline-tools/latest/bin/avdmanager create avd -n "Emulated_Android" -k "system-images;android-34;default;x86_64"  --device "30"  --force
