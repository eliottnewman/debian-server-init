#Debian 12 server Initialization & SSh Hardening

#Project Overview

This project simulates a cloud server deployment using Debian 12.
The goal is to perform initial server setup and secure SSh access using key based authenication,also simulates real world cloud server initializetion process.

#Environment

-OS:Debain 12
-Virtualization:VMware
-Client:win11 powershell
-SSh key type:ed25519

##Objectives

-Basic server initialization
-Create none root user
-Configure SSh key-based login 
-Disable password authentication
-Disable root login
-Apply basic security hardening

--

##Step Perfoemed

###1.Install and boot Debian 12 VM
Config network and ensured SSh service are installed and running.

###2.Install and verify SSh server
Checked SSh status:
-sudo systemctl status ssh

###3.Generate SSh key(client)
Generate ed25519 key:
ssh-keygen -t ed25519

###4.Copy public key to server
-ssh-copy-id user@server_ip
Verified that the public key was added to:
~/.ssh/authorized_keys

###5.Disable password authentication
Modified SSh configuration file:
-/etc/ssh/sshd_config

Set:
PasswordAuthentication no
PermitRootLogin no

Restarted SSh:
sudo systemctl restart ssh

--

##Security Improvements

-Disable root login
-Disable password authentication
-Using key-based login only
-Created none root sudo user
-Verified corrent file permissions for ~/.ssh

--

##Result

Server can only be accessed via SSh key authentucation.
Password login is disable successfully.

##Troubleshooting

###Issue one: SSh service not found

Cause:OpenSSh server package was not installed.

Solution:
Installed OpenSSh server manially.

###Issue two:Connot connect after disabling password login

Cause:
Public key was not properly copied or incorrect file permissions.

Solution:
-Verified ~/.ssh/authorized_keys and file permissions.
-Checked permissions:
    -~/.ssh -> 700
    -authorized_keys -> 600