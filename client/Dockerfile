FROM anroots/sensu-client

RUN apt-get update && \
  apt-get install -y bc build-essential && \
  /opt/sensu/embedded/bin/gem install sensu-plugins-memory-checks sensu-plugins-cpu-checks sensu-plugins-disk-checks sensu-plugins-docker sensu-plugins-rabbitmq sensu-plugins-redis sensu-plugins-slack && \
  apt-get clean -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY conf.d /etc/sensu/conf.d/

CMD dockerize \
  -template /etc/sensu/conf.d/rabbitmq.tmpl:/etc/sensu/conf.d/rabbitmq.json \
  -template /etc/sensu/conf.d/client.tmpl:/etc/sensu/conf.d/client.json \
  /opt/sensu/bin/sensu-client -d /etc/sensu/conf.d
