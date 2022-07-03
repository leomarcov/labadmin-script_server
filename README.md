# Labadmin Script Server
Labadmin Script Server is a server repository to automate script execution on hosts when boot.
Scripts are stored on server and when hosts boots query the list of pending scripts to execute.

## Working schema
  * Script server works over SSH server, and use labadmin-script_server file to decide the list of script that need be executed by hosts.
  * When hosts boots:
    * Connect to server and exec labadmin-script_server to query the list of pending scripts.
    
  
