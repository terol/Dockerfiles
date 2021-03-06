#FROM andreptb/oracle-java:8-alpine

# Define environment variables.
ENV MULE_HOME /opt/mule
ENV MULE_VERSION 3.8.0
ENV MULE_DOWNLOAD_URL https://repository-master.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/${MULE_VERSION}/mule-standalone-${MULE_VERSION}.tar.gz

# Install NTPD for time synchronization.
RUN apk --no-cache add --virtual build-dependencies wget ca-certificates && \
    update-ca-certificates && \
# Create the /opt directory in which software in the container is installed.
    mkdir -p /opt && \
    cd /opt && \
# Install Mule ESB.
    wget ${MULE_DOWNLOAD_URL} && \
    tar xvzf mule-standalone-*.tar.gz && \
    rm mule-standalone-*.tar.gz && \
    mv mule-standalone-* mule && \
    rm -rf /tmp/* && \
    apk del --purge build-dependencies

# Define mount points.
VOLUME ["${MULE_HOME}/logs", "${MULE_HOME}/conf", "${MULE_HOME}/apps", "${MULE_HOME}/domains"]

# OepnShift runtime user
USER 1001

# copy app to apps folder
COPY sample-app_new.zip /opt/mule/apps/

# Define working directory.
WORKDIR /opt/mule

CMD [ "/opt/mule/bin/mule" ]

# Default http port
EXPOSE 8080
# JMX port.
EXPOSE 1099
