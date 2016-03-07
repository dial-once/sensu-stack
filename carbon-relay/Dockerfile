FROM rounds/10m-graphite-carbon-relay
MAINTAINER Jonathan Muller

COPY relay-rules.conf.tmpl relay-rules.conf.tmpl

CMD dockerize \
  -template relay-rules.conf.tmpl:/etc/carbon/relay-rules.conf \
  /usr/bin/carbon-relay --nodaemon --config=/etc/carbon/carbon.conf --pidfile=/var/run/carbon-relay.pid --logdir=/var/log/carbon/ start
