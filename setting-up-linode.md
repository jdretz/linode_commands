# Setting Up Remote Server
1.  Include SSH key when created ("Add Key")      # I have a couple on my desktop that I use 
2.  `$ ssh [root]@[ipaddress]`                    # Sign in to remote server
3.  `$ apt-get update && apt-get upgrade`         # Get server up-to-date
4.  `$ yes`                                       # when prompted 
5.  `$ hostnamectl set-hostname [new hostname]`   # Set hostname for server
6.  `$ nano /etc/hosts` ---> insert new line `[ipaddress]    [hostname]`  # In hosts file add IP address for remote server (host name from step 4), format the same as the `127.0.0.1` etc. line
7.  Save (Ctl+X), Accept (y) and exit (Enter)     
8.  `$ adduser [new username]`                    # Make the user that you will sign in with normalling
9.  Enter new password and personal information 
10.  `$ adduser [new username] sudo`               # Add them to the superuser group so they can execute `sudo` commands
11.  `$ exit`                                     # Log out of remote server
12.  `$ ssh [username]@[ipaddress]`               # Log in to remote server as new user
13.  Enter password 
14.  `$ mkdir -p ~/.ssh`                          # Set up folder for ssh key for new user
15.  `$ exit`                                     # Log out of remote server
16.  Generate key if necessary or use existing key locally   
17.  `$ scp ~/.ssh/id_rsa.pub [linode username]@[linode ipaddress]:~/.ssh/authorized_keys`  # Copy key from local server to remote
18.  `$ ssh [username]@[ipaddress]`               # Log in to remote server again
19.  `$ sudo chmod 700 ~/.ssh/`                   # Change permissions on ssh file
20.  `$ sudo chmod 600 ~/.ssh/*`                  # Change permisisons for files in ssh (i.e authorized keys)
21.  `$ exit`                                     # Log out of remote server
22.  `$ ssh [newusername]@[ip address]`           # test ssh connection
23.  `$ sudo nano /etc/ssh/sshd_config`           # Now that it works, time to change access configurations
24.  Set `PermitRootLogin no`                     # Find this line and change it from 'yes' to 'no'
25.  Uncomment and set `PasswordAuthentication no`        # Only going to use ssh key from now on
26.  Save (Ctl+X), Accept (y) and exit (Enter)
27.  `$ sudo systemctl restart sshd`              # Restart process to start new config
28.  `$ sudo apt-get install ufw` (may already be installed)      # Install Uncomplicated FireWall
29.  `$ sudo ufw default allow outgoing`          # Allow outgoing traffic on ports
30.  `$ sudo ufw default deny incoming`           # Deny all incoming traffic on ports
31.  `$ sudo ufw allow ssh`                       # Allow your own ssh connection on port 22
32.  Allow testing ports, or other ports deemed necessary
33.  `$ sudo ufw enable`                          # Start the firewall 
