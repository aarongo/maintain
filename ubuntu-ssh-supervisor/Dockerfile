
FROM ubuntu:14.04
MAINTAINER  aaron "aaron.docker@gmail.com"

RUN apt-get update \
 && apt-get install -y openssh-server \
 && mkdir /var/run/sshd \
 && echo 'root:pasword' | chpasswd \
 && sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
 && sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config \
 && apt-get install -y --no-install-recommends supervisor \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ADD ./supervisord.conf /etc/supervisor/supervisord.conf


EXPOSE 22 

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
