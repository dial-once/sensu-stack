FROM alpine:latest

MAINTAINER Julien Kernec'h <jkernech@dial-once.com>

# Update base packages
RUN apk update && apk upgrade

# Install base packages and ruby gem dependencies
RUN apk add --no-cache build-base ca-certificates wget libffi-dev

# Install ruby and ruby-bundler
RUN apk add --no-cache ruby-dev ruby-bundler

# Do not install Gem documentation when installing gems
RUN echo "install: --no-rdoc --no-ri" >> /etc/gemrc

# Install sensu gem
RUN gem install sensu

# Install dockerize
RUN wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz \
	&& tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz
