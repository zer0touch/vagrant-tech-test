FROM zer0touch/sonarqube:latest

ENV SONAR_VERSION=6.7.2 \
    SONARQUBE_HOME=/opt/sonarqube \
    # Database configuration
    # Defaults to using H2
    SONARQUBE_JDBC_USERNAME=sonar \
    SONARQUBE_JDBC_PASSWORD=sonar \
    SONARQUBE_JDBC_URL=

# Http port
EXPOSE 9000

RUN set -x \
    wget https://sonarsource.bintray.com/Distribution/sonar-javascript-plugin/sonar-javascript-plugin-3.2.0.5506.jar -P /opt/sonarqube/extensions/plugins && \
    wget https://sonarsource.bintray.com/Distribution/sonar-go-plugin/sonar-go-plugin-0.2.0.875.jar -P /opt/sonarqube/extensions/plugins

VOLUME "$SONARQUBE_HOME/data"

WORKDIR $SONARQUBE_HOME
COPY run.sh $SONARQUBE_HOME/bin/
RUN \
  chown root:root $SONARQUBE_HOME/bin/run.sh ;\
  chmod 750 $SONARQUBE_HOME/bin/run.sh

ENTRYPOINT ["/opt/sonarqube/bin/run.sh"]

