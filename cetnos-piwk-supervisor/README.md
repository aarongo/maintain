centos piwik 
================
###supervisord.conf
    [supervisord]
    nodaemon=true
    [program:sshd]
    command=/usr/sbin/sshd -D
    #start apache
    [program:httpd]
    redirect_stderr=true
    command=/usr/sbin/httpd -DFOREGROUND
    process_name = httpd
### start piwik
        docker run -d -p 1031:22 -p 8090:80 --name piwik1 -h piwik1 --dns 172.17.42.1 172.31.1.160:5000/piwik
