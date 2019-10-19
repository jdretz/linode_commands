# Setting Up a Linode
1.  Include SSH key when created ("Add Key")
2.  `ssh [root]@[ipaddress]`
3.  `apt-get update && apt-get upgrade`
4.  when prompted `yes`
4.  `hostnamectl set-hostname [new hostname]`
5.  `nano /etc/hosts` ---> insert new line `[ipaddress]    [hostname]` (host name from step 4)
6.  Save (Ctl+X), Accept (y) and exit (Enter)
7.  `adduser [new username]`
8.  Enter new password and personal information
9.  `adduser [new username] sudo`
10.  `exit`
11.  `ssh [username]@[ipaddress]`
12.  Enter password
13.  `mkdir -p ~/.ssh`
14.  `exit`
14.  Generate key if necessary or use existing key locally
15.  `scp ~/.ssh/id_rsa.pub [linode username]@[linode ipaddress]:~/.ssh/authorized_keys`
16.  `sudo chmod 700 ~/.ssh/`
17.  `sudo chmod 600 ~/.ssh/*`
18.  `exit`
19.  test ssh connection `ssh [newusername]@[ip address]`
20.  `sudo nano /etc/ssh/sshd_config`
21.  Set "PermitRootLogin no"  
22.  Uncomment and set "PasswordAuthentication no"
23.  Save (Ctl+X), Accept (y) and exit (Enter)
24.  `sudo systemctl restart sshd`
25.  `sudo apt-get install ufw` (may already be installed)
26.  `sudo ufw default allow outgoing`
27.  `sudo ufw default deny incoming`
28.  `sudo ufw allow ssh`
29.  Allow testing ports, or other ports deemed necessary
30.  `sudo ufw enable`
