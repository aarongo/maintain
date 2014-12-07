zabbix-server
===================
<<<<<<< HEAD
NOTE:Á¬½ÓmysqlÊ±Ö´ÐÐsqlÎÄ¼þ Ë³ÐòÎª schema images data
Error£ºzabbix_server.log Ã»ÓÐ±¨ÈÎºÎ´íÎó µ«ÊÇÇ°Ì¨±¨zabbix_server not running
½â¾ö£º¸ü¸Ä°²×°Ê±×îºóÉú³ÉµÄzabbix.conf.php
=======
NOTE:è¿žæŽ¥mysqlæ—¶æ‰§è¡Œsqlæ–‡ä»¶ é¡ºåºä¸º schema images data
Errorï¼šzabbix_server.log æ²¡æœ‰æŠ¥ä»»ä½•é”™è¯¯ ä½†æ˜¯å‰å°æŠ¥zabbix_server not running
è§£å†³ï¼šæ›´æ”¹å®‰è£…æ—¶æœ€åŽç”Ÿæˆçš„zabbix.conf.php
>>>>>>> f064216c19704b9850cfce4062696b5ca4df3bce
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
<<<<<<< HEAD
		docker run -p 1050:22 -p 8089:80 -it --name zabbix_server  -v /zabbixdata:/var/lib/mysql aarongo/centos-zabbix-supervisor
=======
		docker run -p 1050:22 -p 8089:80 -p 3307:3306-it --name zabbix_server  -v /zabbixdata:/var/lib/mysql aarongo/centos-zabbix-supervisor
>>>>>>> f064216c19704b9850cfce4062696b5ca4df3bce
