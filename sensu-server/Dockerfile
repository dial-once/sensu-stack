FROM dialonce/sensu

RUN gem install sensu-plugins-slack sensu-plugins-mailer

COPY conf.d /etc/sensu/conf.d

CMD dockerize \
  -template /etc/sensu/conf.d/server.tmpl:/etc/sensu/conf.d/config.json \
  -template /etc/sensu/conf.d/api.tmpl:/etc/sensu/conf.d/api.json \
  -template /etc/sensu/conf.d/handlers/slack.tmpl:/etc/sensu/conf.d/handlers/slack.json \
  -template /etc/sensu/conf.d/handlers/mailer.tmpl:/etc/sensu/conf.d/handlers/mailer.json \
  sensu-server -d /etc/sensu/conf.d
