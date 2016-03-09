FROM dialonce/sensu

RUN gem install sensu-plugins-slack sensu-plugins-mailer

RUN wget https://github.com/opower/sensu-metrics-relay/archive/master.tar.gz \
  && tar -xzf master.tar.gz \
  && mkdir -p /etc/sensu/extensions \
  && cp -R sensu-metrics-relay-master/lib/sensu/extensions/* /etc/sensu/extensions

COPY conf.d /etc/sensu/conf.d

CMD dockerize \
  -template /etc/sensu/conf.d/server.tmpl:/etc/sensu/conf.d/config.json \
  -template /etc/sensu/conf.d/api.tmpl:/etc/sensu/conf.d/api.json \
  -template /etc/sensu/conf.d/handlers/slack.tmpl:/etc/sensu/conf.d/handlers/slack.json \
  -template /etc/sensu/conf.d/handlers/mailer.tmpl:/etc/sensu/conf.d/handlers/mailer.json \
  -template /etc/sensu/conf.d/relays/carbon.tmpl:/etc/sensu/conf.d/config_relay.json \
  sensu-server -d /etc/sensu/conf.d
