
FROM aarongo/centos-java-supervisor

#Install supervisor
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum -y update  && yum -y install python-pip && /usr/bin/pip install supervisor
RUN mkdir -p /etc/supervisor/conf.d && mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisord.conf
VOLUME /var/log/supervisor
#Install sshd
RUN yum install -y openssh-server && sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
# select root pasword
RUN echo "root:pasword" | chpasswd && echo "root   ALL=(ALL)       ALL" >> /etc/sudoers &&\
    ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key &&\
    mkdir /var/run/sshd
#install apache 
RUN yum -y install httpd && mkdir /var/www/html/piwik
RUN yum -y install wget unzip
RUN yum -y install php php-mysql php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc  php-mbstring php-pdo 


#download piwik
RUN cd /tmp  && wget http://builds.piwik.org/piwik.zip && unzip piwik.zip 
RUN cd /tmp/piwik && mv  *  /var/www/html/piwik/ && chown -R apache:apache /var/www/html/piwik && chmod -R 755 /var/www/html/piwik/


EXPOSE 22 80
CMD ["/usr/bin/supervisord"]
