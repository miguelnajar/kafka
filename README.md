# kafka CONNECT DOCKER IMAGE

#Pluggins require you to download the latest versions and put the .jar files the correct directories.  The Dockerfile will need you to put the pluggin files into the right directories.  The links below are for the jars required for this version of the connector.
Couchbase:  https://packages.couchbase.com/clients/kafka/4.2.2/couchbase-kafka-connect-couchbase-4.2.2.zip
Pub/Sub:    https://repo1.maven.org/maven2/com/google/cloud/pubsub-group-kafka-connector/1.2.0/pubsub-group-kafka-connector-1.2.0.jar
MySQL:      https://repo1.maven.org/maven2/io/debezium/debezium-connector-mysql/2.6.2.Final/debezium-connector-mysql-2.6.2.Final-plugin.tar.gz
Snowflake:  https://repo1.maven.org/maven2/com/snowflake/snowflake-kafka-connector/2.2.2/snowflake-kafka-connector-2.2.2.jar

EXAMPLE: Dockerfile using quay.io/strimzi/kafka:0.41.0-kafka-3.7.0 as the base image:

FROM quay.io/strimzi/kafka:0.41.0-kafka-3.7.0
USER root:root
RUN mkdir -p /opt/kafka/plugins/debezium
RUN mkdir -p /opt/kafka/plugins/snowflake
RUN mkdir -p /opt/kafka/plugins/couchbase
RUN mkdir -p /opt/kafka/plugins/pubsub
# copy the properties files and jars
COPY ./plugins/debezium-connector-mysql-2.6.2/ /opt/kafka/plugins/debezium/
COPY ./plugins/snowflake-kafka-connector-2.2.2/ /opt/kafka/plugins/snowflake/
COPY ./plugins/couchbase-kafka-connect-couchbase-4.2.2/lib/ /opt/kafka/plugins/couchbase/
COPY ./plugins/pubsub-group-kafka-connector-1.2.0/ /opt/kafka/plugins/pubsub/
USER 1001


Example plugins file
$ tree ./plugins/
./plugins/
├── debezium-connector-mysql-2.6.2
│   ├── debezium-connector-mysql-2.6.2.jar
│   ├── debezium-core-2.6.2.jar
│   ├── LICENSE.txt
│   ├── mysql-binlog-connector-java-2.6.2.jar
│   ├── mysql-connector-java-2.6.2.jar
│   ├── README.md
│   └── # ...
├── snowflake-kafka-connector-2.2.2
│   ├── snowflake-kafka-connector-2.2.2.jar
