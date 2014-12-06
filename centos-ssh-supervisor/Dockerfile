FROM centos:centos6
MAINTAINER  aaron "aaron.docker@gmail.com"

#Install supervisor
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum -y update  && yum -y install python-pip && /usr/bin/pip install supervisor
RUN mkdir -p /etc/supervisor/conf.d && mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisord.conf
VOLUME /var/log/supervisor

#install sshd 
RUN yum install -y openssh-server && sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
# select root pasword
RUN echo "root:pasword" | chpasswd && echo "root   ALL=(ALL)       ALL" >> /etc/sudoers
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN mkdir /var/run/sshd

EXPOSE 22
CMD ["/usr/bin/supervisord"]
