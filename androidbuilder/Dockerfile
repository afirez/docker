FROM ubuntu:16.04
MAINTAINER afirez "afirez.io@gmail.com"

RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends openjdk-8-jdk unzip curl && \
    apt-get clean
ENV USR_LOCAL /usr/local
ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
RUN curl -L "${ANDROID_SDK_URL}" | tar --no-same-owner -xz -C ${USR_LOCAL}
ENV ANDROID_HOME ${USR_LOCAL}/android-sdk-linux
ENV ANDROID_SDK ${USR_LOCAL}/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN echo "export PATH=${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools" >> /etc/profile

ENV ANDROID_SDK_COMPONENTS tools,platform-tools,build-tools-19.1.0,build-tools-22.0.1,build-tools-27.0.3,build-tools-28.0.3,android-19,android-22,android-27,android-28,extra-android-m2repository,extra-google-m2repository

RUN echo y | android update sdk --no-ui --all --filter "${ANDROID_SDK_COMPONENTS}"

ENV TERM dumb
