---
title: "Custom Filters in Fail2ban"
date: 2023-12-06 00:00:00 +0000
categories: [Cybersecurity]
tags: [fail2ban]    
author: Hamza Achahboune
layout: post
---


![img-description](/assets/img/Blog/fail2ban_conf.png)
# Example Configurations for Fail2Ban Custom Filters
### Blocking Failed WordPress Login Attempts :

WordPress is a popular content management system that is often targeted by hackers. You can use Fail2Ban to block failed login attempts to the WordPress admin panel. To create a custom filter for this, add the following code to a new filter configuration file:
```
[Definition]
failregex = .*authentication failure; logname=.*\s+ rhost=<HOST>(\s+ user=.*)?\s*$
ignoreregex =
```
Then, add the filter to the jail configuration file for WordPress:
```
[wordpress]
enabled  = true
filter   = wordpress
logpath  = /var/log/auth.log
port     = http,https
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the WordPress admin panel three times within 24 hours.

###  Blocking SSH Brute Force Attacks from Specific Countries
If you notice that most of the SSH brute force attacks on your server come from a specific country, you can create a custom filter to block those IP addresses. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = .*authentication failure; logname=.*\s+ rhost=<HOST>\s*$
ignoreregex =
```
Then, add the filter to the jail configuration file for SSH:
```
[ssh]
enabled  = true
filter   = ssh-country
logpath  = /var/log/auth.log
port     = ssh
maxretry = 3
bantime  = 86400
```
In this configuration, replace <COUNTRY> with the country code of the country you want to block. For example, to block all SSH brute force attacks from China, the filter configuration file should look like this:
```
[Definition]
failregex = .*authentication failure; logname=.*\s+ rhost=<HOST>\s*$
ignoreregex =
```
And the jail configuration file for SSH should look like this:
```
[ssh]
enabled  = true
filter   = ssh-china
logpath  = /var/log/auth.log
port     = ssh
maxretry = 3
bantime  = 86400
```
```
[ssh-china]
enabled  = true
filter   = ssh-country
logpath  = /var/log/auth.log
port     = ssh
maxretry = 3
bantime  = 86400
banaction = iptables-multiport[name=SSH, port="ssh", protocol=tcp]
banip    = <IP>
bantime.increment = true
bantime.factor = 1.5
bantime.maxtime = 2592000
```
This configuration will block all SSH brute force attacks from IP addresses in China.

###  Blocking Failed Mail Login Attempts
If you run a mail server, you can use Fail2Ban to block failed login attempts to the mail server. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = .*authentication failure; logname=.*\s+ rhost=<HOST>\s*$
ignoreregex =
```
Then, add the filter to the jail configuration file for mail:
```
[postfix]
enabled  = true
filter   = postfix-auth
logpath  = /var/log/mail.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the mail server three times within 24 hours.

###  Blocking Excessive HTTP Requests
If you run a web server, you can use Fail2Ban to block excessive HTTP requests from a single IP address. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST> -.*"(GET|POST|HEAD).* HTTP.*" (4[0-9]{2}|5[0-9]{2})
ignoreregex =
```
Then, add the filter to the jail configuration file for HTTP:
```
[http-get-dos]
enabled  = true
filter   = http-get-dos
logpath  = /var/log/apache2/access.log
maxretry = 300
findtime = 300
bantime  = 600
```
This configuration will block any IP address that makes more than 300 HTTP requests within 5 minutes.

###  Blocking Excessive SMTP Requests
If you run a mail server, you can use Fail2Ban to block excessive SMTP requests from a single IP address. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*SMTPD_PROXY.*Client host rejected: Access denied$
ignoreregex =
```
Then, add the filter to the jail configuration file for SMTP:
```
[postfix-smtp]
enabled  = true
filter   = postfix-smtp
logpath  = /var/log/mail.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that makes over 3 SMTP requests within 24 hours.

### Blocking Excessive SSH Requests
If you run an SSH server, you can use Fail2Ban to block excessive SSH requests from a single IP address. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*ssh.*$
ignoreregex =
```
Then, add the filter to the jail configuration file for SSH:
```
[ssh-ddos]
enabled  = true
filter   = ssh-ddos
logpath  = /var/log/auth.log
maxretry = 3
findtime = 300
bantime  = 86400
```
This configuration will block any IP address that makes over 3 SSH requests within 5 minutes.

