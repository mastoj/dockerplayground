FROM      ubuntu:14.04.2
MAINTAINER Tomas Jansson <tomas.jansson@gmail.com>

ENV ES_VERSION 3.2.2

ADD http://download.geteventstore.com/binaries/EventStore-OSS-Ubuntu-v$ES_VERSION.tar.gz /tmp/
RUN tar xfz /tmp/EventStore-OSS-Ubuntu-v$ES_VERSION.tar.gz -C /opt

EXPOSE 3113
EXPOSE 2113
EXPOSE 1113
EXPOSE 2112
EXPOSE 1112

VOLUME /data/db
VOLUME /data/logs

ENV EVENTSTORE_MAX_MEM_TABLE_SIZE 100000
ENV EVENTSTORE_WORKER_THREADS 12

WORKDIR /opt/EventStore-OSS-Ubuntu-v$ES_VERSION

CMD internalip=$(hostname -i) && \
    ./run-node.sh --ext-http-prefixes=http://*:2113/ --ext-ip=0.0.0.0 \
    --int-ip=$internalip --db /data/db --log /data/logs --run-projections=all \
    --cluster-size=3 --cluster-dns 192.168.99.101 --cluster-gossip-port=2113
