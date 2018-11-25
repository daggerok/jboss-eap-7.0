# jboss-eap-7.0 [![Build Status](https://travis-ci.org/daggerok/jboss-eap-7.0.svg?branch=master)](https://travis-ci.org/daggerok/jboss-eap-7.0)
Patched JBoss EAP 7.0 (including __7.0.9 patch__) Docker automation build based on centos7 / alpine3.8 images

[daggerok/jboss-eap-7.0](https://hub.docker.com/r/daggerok/jboss-eap-7.0/)

## tags

- [latest](https://github.com/daggerok/jboss-eap-7.0/blob/master/Dockerfile)

- [7.0.9-alpine](https://github.com/daggerok/jboss-eap-7.0/blob/7.0.9-alpine/Dockerfile)
- [7.0.9-centos](https://github.com/daggerok/jboss-eap-7.0/blob/7.0.9-centos/Dockerfile)

- [7.0.1-alpine](https://github.com/daggerok/jboss-eap-7.0/blob/7.0.1-alpine/Dockerfile)
- [7.0.1-centos](https://github.com/daggerok/jboss-eap-7.0/blob/7.0.1-centos/Dockerfile)

- [7.0.0-alpine](https://github.com/daggerok/jboss-eap-7.0/blob/7.0.0-alpine/Dockerfile)
- [7.0.0-centos](https://github.com/daggerok/jboss-eap-7.0/blob/7.0.0-centos/Dockerfile)

## usage

### health check

```Dockerfile

FROM daggerok/jboss-eap-7.0:7.0.9-alpine
HEALTHCHECK --timeout=1s --retries=99 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/health \
         || exit 1
ADD ./target/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war

```

### multi deployment

```Dockerfile

FROM daggerok/jboss-eap-7.0:7.0.0-centos
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

### remote debug

```Dockerfile

FROM daggerok/jboss-eap-7.0:latest
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"
EXPOSE 5005
COPY ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

_ports_

- management: 9990
- web http: 8080
- https: 8443
