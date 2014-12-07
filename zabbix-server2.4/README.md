zabbix-server
===================
NOTE:连接mysql时执行sql文件 顺序为 schema images data
Error：zabbix_server.log 没有报任何错误 但是前台报zabbix_server not running
解决：更改安装时最后生成的zabbix.conf.php
###zabbix.conf.php
		<?php
		// Zabbix GUI configuration file
		global $DB;

		$DB['TYPE']     = 'MYSQL';
		$DB['SERVER']   = 'localhost';
		$DB['PORT']     = '0';
		$DB['DATABASE'] = 'zabbix';
		$DB['USER']     = 'zabbix';
		$DB['PASSWORD'] = 'zabbix';

		// SCHEMA is relevant only for IBM_DB2 database
		$DB['SCHEMA'] = '';

		$ZBX_SERVER      = 'localhost';(****)               
		$ZBX_SERVER_PORT = '10051';
		$ZBX_SERVER_NAME = '';

		$IMAGE_FORMAT_DEFAULT = IMAGE_FORMAT_PNG;
		?>
###supervisord.conf
		[supervisord]
		nodaemon=true
		[program:sshd]
		command=/usr/sbin/sshd -D

		[program:httpd]
		redirect_stderr=true
		command=/usr/sbin/httpd -DFOREGROUND
		process_name = httpd

		[program:zabbix_server]
		redirect_stderr=true
		command=/usr/local/zabbix/sbin/zabbix_server
		process_name=zabbix_server

		[program:zabbix_agentd]
		redirect_stderr=true
		command=/usr/local/zabbix/sbin/zabbix_agentd
		process_name=zabbix_agentd

		[program:mysqld]
		command=/etc/init.d/mysqld start
###Start zabbix_server
		docker run -p 1050:22 -p 8089:80 -p 3307:3306-it --name zabbix_server  -v /zabbixdata:/var/lib/mysql aarongo/centos-zabbix-supervisor
