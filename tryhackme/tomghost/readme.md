### Writeup of THM TomGhost


#### Enumeration
1. We start with running nmap. We see that there are 4 open ports: 22(ssh), 53(tcpwrapped), 8009(ajp), 8080(apche tomcat)
![nmap output](./tomghost/resources/nmap.png)
2. On running dirb, we were not able to find many open directories.
#### Foothold
1. After a bit of googling, we were able to find about GhostCat vulnerabiliy (CVE-2020-1938). It has a module in metasploit which we used to get access to 
/WEB-INF/web.xml [module name: admin/http/tomcat_ghostcat].
#### Getting flags
##### Flag 1
1. We were able to get the username:skyfuck and the user's password from the web.xml allowing us to ssh as the user:
![ssh to skyfuck](./tomghost/resources/user_directory.png)
2. We were able to get the first flag at /home/merlin/user.txt

##### Privilege Escalation
1. We have access to the gpg key and the encrypted file in the user skyfuck's home directory. However, we need passphrase 
to decrypt.
![check passphrase](./tomghost/resources/passphrase.png)
2. We copy the key and the encrypted file to our local machine using scp. We then use gpg2john to convert the tryhackme.asc file to a format which john understands
using the command: gpg2john tryhackme.asc > try. 
3. We then use john to get the passphrase.
![john output](./tomghost/resources/john_output.png)
4. We can use the passphrase to decrypt credential.gpg:
![decryption output](./tomghost/resources/gpg_decrypt.png)
5. We can switch user to merlin using the credential we got. When we checked the sudo permission on merlin, we were able to see that the user can 
run zip using sudo.                                                                                                               
![jmerlin sudo permission](./tomghost/resources/sudo_permission.png)
6. We can use the following command to get root access
![escalation privilege](./tomghost/resources/priv_esc.png) 
7. We finally got the second key at /root:                                                                      
![john output](./tomghost/resources/sec_flag.png)
