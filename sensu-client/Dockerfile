FROM dialonce/sensu

MAINTAINER Julien Kernec'h <jkernech@dial-once.com>

RUN gem install \
  sensu-plugins-memory-checks \
  sensu-plugins-cpu-checks \
  sensu-plugins-disk-checks \
  sensu-plugins-docker \
  sensu-plugins-rabbitmq \
  sensu-plugins-redis

COPY conf.d /etc/sensu/conf.d

CMD dockerize \
  -template /etc/sensu/conf.d/client.tmpl:/etc/sensu/conf.d/client.json \
  -template /etc/sensu/conf.d/checks/rabbitmq.tmpl:/etc/sensu/conf.d/checks/rabbitmq.json \
  sensu-client -d /etc/sensu/conf.d
