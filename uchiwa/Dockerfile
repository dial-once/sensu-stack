FROM alpine:latest

MAINTAINER Julien Kernec'h <jkernech@dial-once.com>

# Update base packages
RUN apk update && apk upgrade

# Install base packages and ruby gem dependencies
RUN apk add --no-cache ca-certificates wget git go godep nodejs

# Set go env
ENV GOROOT /usr/lib/go
ENV GOPATH /gopath
ENV GOBIN /gopath/bin
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

# Checkout the source
RUN go get github.com/sensu/uchiwa

# Set the workdir
WORKDIR $GOPATH/src/github.com/sensu/uchiwa

# Install npm/bower dependencies
RUN npm install bower -g && bower --allow-root install

RUN ls $GOPATH/src/github.com/sensu/uchiwa/public/bower_components/

# Remove bower and nodejs
RUN npm uninstall bower -g && apk del git nodejs

ENV HTTP_USER=hiro HTTP_PASS=nakamura SENSU_NAME="Sensu" UCHIWA_HOST="0.0.0.0" UCHIWA_PORT=80 UCHIWA_REFRESH=5

EXPOSE 80

RUN wget https://github.com/jwilder/dockerize/releases/download/v0.0.4/dockerize-linux-amd64-v0.0.4.tar.gz && \
	tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.0.4.tar.gz && \
	mkdir /etc/uchiwa

COPY config.tmpl /etc/uchiwa/

CMD dockerize -template /etc/uchiwa/config.tmpl:/etc/uchiwa/config.json \
  godep go run uchiwa.go -c /etc/uchiwa/config.json
