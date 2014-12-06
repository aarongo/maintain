FROM centos:centos6
MAINTAINER  aaron "aaron.docker@gmail.com"

RUN yum search java | grep -i --color JDK &&\
    yum -y install java-1.7.0-openjdk java-1.7.0-openjdk-devel &&\
    ls -l /usr/lib/jvm/ &&\
    echo "export JAVA_HOME=/usr/lib/jvm/jre-1.7.0-openjdk.x86_64" >> /etc/profile

CMD bash -l
