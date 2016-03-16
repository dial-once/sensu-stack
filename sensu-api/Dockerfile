FROM dialonce/sensu

MAINTAINER Julien Kernec'h <jkernech@dial-once.com>

ENV API_USER=WqNu4awAaNoP API_PASS=abcXvzSqoSw7

COPY conf.d /etc/sensu/conf.d

EXPOSE 4567

CMD dockerize \
  -template /etc/sensu/conf.d/config.tmpl:/etc/sensu/conf.d/config.json \
	sensu-api -d /etc/sensu/conf.d
