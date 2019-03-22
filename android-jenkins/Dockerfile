FROM jenkins/jenkins:2.168
MAINTAINER afirez <afirez.io@gmail.com>

USER root

# JAVA
RUN apt update
RUN apt-get install openjdk-8-jre -y
RUN ls /usr/lib/jvm/
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-amd64

# Gradle
ENV GRADLE_URL http://services.gradle.org/distributions/gradle-4.6-all.zip
ADD ${GRADLE_URL} gradle-4.6-bin.zip
RUN unzip -d /usr/local/ gradle-4.6-bin.zip && \
    ln -s /usr/local/gradle-4.6 /usr/local/gradle && \
    rm gradle-4.6-bin.zip
ENV GRADLE_HOME /usr/local/gradle
ENV PATH ${PATH}:${GRADLE_HOME}/bin
RUN echo "export PATH=${PATH}:${GRADLE_HOME}/bin" >> /etc/profile

# Node.js v8.9.2 by taobao mirrors
RUN wget https://npm.taobao.org/mirrors/node/v8.9.2/node-v8.9.2-linux-x64.tar.gz && \
    tar -C /usr/local --strip-components 1 -xzf node-v8.9.2-linux-x64.tar.gz && \
    rm node-v8.9.2-linux-x64.tar.gz

# yarn
RUN npm install -g yarn react-native-cli && \
    yarn config set registry https://registry.npm.taobao.org --global && \
    yarn config set disturl https://npm.taobao.org/dist --global

# android sdk
RUN mkdir -p opt/android/sdk \
    && chown -R jenkins.jenkins /opt/android/sdk \
    && cd opt/android/sdk/ \
    && curl https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip -o android-sdk.zip && unzip android-sdk.zip -d . && rm android-sdk.zip \
    && yes | ./tools/bin/sdkmanager --licenses \
    && ./tools/bin/sdkmanager "tools" \
    && ./tools/bin/sdkmanager "build-tools;28.0.3" "build-tools;27.0.3" "build-tools;22.0.1" "build-tools;19.1.0" "platforms;android-28" "platforms;android-27" "platforms;android-22" "platforms;android-19" "extras;android;m2repository" "extras;google;m2repository" --no_https \
    && ./tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2" "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" --no_https \
    && ./tools/bin/sdkmanager --list
ENV ANDROID_HOME /opt/android/sdk
ENV PATH ${PATH}:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN echo ANDROID_HOME="$ANDROID_HOME" >> /etc/profile

# drop back to the regular jenkins user - good practice
USER jenkins
