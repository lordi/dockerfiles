FROM ksoichiro/android

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

RUN (while /bin/true; do sleep 1; echo y; done) | android update sdk --filter platform-tools,tools,android-17,extra-android-support,system-image,sys-img-armeabi-v7a-android-17 --all --no-ui --force

# Set up and run emulator
RUN echo no | android create avd --force -n test -t android-17
# Avoid emulator assumes HOME as '/'.
ENV HOME /root
ADD wait-for-emulator /usr/local/bin/
ADD start-emulator /usr/local/bin/

RUN mkdir -p /opt/tmp && android create project -g -v 0.9.+ -a MainActivity -k com.example.example -t android-17 -p /opt/tmp
RUN cd /opt/tmp && ./gradlew tasks
RUN rm -rf /opt/tmp

VOLUME /workspace
WORKDIR /workspace
