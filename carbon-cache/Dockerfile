FROM rounds/10m-graphite-carbon-cache
MAINTAINER Jonathan Muller

COPY carbon.conf.tmpl carbon.conf.tmpl

CMD dockerize \
  -template carbon.conf.tmpl:/etc/carbon/carbon.conf \
  /usr/bin/carbon-cache --nodaemon --config=/etc/carbon/carbon.conf --pidfile=/var/run/carbon-cache.pid --logdir=/var/log/carbon/ start
