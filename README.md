# Labadmin Script Server
Labadmin Script Server is a server repository to automate script execution on hosts when boot, written in Bash.
  * Scripts are stored on server and when hosts boots query the list of pending scripts to execute.
  * Pending scripts to executed are selected by:
    * Regular expresión according hostname: only host with hostname match regular expresion script are executed.
    * Select script: each script has a select function to personalize if script is executed (each time, only if no had a correct execution, 

## Working schema
  * Script server works over SSH server, and use `labadmin-script_server` file to decide the list of script that need be executed by hosts.
  * When hosts boots:
    * Connect to server and exec `labadmin-script_server` to query the list of pending scripts.
    
  
## Install
  * Congig SSH server and config as you need
```bash
apt install openssh-server
vi /etc/ssh/sshd_config
systemctl restart ssh.service
 ```
  * Create dedicated user
```bash
adduser labadmin
 ```
  * Copy or clone proyect (preferred in `/opt` dir)
```bash
cd /opt
git clone https://github.com/leomarcov/labdmin-script_server
 ```
