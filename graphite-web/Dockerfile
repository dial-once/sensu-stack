FROM rounds/10m-graphite-web
MAINTAINER Jonathan Muller

COPY local.settings.py.tmpl local.settings.py.tmpl

CMD dockerize \
  -template local.settings.py.tmpl:/etc/graphite/local_settings.py \
  gunicorn_django -b 0.0.0.0:80 /usr/lib/python2.7/dist-packages/graphite/settings.py
