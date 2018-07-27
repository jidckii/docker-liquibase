#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for jidckii/liquibase:mysql
#    -- automatically generated  --
#+++++++++++++++++++++++++++++++++++++++

FROM openjdk:8-jre-alpine

LABEL maintainer=jidckii@gmail.com 

ENV LIQUIBASE_VERSION="3.6.2" \
    MYSQL_DRIVER_VERSION="5.1.45" \
    SLF4J_VERSION="1.7.25" \
    LIQUIBASE_DRIVER="com.mysql.jdbc.Driver" \
    LIQUIBASE_CLASSPATH="/opt/mysql-connector-java/mysql.jar" \
    LIQUIBASE_URL="" \
    LIQUIBASE_USERNAME="" \
    LIQUIBASE_PASSWORD="" \
    LIQUIBASE_CHANGELOG="liquibase.xml" \
    LIQUIBASE_CONTEXTS="" \
    LIQUIBASE_OPTS=""

COPY conf/ /opt/docker/

RUN set -x \
    && apk add --no-cache wget \
&& wget -q -O /tmp/mysql-connector-java.tar.gz "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-${MYSQL_DRIVER_VERSION}.tar.gz" \
    && tar -xzf /tmp/mysql-connector-java.tar.gz -C /opt/ mysql-connector-java-${MYSQL_DRIVER_VERSION}/mysql-connector-java-${MYSQL_DRIVER_VERSION}-bin.jar \
    && mv /opt/mysql-connector-java-${MYSQL_DRIVER_VERSION} /opt/mysql-connector-java \
    && mv /opt/mysql-connector-java/mysql-connector-java-${MYSQL_DRIVER_VERSION}-bin.jar /opt/mysql-connector-java/mysql.jar \
    && rm -f /tmp/mysql-connector-java.tar.gz \
&& wget -q -O /tmp/liquibase.tar.gz "https://github.com/liquibase/liquibase/releases/download/liquibase-parent-${LIQUIBASE_VERSION}/liquibase-${LIQUIBASE_VERSION}-bin.tar.gz" \
    && mkdir -p /opt/liquibase \
    && tar -xzf /tmp/liquibase.tar.gz -C /opt/liquibase \
    && rm -f /tmp/liquibase.tar.gz \
    && chmod +x /opt/liquibase/liquibase \
    && ln -s /opt/liquibase/liquibase /usr/local/bin/ \
&& wget -q -O /opt/liquibase/lib/slf4j-api-${SLF4J_VERSION}.jar http://central.maven.org/maven2/org/slf4j/slf4j-api/${SLF4J_VERSION}/slf4j-api-${SLF4J_VERSION}.jar \
&& chmod +x /opt/docker/bin/entrypoint.sh \
    && mkdir /liquibase \
    && ln -sf /opt/docker/bin/entrypoint.sh /entrypoint

WORKDIR /liquibase
ENTRYPOINT ["/entrypoint"]
