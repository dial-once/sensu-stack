FROM alpine:latest
MAINTAINER Jonathan Muller

RUN apk add --no-cache python && \
    apk add --no-cache --virtual build-dependencies build-base wget py-pip openssl ca-certificates python-dev \
  && wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz && \
    tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz && \
    rm dockerize-linux-amd64-v0.2.0.tar.gz \
  && pip install --upgrade pip \
  && pip install --no-cache-dir whisper carbon \
  && apk del build-dependencies

COPY conf /etc/carbon/conf

VOLUME /opt/graphite/storage

CMD dockerize -template /etc/carbon/conf/carbon.conf.tmpl:/opt/graphite/conf/carbon.conf \
  && cp /opt/graphite/conf/storage-schemas.conf.example /opt/graphite/conf/storage-schemas.conf \
  && /opt/graphite/bin/carbon-cache.py --nodaemon start
