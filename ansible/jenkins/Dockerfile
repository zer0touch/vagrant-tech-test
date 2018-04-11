FROM zer0touch/jenkins:alpine-latest

ADD https://github.com/aerokube/cm/releases/download/1.4.2/cm_linux_amd64 /usr/local/bin/cm
ADD https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.1.0.1141-linux.zip /tmp/sonar.zip

ENV PATH=$PATH:/opt/bin

RUN \
  apk add go openjdk8 bash wget musl-dev docker --update && \
  chmod 750 /usr/local/bin/cm && \
  cd /tmp && unzip sonar.zip && \
  mv /tmp/sonar-scanner-3.1.0.1141-linux /opt/ || echo exists && \
  rm -f /tmp/sonar.zip



