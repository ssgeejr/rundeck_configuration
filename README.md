#### Reminder: user the develop branch for the latest updates, comments, notes and changes ####

Rundeck Homepage: http://rundeck.org/index.html

Install: http://rundeck.org/downloads.html

I used the deb file and noticed a few items that could be improved upon ... 

1) set RDECK_BASE in /etc/profile *or your prefered location*
```
sudo echo "RDECK_BASE=/var/lib/rundeck" >> /etc/profile
sudo echo "export RDECK_BASE"
```

2) Load the changes into your environment
`. /etc/profile`

3) Configure the server to use the correct hostname:
```
Update the settings in the following two files:
/etc/rundeck/framework.properties
-framework.server.name = localhost
+framework.server.name = yourserver.domain.com
-framework.server.hostname = localhost
+framework.server.hostname = yourserver.domain.com
-framework.server.hostname = localhost
+framework.server.hostname = yourserver.domain.com

/etc/rundeck/rundeck-config.properties
-grails.serverURL=http://localhost:4440
+grails.serverURL=http://yourserver.domain.com:4440
```

4) Install the Ansible-Plugin
```
Plugin Github Project: https://github.com/Batix/rundeck-ansible-plugin/
Plugin Github Releases: : https://github.com/Batix/rundeck-ansible-plugin/releases
[At the time of this writing, 1.2.1 is the latest stable build]

wget -P $RDECK_BASE/libext https://github.com/Batix/rundeck-ansible-plugin/releases/download/1.2.1/ansible-plugin-1.2.1.jar
```

5) Start-up the server
```
/etc/init.d/rundeck restart
or (restart didn't work for me ... )
/etc/init.d/rundeck stop
/etc/init.d/rundeck start
```
6) Log in to the server
```
Rundeck URL: http://yourserver.domain.com:4440
username: admin
password: admin
```

**Ansible Install**

Install Ansible
On Debian-8:  apt-get install ansible -y  
you should now have the following directory structure:
```
/etc/ansible
├── ansible.cfg
└── hosts
```




... that's all I have for the moment ... 

Testing

Test Job: RemoteFileCopy

... more documentation to follow ...
```
Remote copy results [success]
rundeck@otherserver:~$ ls -lta /tmp
total 32
-rw-r--r--  1 rundeck rundeck 1355 Apr 13 10:03 copyme
```


all the locations for the directory 'rundeck'
```
root@buildpoc01:/etc/init.d# find / -type d -name rundeck -print
/var/log/rundeck
/var/lib/rundeck
/var/lib/rundeck/exp/webapp/WEB-INF/rundeck
/var/lib/rundeck/exp/webapp/WEB-INF/classes/org/rundeck
/var/lib/rundeck/exp/webapp/WEB-INF/classes/com/dtolabs/rundeck
/var/lib/rundeck/exp/webapp/WEB-INF/classes/rundeck
/var/rundeck
/etc/rundeck
/usr/share/doc/rundeck
/tmp/rundeck
```