###  Blocking Failed Nginx Login Attempts
If you run an Nginx web server with basic authentication, you can use Fail2Ban to block failed login attempts. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = .*user .* was not found in .*access log.*
ignoreregex =
```
Then, add the filter to the jail configuration file for Nginx:
```
[nginx-auth]
enabled  = true
filter   = nginx-auth
logpath  = /var/log/nginx/*error.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to Nginx three times within 24 hours.

###  Blocking Failed FTP Login Attempts
If you run an FTP server, you can use Fail2Ban to block failed login attempts. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.* \[.*\] FAILED LOGIN .*$
ignoreregex =
```
Then, add the filter to the jail configuration file for FTP:
```
[proftpd]
enabled  = true
filter   = proftpd
logpath  = /var/log/proftpd/proftpd.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the FTP server three times within 24 hours.

###  Blocking Excessive MySQL Requests
If you run a MySQL server, you can use Fail2Ban to block excessive requests from a single IP address. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*connect to mysql server.*
ignoreregex =
```
Then, add the filter to the jail configuration file for MySQL:
```
[mysqldos]
enabled  = true
filter   = mysqldos
logpath  = /var/log/mysql/mysql.log
maxretry = 3
findtime = 300
bantime  = 86400
```
This configuration will block any IP address that makes more than 3 MySQL requests within 5 minutes.

###  Blocking Failed SSH Login Attempts with Invalid Usernames
If you run an SSH server, you can use Fail2Ban to block failed login attempts with invalid usernames. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.* sshd.*invalid user.*
ignoreregex =
```
Then, add the filter to the jail configuration file for SSH:
```
[ssh-invaliduser]
enabled  = true
filter   = ssh-invaliduser
logpath  = /var/log/auth.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the SSH server with an invalid username three times within 24 hours.

###  Blocking Failed SMTP Login Attempts
If you run a mail server, you can use Fail2Ban to block failed login attempts to the SMTP server. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*authentication failed.*$
ignoreregex =
```
Then, add the filter to the jail configuration file for SMTP:
```
[postfix-sasl]
enabled  = true
filter   = postfix-sasl
logpath  = /var/log/mail.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the SMTP server three times within 24 hours.

###  Blocking Failed Dovecot Login Attempts
If you run a mail server with Dovecot, you can use Fail2Ban to block failed login attempts to the Dovecot server. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*dovecot.*:.*auth.*failed.*
ignoreregex =
```
Then, add the filter to the jail configuration file for Dovecot:
```
[dovecot]
enabled  = true
filter   = dovecot
logpath  = /var/log/mail.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the Dovecot server three times within 24 hours.

###  Blocking Excessive SSH Login Attempts from Specific IPs
If you notice that some IP addresses are making excessive SSH login attempts, you can use Fail2Ban to block them. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.* sshd.*
ignoreregex =
```
Then, add the filter to the jail configuration file for SSH:
```
[ssh-iptables]
enabled  = true
filter   = sshd
banaction = iptables-allports
logpath  = /var/log/auth.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that makes more than 3 SSH login attempts within 24 hours.

###  Blocking Excessive HTTP Requests from Specific IPs
If you notice that some IP addresses are making excessive HTTP requests, you can use Fail2Ban to block them. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*"(GET|POST|HEAD).* HTTP.*" (4[0-9]{2}|5[0-9]{2})
ignoreregex =
```
Then, add the filter to the jail configuration file for HTTP:
```
[apache-badbots]
enabled  = true
filter   = apache-badbots
logpath  = /var/log/apache2/access.log
maxretry = 2
bantime  = 86400
```
This configuration will block any IP address that makes more than 2 HTTP requests with a 4xx or 5xx response code within 24 hours.

###  Blocking Excessive SMTP Requests from Specific IPs
If you notice that some IP addresses are making excessive SMTP requests, you can use Fail2Ban to block them. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*SMTP.*$
ignoreregex =
```
Then, add the filter to the jail configuration file for SMTP:
```
[postfix-smtp-iptables]
enabled  = true
filter   = postfix-smtp-iptables
banaction = iptables-allports
logpath  = /var/log/mail.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that makes more than 3 SMTP requests within 24 hours.

###  Blocking Failed SSH Login Attempts with Specific Usernames
If you want to block failed SSH login attempts with specific usernames, you can use Fail2Ban to do so. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.* sshd.*Invalid user (user1|user2|user3).*
ignoreregex =
```
Then, add the filter to the jail configuration file for SSH:
```
[ssh-invaliduser-iptables]
enabled  = true
filter   = ssh-invaliduser
banaction = iptables-allports
logpath  = /var/log/auth.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the SSH server with the specified usernames three times within 24 hours.

###  Blocking Failed ProFTPD Login Attempts with Specific Usernames
If you want to block failed ProFTPD login attempts with specific usernames, you can use Fail2Ban to do so. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = proftpd:.*(:AUTH_FAILED:|USER user1|USER user2|USER user3)
ignoreregex =
```
Then, add the filter to the jail configuration file for ProFTPD:
```
[proftpd-iptables]
enabled  = true
filter   = proftpd
banaction = iptables-allports
logpath  = /var/log/proftpd/proftpd.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the ProFTPD server with the specified usernames three times within 24 hours.

###  Blocking Failed vsftpd Login Attempts with Specific Usernames
If you want to block failed vsftpd login attempts with specific usernames, you can use Fail2Ban to do so. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = vsftpd: pam_unix\(vsftpd:auth\): check pass; user unknown|FAIL LOGIN: Client "<HOST>"
ignoreregex =
```
Then, add the filter to the jail configuration file for vsftpd:
```
[vsftpd-iptables]
enabled  = true
filter   = vsftpd
banaction = iptables-allports
logpath  = /var/log/vsftpd.log
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the vsftpd server with the specified usernames three times within 24 hours.

###  Blocking Failed Pure-FTPd Login Attempts with Specific Usernames
If you want to block failed Pure-FTPd login attempts with specific usernames, you can use Fail2Ban to do so. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = pure-ftpd: \(.*@<HOST>\) \[WARNING\] Authentication failed for user [user1|user2|user3]
ignoreregex =
```
Then, add the filter to the jail configuration file for Pure-FTPd:
```
[pureftpd-iptables]
enabled  = true
filter   = pureftpd
banaction = iptables-allports
logpath  = /var/log/syslog
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the Pure-FTPd server with the specified usernames three times within 24 hours.

###  Blocking Failed Samba Login Attempts with Specific Usernames
If you want to block failed Samba login attempts with specific usernames, you can use Fail2Ban to do so. To do this, create a new filter configuration file with the following code:
```
[Definition]
failregex = ^<HOST>.*smbd.*Failed (password|publickey) for user (user1|user2|user3).*
ignoreregex =
```
Then, add the filter to the jail configuration file for Samba:
```
[samba-iptables]
enabled  = true
filter   = samba
banaction = iptables-allports
logpath  = /var/log/samba/log.%m
maxretry = 3
bantime  = 86400
```
This configuration will block any IP address that fails to log in to the Samba server with the specified usernames three times within 24 hours.
