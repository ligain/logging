# Logging  practice
There is 2 servers: **web** and **log**. **web** has a nginx server which produced logs. **log** is a remote server to collect logs.

- all critical logs from **web** must be stored locally and sent on the **log**  
- access and error logs from nginx have to be sent on the **log**  
- audit logs (when nginx config changes) have to be sent on the **log** 

# Run  
0) `vagrant` and `Ansible` should be installed on your system
```
$ vagrant -v
Vagrant 2.2.5
$ ansible --version
ansible 2.9.1
...
```
1) Clone this repository
```bash  
$ git clone https://github.com/ligain/logging.git  
``` 
2) Go to project folder
```bash  
$ cd logging/
```  
3) Run `Vagrantfile`
```bash  
$ vagrant up
```
4) Nginx logs on the **log**
![nginx_logs](https://raw.githubusercontent.com/ligain/logging/master/screenshots/nginx_logs.png)

5) Nginx audit logs on the **log**
![nginx_audit_log](https://raw.githubusercontent.com/ligain/logging/master/screenshots/nginx_audit_log.png)

# Project Goals 
The code is written for educational purposes.
