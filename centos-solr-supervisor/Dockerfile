FROM aarongo/solr-base
#FROM aarongo/centos-java-supervisor
MAINTAINER  aaron "aaron.docker@gmail.com"
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
#install tomcat
RUN java -version && yum -y install wget && yum -y install tar
RUN cd /tmp && wget http://www.us.apache.org/dist/tomcat/tomcat-7/v7.0.57/bin/apache-tomcat-7.0.57.tar.gz && cd /tmp && tar xzf apache-tomcat-7.0.57.tar.gz &&  mv apache-tomcat-7.0.57 /usr/local/tomcat && mkdir /solrdeploy && chmod +x /usr/local/tomcat/bin/*
ADD ./server.xml /usr/local/tomcat/conf/
ADD ./tomcat-users.xml /usr/local/tomcat/conf/
#Installing Apache Commons Loggins
RUN wget http://archive.apache.org/dist/commons/logging/binaries/commons-logging-1.1.3-bin.tar.gz &&\
    tar zxf commons-logging-1.1.3-bin.tar.gz && cd commons-logging-1.1.3 &&\
    cp commons-logging-*.jar /usr/local/tomcat/lib
#Installing SLF4J
RUN wget http://www.slf4j.org/dist/slf4j-1.7.7.tar.gz && tar xzf slf4j-1.7.7.tar.gz &&\
    cd slf4j-1.7.7 && cp slf4j-*.jar /usr/local/tomcat/lib
#Installing solr 
#RUN cd /tmp && wget http://mirrors.hust.edu.cn/apache/lucene/solr/4.8.1/solr-4.8.1.tgz && tar xzf solr-4.8.1.tgz 
RUN mkdir  /solrhome && cp /solr-4.8.1/dist/solr-4.8.1.war /solrdeploy/solr.war && cp -r /solr-4.8.1/example/solr /solrhome/
#ADD ./schema.xml /home/solr/collection1/conf/

VOLUME ["/solrdeploy"]
VOLUME ["/solrhome"]

EXPOSE 22 8080
CMD ["/usr/bin/supervisord"]
