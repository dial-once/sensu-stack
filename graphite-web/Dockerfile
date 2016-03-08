FROM alpine:latest
MAINTAINER Jonathan Muller

RUN apk add --no-cache python py-pip && \
    apk add --no-cache --virtual build-dependencies build-base wget openssl ca-certificates python-dev \
  && wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz && \
    tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz && \
    rm dockerize-linux-amd64-v0.2.0.tar.gz \
  && pip install --upgrade pip \
  && pip install --no-cache-dir Django pytz graphite-web gunicorn django-tagging whisper \
  && apk del build-dependencies

COPY local.settings.py.tmpl local.settings.py.tmpl

VOLUME /opt/graphite/storage

EXPOSE 8000

CMD dockerize \
  -template local.settings.py.tmpl:/opt/graphite/webapp/graphite/local_settings.py \
  && mkdir -p /opt/graphite/storage/log/webapp \
  && cp /opt/graphite/conf/graphite.wsgi.example /opt/graphite/webapp/graphite/graphite_wsgi.py \
  && cd /opt/graphite/webapp/graphite \
  && python manage.py migrate --run-syncdb \
  && gunicorn -w 2 -b 0.0.0.0:8888 graphite_wsgi:application
  
