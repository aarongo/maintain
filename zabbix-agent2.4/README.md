zabbix-agent
========
###zabbix-agent install Centos-*-supervisor for zabbix-agent
		centos-memcached-supervisor
		centos-mongodb-supervisor
		centos-mysql-supervisor
		centos-solr-supervisor
		centos-ssh-supervisor
		centos-tomcat-supervisor
		cetnos-java-base
		zabbix-server2.4
###Start zabbix-agentd supervisord.conf
		[program:zabbix_agentd]
		command=/usr/local/zabbix_agent/sbin/zabbix_agentd
		user=zabbix
		startsecs=0
		autorestart=false
		redirect_stderr = true