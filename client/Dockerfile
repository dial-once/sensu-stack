FROM anroots/sensu-client

RUN apt-get update && \
  apt-get install -y bc build-essential git && \
  gem install sensu-plugins-memory-checks sensu-plugins-cpu-checks sensu-plugins-disk-checks sensu-plugins-docker sensu-plugins-rabbitmq bundler && \
  apt-get clean -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY conf.d /etc/sensu/conf.d/

CMD dockerize \
  -template /etc/sensu/conf.d/rabbitmq.tmpl:/etc/sensu/conf.d/rabbitmq.json \
  -template /etc/sensu/conf.d/client.tmpl:/etc/sensu/conf.d/client.json \
  -template /etc/sensu/conf.d/default_checks.tmpl:/etc/sensu/conf.d/default_checks.json \
  /opt/sensu/bin/sensu-client -d /etc/sensu/conf.d
