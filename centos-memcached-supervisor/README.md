centos-memcached-supervisor
===========================
docker pull centos-memcached-supervisor

docker-supervisor-memcache 
-----------------------------------
### Superviso config
    [supervisord]
    nodaemon=true
    [program:sshd]
    command=/usr/sbin/sshd -D

    [program:tomcat]
    command = /usr/local/tomcat/bin/catalina.sh run
    stopasgroup = true
    redirect_stderr = true
    stdout_logfile = /var/log/supervisor/%(program_name)s.log
### Start docker supervisor memcache and sshd
  docker run -p 2222:22 -p 11211:11211 -it aarongo/centos-memcache-supervisor
