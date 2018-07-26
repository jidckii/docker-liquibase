#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for jidckii/liquibase:mysql
#    -- automatically generated  --
#+++++++++++++++++++++++++++++++++++++++

FROM openjdk:8-jre-slim

LABEL maintainer=jidckii@gmail.com 

ENV LIQUIBASE_VERSION="3.6.2" \
    MYSQL_DRIVER_VERSION="5.1.45" \
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
    && apt-get update \
    && apt-get install -yq --no-install-recommends wget \
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
&& chmod +x /opt/docker/bin/entrypoint.sh \
    && mkdir /liquibase \
    && ln -sf /opt/docker/bin/entrypoint.sh /entrypoint \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/* \
&& apt-get autoremove -y -f \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /liquibase
ENTRYPOINT ["/entrypoint"]
