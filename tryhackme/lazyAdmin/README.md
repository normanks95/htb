README.md

## **Machine name: Lazy Admin**

### **1. Running nmap**
![86018fdeccf26e828f3eb8df5a9cfc81.png](./_resources/5561e5685d6247ef8c7f96a7ae95e76a.png)
After running nmap, we were able to find 2 open port on the server: 22(ssh) and 80(http).
### **2. Service enumeration**
#### **1. HTTP**
	1. We ran dirb and found the below directories
![cd769a13f21dfc9b7604812b316ac25f.png](./_resources/9627eedacec84d4d832d93a6b172cb2f.png)


	2. On checking */content/inc*, we could find a mysql backup at */content/inc/mysql_backup/*
![ddb37fec92a9b48e8ac48f128f36f654.png](./_resources/d8fef30e241543e688a855b7aac40171.png)


	3. We were able to find the username and the password in the sql files
![f1fb2422c1225be22ee712f66bb28adf.png](./_resources/445b957105ed43b8aa29f1421750e59f.png)
	
	
	4. We were then able to login to the console at */content/as*
![7615e3ad83bdd7000f1bc74843f7c4cf.png](./_resources/6e72e8913a76493b8aa282e52b655527.png)
### **3. Foothold**
1. After gaining access to the dashboard we can uplload a reverse php script from the media center tab. We were not able to upload a php file, however, we were able to zip it and upload it after checking the extract zip option.


![cea4df2a0c901668879258796d0092dd.png](./_resources/b559b4cdd9174fbdb4c4ce06f667c0e3.png)
2. We can then start a reverse shell and access the reverse shell script from */content/attachment/*


![827e1e01d6f55a4efbdc49c33bc7becd.png](./_resources/6dc247b4f96e4f19a2a6f6fe6b2cd4a9.png)
### **4. First flag**
Once we have access to the reverse shell, we can get access to the first flag at 


![084dfcf61c334c2690bee123e086b20c.png](./_resources/48932f0a727a4dac8a01d5f2638cb98f.png)

### **5. Sudo permission**
When checking the sudo permission, we were able to find that the user can run a perl script using sudo privileges.


![2207d27a5451f7fb7d6ee17c483f5be6.png](./_resources/af70f1bfe52f45a6a73a6dcb627d5630.png)
### **5. Exploit**
The user only has read right to the script

![d3d57f2062c41cbc4eb8b66160d652b7.png](./_resources/d46b27a7dbbf4fb7bd65fa02712e6e41.png) 

However, the user has write permission to shell script is executes. We therefore set a sticky bit on bash: 

![fe6584ca932d8a7a21b1d901f711f3df.png](./_resources/86a748810ee543ffb99bb2336a3740a2.png)
We then run the script using sudo to get root access


![8dc158e97afe307ecb2b1860b5c8ceff.png](./_resources/c3bfb9a6772a4b819097cedd8f54d086.png)
#### **3. Final Flag**
We can then get the final flag at */root* 


![559ac63787291e9f6364ae2598ecba7d.png](./_resources/bf39c89e68b44279b5d9b0b9e7970d94.png)
