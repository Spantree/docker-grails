FROM dockerfile/java:oracle-java8

MAINTAINER Cedric Hurst <cedric@spantree.net>

ENV GRAILS_VERSION 3.0.0

# Install Grails
WORKDIR /tmp
RUN wget --quiet https://github.com/grails/grails-core/releases/download/v${GRAILS_VERSION}/grails-${GRAILS_VERSION}.zip && \
  unzip grails-${GRAILS_VERSION}.zip && \
  mv grails-${GRAILS_VERSION} /opt/grails

# Bootstrap dependencies by creating and compiling a temporary Grails project
WORKDIR /tmp
RUN /opt/grails/bin/grails create-app tmp-app && \
  cd tmp-app && \
  /opt/grails/bin/grails compile && \
  cd .. && \
  rm -Rf tmp-app

# Mount the app
WORKDIR /
RUN mkdir /app
WORKDIR /app

EXPOSE 8080

CMD ["/opt/grails/bin/grails", "run-app"]