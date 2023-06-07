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
