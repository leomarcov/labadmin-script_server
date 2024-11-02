# Labadmin Script Server
<img align="left" src="https://cdn4.iconfinder.com/data/icons/online-marketing-hand-drawn-vol-1/52/coding__development__programming__html__php__script__webcoding-128.png">

**Labadmin Script Server** is a server repository to automate script execution on hosts during booting time. Its written in Bash shellscript and connection is managed over SSH.

Scripts are organized in repsitories and each time hosts boots query if there are pending scripts to exec. In that case download and exec them.


&nbsp; 
# Working schema
  * Script server works over SSH server, and use `labadmin-script_server` file to decide the list of script that need be executed by hosts.
  * When hosts boots:
    * Connect to server and exec `labadmin-script_server` to query the list of pending scripts.
  * Scripts are stored on server and when hosts boots query the list of pending scripts to execute.
  * Pending scripts to execute are selected by:
    * **Regular expresión** according **hostname**: only host with hostname match regular expresion script are executed.
    * **Select script**: each script has a select function to personalize if script is executed (each time, only if no had a correct execution.
  
# Install
  * Copy or clone proyect (preferred in `/opt` dir)
```bash
cd /opt
git clone https://github.com/leomarcov/labadmin-script_server
 ```
 * Config SSH server and config as you need. Make sure `PubkeyAuthentication` is allowed.
```bash
apt install openssh-server
vi /etc/ssh/sshd_config
  Port 58889
  PubkeyAuthentication yes

systemctl restart ssh.service
 ```
  * Create dedicated user for agent and admin
```bash
adduser --disabled-password lss-agent 			# Only login with private key
adduser --disabled-password lss-admin  			# Only login with private key
```
  * Set permissions for agent and admin user
```bash
chown lss-admin:lss-agent /opt/labadmin-script_server
chmod 750 /opt/labadmin-script_server
chown -R lss-admin:lss-admin /opt/labadmin-script_server/repositories/

# Make sure ssh user has write permission to log files!:
find /opt/labadmin-script_server/repositories/ -type f -name log -exec chmod a+w {} \;
touch /opt/labadmin-script_server/log; chown lss-admin:lss-agent /opt/labadmin-script_server/log; chmod g+w /opt/labadmin-script_server
 ```
  * Generate SSH private and public keys for client (hosts) authentications
```bash
ssh-keygen
 ```
  * Copy private and public keys
```bash
# Public key must be inserted into lss-agent user authorized_keys file
mkdir -p /home/lss-agent/.ssh
cat id_rsa.pub >> /home/lss-agent/.ssh/authorized_keys
chmod 600 /home/lss-agent/.ssh/authorized_keys
chown -R lss-agent:lss-agent /home/lss-agent/.ssh

# Private key is used for each agent client. Copy and config this key in hosts
```



&nbsp;  
# Lincense
Labadmin Script Server license is [GPLv3](LICENSE)

# Contact
My name is Leonardo Marco. I'm sysadmin teacher in [CIFP Carlos III](https://cifpcarlos3.es/), Cartagena, Murcia (Spain).
