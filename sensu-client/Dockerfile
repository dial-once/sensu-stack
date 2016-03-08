FROM dialonce/sensu

RUN gem install sensu-plugins-memory-checks sensu-plugins-cpu-checks sensu-plugins-disk-checks sensu-plugins-docker sensu-plugins-rabbitmq sensu-plugins-redis sensu-plugins-slack

COPY conf.d /etc/sensu/conf.d

CMD dockerize \
  -template /etc/sensu/conf.d/client.tmpl:/etc/sensu/conf.d/client.json \
  -template /etc/sensu/conf.d/default_checks.tmpl:/etc/sensu/conf.d/default_checks.json \
  sensu-client -d /etc/sensu/conf.d
