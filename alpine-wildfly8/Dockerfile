FROM alpine-jdk8:1.0

MAINTAINER CloudWerkstatt

# http://download.jboss.org/wildfly/8.2.1.Final/wildfly-8.2.1.Final.tar.gz

ENV WILDFLY_VERSION 8.2.1.Final 
ENV JBOSS_HOME /opt/jboss/wildfly

RUN cd $HOME \
    && mkdir -p /opt/jboss \
    && curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz \
    && tar xfzv wildfly-$WILDFLY_VERSION.tar.gz -C /tmp \
    && mv /tmp/wildfly-$WILDFLY_VERSION $JBOSS_HOME \
    && rm wildfly-$WILDFLY_VERSION.tar.gz \
    && mkdir -p $JBOSS_HOME/standalone/{logs,data} \
    && chmod -R 777 $JBOSS_HOME \
    && adduser -D default

# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true 

# Expose the ports we're interested in 
EXPOSE 8080 


USER default

# Set the default command to run on boot 
# This will boot WildFly in the standalone mode and bind to all interface 
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
