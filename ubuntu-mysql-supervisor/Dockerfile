FROM aarongo/ubuntu-ssh-supervisor
MAINTAINER  aaron "aaron.docker@gmail.com"

RUN apt-get update \
  && apt-get install -y  mysql-server \
  && rm -rf /var/lib/mysql/mysql \
  && rm -rf /var/lib/apt/lists/* 
ADD start /start
ADD ./supervisord.conf /etc/supervisor/supervisord.conf
RUN chmod 755 /start

EXPOSE 22 3306
VOLUME ["/ubuntu-data"]
VOLUME ["/run/mysqld"]

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
