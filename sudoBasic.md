- Create a new sudoers file in the ```/etc/sudoers.d``` directory that will contain a standalone entry for webmasters: (```-f``` is flag to create a new file)
```sudo visudo -f /etc/sudoers.d/web_admin```
#### If you want to create file in root file and don't have access, use ```sudo visudo <filename>```

- Press ```i```

- Now enter in the following at the top of the file:
```Cmnd_Alias  WEB = /bin/systemctl restart httpd.service, /bin/systemctl reload httpd.service```

- Add another line in the file for ```rakasd``` to be able to use the ```sudo``` command in conjunction with any commands listed in the ```WEB``` alias:
```rakasd ALL=WEB```

- To save type Esc and now to close the file type ```:wq!```.

- To double check that file has been created: ```sudo visudo```

- Next, log in to the rakasd account:
```sudo su - rakasd```

- Attempt to restart the web service:
```sudo systemctl restart httpd.service```
#### If rakasd account asks for password and password is correct, rakasd has access to restart the web service with the sudo command

- Try to read the new ```web_admin sudoers``` file:
```sudo cat /etc/sudoers.d/web_admin```

- Since the ```cat``` command is not listed in the command alias group for ```WEB, rakasd``` cannot use ```sudo``` to read this file.

#### Issue: ```/etc/sudoers.d/web_admin busy, try again later```
              - Reference to this weblink: https://www.2daygeek.com/check-find-parent-process-id-pid-ppid-linux/




- Log in to one of the servers (which will then be referred to as server1 throughout the rest of the lab guide) using the credentials provided:
```ssh dev@<server1_PUBLIC_IP>```
The password for dev is the same as the one for cloud_user.

### Enable SSH to Connect Without a Password from the dev User on server1 to the dev User on server2
- Generate an SSH key:
```[dev@server1]$ ssh-keygen```
- Press Enter three times to accept the defaults.
- Then copy it over to the private IP of the other server:
```[dev@server1]$ ssh-copy-id <server2_PRIVATE_IP>```
- Now if we try to log into server2 without a password, it should work. Try it:
```[dev@server1]$ ssh <server2_PRIVATE_IP>```
- Log out to get back to server1:
```[dev@server2]$ logout```

### Copy All tar Files from /home/dev/ on server1 to /home/dev/ on server2
- Copy the files:
```[dev@server1]$ scp *.gz <server2_PRIVATE_IP>:~/```
- Connect to server2 again:
```[dev@server1]$ ssh <server2_PRIVATE_IP>```
- Make sure they're there:
```[dev@server2]$ ll```
It should show the two files.

### Extract the Files, Making Sure the Output is Redirected
- Extract the files:
```[dev@server2]$ tar -xvf deploy_content.tar.gz >> tar-output.log```
```[dev@server2]$ tar -xvf deploy_script.tar.gz >> tar-output.log```

- Take a look at what's in the directory now:
```ll```
We'll see the new files and their permissions.

### Set the Umask So New Files Are Only Readable and Writeable by the Owner
- We need to make new files with 0600 (-rw-------) permissions. Since the default is 0666, and we want it to be 0600, run the following:
```[dev@server2]$ umask 0066```

### Verify the /home/dev/deploy.sh Script Is Executable and Run It
- Check permissions on deploy.sh:
```[dev@server2]$ ls -l deploy.sh```
- Make the script executable:
```[dev@server2]$ chmod +x deploy.sh```
- Run it:
```[dev@server2]$ ./deploy.sh```
