ubuntu-mysql-supervisor
=======================
The frist: docker pull aarongo/ubuntu-ssh-supervisor
###supervisor config
    [supervisord]
    nodaemon=true
    [program:sshd]
    command=/usr/sbin/sshd -D

    [program:mysqld]
    command=/start
###Started ubuntu mysql
    docker run -p 1024:22 -p 3306:3306 -it -v /ubuntu-data:/var/lib/mysql aarongo/ubuntu-mysql-supervisor
