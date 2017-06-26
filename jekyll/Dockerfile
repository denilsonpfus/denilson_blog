FROM ubuntu:16.04
MAINTAINER Denilson Ferreira <denilsonpfus@gmail.com>
ENV REFRESHED_AT 2017-06-26 17:20

RUN apt-get -yqq update
RUN apt-get -yqq install ruby ruby-dev build-essential nodejs
RUN gem install jekyll -v 2.5.3

VOLUME /data
VOLUME /var/www/html
WORKDIR /data

ENTRYPOINT [ "jekyll", "build", "--destination=/var/www/html" ]