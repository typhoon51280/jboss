# JBOSS [![Build Status](https://travis-ci.org/daggerok/jboss.svg?branch=master)](https://travis-ci.org/daggerok/jboss)
automated build for docker hub

## JBOSS EAP
based on `openjdk:8u151-jdk-alpine` image

tags:

- eap-7.1
- eap-7.1-full
- eap-6.4

**Exposed ports**:

- 8080 - deployed apps http port
- 8009, 8083, 8093 - who cares ports...

### Usage (with healthcheck):

```

FROM daggerok/jboss:jboss-eap-7.1-full
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/health \
         || exit 1
ADD ./build/libs/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war

```

#### Remote debug / multi-build deployment:

```

FROM daggerok/jboss:jboss-eap-6.4
# Remote debug:
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
# Multi-builds deployment:
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

## JBOSS WildFly
based on Linux Alpine, OpenJDK 8u151

tags:

- wildfly-12.0.0.Final
- wildfly-11.0.0.Final
- wildfly-10.1.0.Final
- wildfly-10.0.0.Final
- wildfly-9.0.2.Final
- wildfly-9.0.1.Final
- wildfly-9.0.0.Final
- wildfly-8.2.0.Final
- wildfly-8.1.0.Final
- wildfly-8.0.0.Final

**Exposed ports**:

- 8080 - deployed apps http port
- 9990 - console port
- 8443 - https port

**Console**:

- url: http://127.0.0.1:9990/console
- user: admin
- password: Admin.123

### Usage:

```

FROM daggerok/jboss:wildfly-12.0.0.Final
ADD ./build/libs/*.war ${JBOSS_HOME}/standalone/deployments/

```

#### Remote debug:

```

FROM daggerok/jboss:wildfly-8.0.0.Final-alpine
RUN echo "JAVA_OPTS=\"\$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 \"" >> ${JBOSS_HOME}/bin/standalone.conf
EXPOSE 5005
COPY ./build/libs/*.war ./target/*.ear ${JBOSS_HOME}/standalone/deployments/

```

## JBOSS 6.1.0.Final

**Exposed ports**:

- 8080 - HTTP port
- 1009 - JNDI port
- 8009 - AJP 1.3 Connector port
- 8083 - RMI WebService port
- 8093 - MBean port

### Usage (with healthcheck):

```

FROM daggerok/jboss:6.1.0.Final
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/api/health \
         || exit 1
ADD ./build/libs/*.war ${JBOSS_HOME}/server/default/deploy/my-service.war

```

#### Remote debug / multi-build deployment:

```

FROM daggerok/jboss:6.1.0.Final
# Remote debug:
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
# Multi-builds deployment:
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/server/default/deploy/

```

## JBOSS 5.1.0.Final

**Exposed ports**:

- 8080 - HTTP port
- 1009 - JNDI port
- 8009 - AJP 1.3 Connector port
- 8083 - RMI WebService port
- 8093 - MBean port

### Usage (with healthcheck):

```

FROM daggerok/jboss:5.1.0.Final
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/api/health \
         || exit 1
ADD ./build/libs/*.war ${JBOSS_HOME}/server/default/deploy/my-service.war

```

#### Remote debug / multi-build deployment:

```

FROM daggerok/jboss:5.1.0.Final
# Remote debug:
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
# Multi-builds deployment:
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/server/default/deploy/

```

## JBOSS 4.2.3.GA
**tags**:

- 4.2.3.GA based on `openjdk:8u151-jre-alpine3.7` image
- 4.2.3.GA-java1.5 based on `lwis/java5` image

**Exposed ports**:

- 8080 - HTTP port
- 1009 - JNDI port
- 8009 - AJP 1.3 Connector port
- 8083 - RMI WebService port
- 8093 - MBean port

### Usage (with healthcheck):

```

FROM daggerok/jboss:4.2.2.GA-java1.5
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/api/health \
         || exit 1
ADD ./build/libs/*.war ${JBOSS_HOME}/server/default/deploy/my-service.war

```

#### Remote debug / multi-build deployment:

```

FROM daggerok/jboss:4.2.3.GA
# Remote debug:
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
# Multi-builds deployment:
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/server/default/deploy/

```

## JBOSS 4.2.2.GA
based on `openjdk:8u151-jre-alpine3.7` image

**Exposed ports**:

- 8080 - HTTP port
- 1009 - JNDI port
- 8009 - AJP 1.3 Connector port
- 8083 - RMI WebService port
- 8093 - MBean port

### Usage (with healthcheck):

```

FROM daggerok/jboss:4.2.2.GA
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/api/health \
         || exit 1
ADD ./build/libs/*.war ${JBOSS_HOME}/server/default/deploy/my-service.war

```

#### Remote debug / multi-build deployment:

```

FROM daggerok/jboss:4.2.2.GA
# Remote debug:
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
# Multi-builds deployment:
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/server/default/deploy/

```
