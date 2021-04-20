FROM openjdk:11.0-jre-slim

LABEL maintainer "ltoddy <taoliu0509@gmail.com>"

ENV EK_VERSION=7.12.0

RUN apt update \
 && apt install -y wget sudo \
 && useradd -m -s /bin/bash elasticsearch \
 && echo elasticsearch ALL=NOPASSWD: ALL >/etc/sudoers.d/elasticsearch \
 && chmod 440 /etc/sudoers.d/elasticsearch

USER elasticsearch

WORKDIR /elastic

EXPOSE 9200 5601

RUN wget -q -O - https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${EK_VERSION}-no-jdk-linux-x86_64.tar.gz | tar -zx \
 && mkdir -p elasticsearch-${EK_VERSION}/data \
 && wget -q -O - https://artifacts.elastic.co/downloads/kibana/kibana-${EK_VERSION}-linux-x86_64.tar.gz | tar -zx

CMD elasticsearch-${EK_VERSION}/bin/elasticsearch -E http.host=0.0.0.0 --quiet & kibana-${EK_VERSION}-linux-x86_64/bin/kibana --allow-root --host 0.0.0.0 -Q
