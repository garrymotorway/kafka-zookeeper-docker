FROM alpine:3.14

RUN apk update
RUN apk add bash

WORKDIR tmp

# Install Java
RUN apk add openjdk11-jre
ENV JAVA_HOME "/usr"

# Install Kafka
RUN wget https://dlcdn.apache.org/kafka/3.1.2/kafka_2.13-3.1.2.tgz
RUN tar -zxf kafka_2.13-3.1.2.tgz
RUN cp -R kafka_2.13-3.1.2 /usr/local/kafka/

# Configure Kafka
COPY ./server.properties /usr/local/kafka/config/server.properties

RUN mkdir /tmp/kafka-logs

RUN mkdir /app
COPY ./start-kafka.sh /app/
RUN chmod +x /app/start-kafka.sh

WORKDIR /usr/local/kafka/bin

ENTRYPOINT [ "/app/start-kafka.sh" ]

# ENTRYPOINT ["tail", "-f", "/dev/null"]