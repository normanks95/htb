README.md

## **Machine name: Bounty Hunter**

### **1. Running nmap**
![f1383eee7a5ed15c11b1d1fc3187be7d.png](./_resources/0db99a6046fb4c599f4b872a2f81c630.png)
After running nmap, we were able to find 3 open port on the server: 21(ftp), 22(ssh) and 80(http). We were also able to find that ftp allows anonymous login.
### **2. Service enumeration**
#### **1. FTP**
We logged in using user anonymous to ftp and were able to find 2 files: locks.txt and task.txt. On checking the files after downloading them, we find that locks.txt had a list of words which could be password and we were also able to find the user who wrote tasks.txt
![7e76fdf1c414333037b5ee5017c788d2.png](./_resources/5d0707b628f1449aae23aa9924c455b2.png)
#### **2. ncrack**
We use the writer of task.txt and the list in locks.txt and use ncrack. We were able to get the password for the user.
![c00fd168e5193055c8ed68db38a7ee67.png](./_resources/55d41204d2a0485a84be4816893696b8.png)
### **3. Exploit**
As we have the password from ncrack, we can login to ssh:                                                
![212a7c40fee63db6be8059a714792d71.png](./_resources/374dbc5174ca401caf77ffae18a86cfd.png)
We were able to find the user.txt at /home/lin/Desktop
#### **1. Checking sudo permission**
On checking sudo permission granted to user, we see that the user can run tar using sudo. 
![1459c8034ed6b7e5f1664c74fb460225.png](../_resources/df50b53ae02648269785ee79cd8799da.png)
#### **2. Post exploit**
We use the [tar sudo exploit](https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/) here to set the sticky bit to bash.
![4f7409c0daf1fa472d20409a247c1496.png](./_resources/13800da2b97548f59c3aebc09b2c95b5.png)
#### **3. Final Flag**
We can then get the final flag at /root                                                       
![559ac63787291e9f6364ae2598ecba7d.png](./_resources/bf39c89e68b44279b5d9b0b9e7970d94.png)

