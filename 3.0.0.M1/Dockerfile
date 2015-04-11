FROM spantree/ubuntu-oraclejdk8:latest

MAINTAINER Cedric Hurst <cedric@spantree.net>

ENV GRAILS_VERSION 3.0.0.M1
ENV GRAILS_HOME /opt/grails
ENV PATH $PATH:$GRAILS_HOME/bin

# Install Grails
WORKDIR /tmp
RUN wget --quiet https://github.com/grails/grails-core/releases/download/v${GRAILS_VERSION}/grails-${GRAILS_VERSION}.zip && \
  jar -xf grails-${GRAILS_VERSION}.zip && \
  mv grails-${GRAILS_VERSION} /opt/grails && \
  chmod a+x /opt/grails/bin/grails && \
  find /opt/grails -iname "*-javadoc.jar" -o -iname "*-sources.jar" -exec rm -rf {} \; && \
  rm -rf grails-${GRAILS_VERSION}.zip

# Bootstrap cached dependencies by creating and compiling a temporary Grails project
# (must use underscore instead of hyphen in project name due to known issue in M1)
RUN /opt/grails/bin/grails create-app tmp_app && \
  cd tmp_app && \
  /opt/grails/bin/grails compile && \
  cd .. && \
  rm -Rf /tmp/*

# Mount the app
WORKDIR /app

EXPOSE 8080

CMD ["/opt/grails/bin/grails", "run-app"]
