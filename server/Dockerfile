FROM anroots/sensu-server

RUN apt-get update && \
  apt-get install -y bc build-essential && \
  /opt/sensu/embedded/bin/gem install sensu-plugins-slack sensu-plugins-mailer && \
  apt-get clean -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


COPY conf.d /etc/sensu/conf.d

CMD dockerize \
  -template /etc/sensu/conf.d/server.tmpl:/etc/sensu/conf.d/config.json \
  -template /etc/sensu/conf.d/api.tmpl:/etc/sensu/conf.d/api.json \
  /opt/sensu/bin/sensu-server -d /etc/sensu/conf.d
