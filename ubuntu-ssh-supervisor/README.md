ubuntu-ssh-supervisor
=====================
Subsequent operations base

###ubuntu-ssh-supervisor-configuration
    [supervisord]
    nodaemon=true
    [program:sshd]
    command=/usr/sbin/sshd -D
###Start ubuntu ssh
    docker run -p 1024:22 -it aarongo/ubuntu-ssh-supervisor
