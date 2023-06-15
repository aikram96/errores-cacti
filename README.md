# How to solve common issues installing cacti

Trying to install **cacti** on **centos7** on my virtual box was causing some issues. After hours of doing research, I found out how to solve them. 

# Cacti

First, we need to understand what **cacti** is. Cacti is an open-source tool for monitoring systems (servers and network in real-time) where you can *analyze*, *interpret*, and *control* different env variables by visual charts. 

> First, we need to install **centos7** on your virtual box.

## Common Errors

### MariaDB issues

The issues related to MariaDB were caused by the timezone. To solve them you can try the following steps:

- [ ] Enter to MariaDB
	> #mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p mysql

- [ ]  Enter your password
	> Enter ur password: ****

- [ ]  Configure your timezone
	> #mysql> use mysql;
	
	> #mysql> GRANT SELECT ON mysql.time_zone_name TO cactiuser@localhost;


	> #mysql> flush privileges;

### Spine issues

When you are facing a spine issue is not possible to validate the **cacti** dashboard on the web. To solve the issue, review the following extract:

Install some dependencies

	> #yum -y install autoconf automake gcc mysql mysql-devel net-snmp-devel libtool openssl-devel dos2unix
	> #cd /tmp

Install the same version of **cacti** for **spine**

	> #wget http://www.cacti.net/downloads/spine/cacti-spine-1.1.16.tar.gz 
	> #tar xzvf cacti-spine-1.1.16.tar.gz
	> #cd cacti-spine-1.1.16
	> #./bootstrap
	> #./configure
	> #make
	> #make install
	> #chown root:root /usr/local/spine/bin/spine
	> #chmod +s /usr/local/spine/bin/spine
	> #ls -lt /usr/local/spine/bin/
	> #cp spine.conf.dist /etc/spine.conf

When you open the **spine.conf** you should see

	> #vi /etc/spine.conf
		>/usr/local/spine/bin/spine

Finally, you can reload the cacti dashboard on the web platform. No more issues would be displayed!

