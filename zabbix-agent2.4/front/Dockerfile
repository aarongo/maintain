FROM 172.31.1.160:5000/tomcat:front
MAINTAINER  aaron "aaron.docker@gmail.com"

COPY supervisord.conf /etc/supervisord.conf

#Install Zabbix_agentd
RUN yum -y install gcc
RUN cd /tmp && wget http://downloads.sourceforge.net/project/zabbix/ZABBIX%20Latest%20Stable/2.4.2/zabbix-2.4.2.tar.gz
RUN cd /tmp && tar xzf zabbix-2.4.2.tar.gz && groupadd zabbix && useradd -g zabbix zabbix
RUN cd /tmp/zabbix-2.4.2 && ./configure --prefix=/usr/local/zabbix_agent --enable-agent && make install

RUN cp /tmp/zabbix-2.4.2/misc/init.d/fedora/core/* /etc/init.d/ && cd /etc/init.d/ && chmod 755 zabbix_* &&\
    chkconfig --add zabbix_agentd &&\
    chkconfig zabbix_agentd on
#Install mount.nfs4
RUN yum -y install mount.nfs4
COPY ./zabbix_agentd.conf /usr/local/zabbix_agent/etc/zabbix_agentd.conf
ADD ./server.xml /usr/local/tomcat/conf/

EXPOSE 22 8080 10050
CMD ["/usr/bin/supervisord"]
