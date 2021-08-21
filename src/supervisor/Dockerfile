FROM ubuntu:20.04

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]