FROM alpine:latest
MAINTAINER Jonathan Muller

RUN apk --no-cache add \
    python \
    python-dev \
    py-pip \
    openssl \
    build-base \
  && wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz \
  && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz \
  && pip install https://github.com/graphite-project/ceres/tarball/master \
  && pip install whisper carbon

COPY carbon.conf.tmpl carbon.conf.tmpl

VOLUME /opt/graphite/storage

CMD dockerize -template carbon.conf.tmpl:/opt/graphite/conf/carbon.conf \
  && cp /opt/graphite/conf/storage-schemas.conf.example /opt/graphite/conf/storage-schemas.conf \
  && /opt/graphite/bin/carbon-cache.py --nodaemon start
