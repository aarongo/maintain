FROM aarongo/centos-zabbix-supervisor
MAINTAINER  aaron "aaron.docker@gmail.com"

RUN  yum install -y mysql-server mysql 
RUN /etc/init.d/mysqld start &&\  
  mysql -e "grant all privileges on *.* to 'root'@'%' identified by 'comall2014';"&&\  
    mysql -e "grant all privileges on *.* to 'root'@'localhost' identified by 'comall2014';"&&\  
   mysql -u root -pcomall2014 -e "show databases;" 
COPY supervisord.conf /etc/supervisord.conf

#Install zabbix
RUN  yum -y install wget tar httpd php mysql-devel gcc net-snmp-devel curl-devel perl-DBI php-gd php-mysql php-bcmath php-mbstring php-xml
RUN cd /tmp && wget http://downloads.sourceforge.net/project/zabbix/ZABBIX%20Latest%20Stable/2.4.2/zabbix-2.4.2.tar.gz
RUN cd /tmp && tar xzf zabbix-2.4.2.tar.gz && groupadd zabbix && useradd -g zabbix zabbix

#Configure Install zabbix 
RUN cd /tmp/zabbix-2.4.2 && ./configure --with-mysql --with-net-snmp --with-libcurl \
    --enable-server --enable-agent --enable-proxy --prefix=/usr/local/zabbix && make install && mkdir /var/www/html/zabbix
Copy php config to /var/www/html/
RUN cd /tmp/zabbix-2.4.2/frontends/php/ && cp -a . /var/www/html/zabbix
RUN ln -s /usr/local/zabbix/sbin/zabbix_server /usr/local/sbin/ && ln -s /usr/local/zabbix/sbin/zabbix_agentd /usr/local/sbin/
RUN cp /tmp/zabbix-2.4.2/misc/init.d/fedora/core/* /etc/init.d/ && cd /etc/init.d/ && chmod 755 zabbix_* &&\
    chkconfig --add zabbix_server &&\
    chkconfig --add zabbix_agentd &&\
    chkconfig zabbix_server on &&\
    chkconfig zabbix_agentd on 
COPY php.ini /etc/php.ini
VOLUME ["/zabbixdata"]

EXPOSE 22 80 3306 
CMD ["/usr/bin/supervisord"]


