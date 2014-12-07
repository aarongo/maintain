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
