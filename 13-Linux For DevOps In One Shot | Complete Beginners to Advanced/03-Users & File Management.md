#Day 3 - Users and Files Management
===================================



#System-Level Commands -
========================


1. uname  -> It will show which Platform we are using in our case as we are using Ubuntu it will show Linux [In Mac it shows Darwin]



2. uptime  -> It will show the Time period our Machine is Operational or We are using it, How Many users are Active and Is there any Load on the Machine



3. Date  -> It will Display the Current Date and Time in UTC 



4. who,whoami  -> "who" will show us which User has logged in and when he has logged in & How Many users are logged-in in this system

"whoami" Will show us the Current Logged-In Users Username 



5. which  -> It allows users to search the list of paths in the $PATH environment variable and outputs the full path of the command specified as an argument like if we want to check which version of Java, Python, Docker, Jenkins, Terraform and any other apps that are Installed.



6.  id  -> It is used to display user and group information, including user IDs (UID), group IDs (GID), and the groups a user belongs to. It can show information for the currently logged-in user or for a specified user. 



7.  sudo  -> The "sudo" command in Linux allows users to run commands with the security privileges of another user, typically the superuser (root). Sudo is a Group which has the All the Permissions to do Everything in Linux.



8. shutdown  -> For shutdown we will have to use "sudo" without that system will not be able to shutdown. [The Public IP Address will get changed when we shutdown as it is "Dynamically Assigned"]



9. reboot  -> For reboot we will have to use "sudo" without that system will not be able to reboot.



10. apt (Advanced Package Tool) -> apt is a commandline package manager and provides commands for searching and managing as well as querying information about packages. It provides the same functionality as the specialized APT tools, like apt-get and apt-cache.



11. yum (Yellowdog Updater, Modified) -> A command-line package management tool primarily used in RPM-based Linux distributions like CentOS, Fedora, and Red Hat Enterprise Linux



12. dnf (Dandified YUM) -> The successor to yum, offering improved performance and dependency resolution. It is the default package manager for Fedora and is also used in other Red Hat-based systems. 



13. pacman  -> Used in Arch Linux and its derivatives. It's known for its speed, simplicity, and direct control over package management. It offers robust dependency resolution. 



14. portage  -> Used in Gentoo Linux, ChromeOS. It's a source-based package manager, meaning it compiles software from source code on your machine. It provides a high degree of customization and flexibility but requires more resources and time. 



15. rpm -> RPM (Red Hat Package Manager) is a low-level package manager, while YUM (Yellowdog Updater, Modified) is a higher-level package manager that uses RPM. RPM handles individual packages and their files, but YUM simplifies package management by handling dependencies and allowing for bulk operations and automatic updates from repositories. 








----------------------------------------------------------------






#User & Group Management Commands - 
====================================


1. sudo  -> The "sudo" command in Linux allows users to run commands with the security privileges of another user, typically the superuser (root). Sudo is a Group which has the All the Permissions to do Everything in Linux.



2. useradd  -> create a new user or update default new user [A new user with name mike will be created with a home directory]

# "sudo useradd -m mike"



3. whoami  -> "whoami" Will show us the Current Logged-In Users Username 



4. Su  -> This is used to Switch from One User to Another [After using the below command you will have to provide the passwd for mike user]

# su mike  [To check if the user has been Switched u can use the command "whoami"]



5. passwd  -> This is used to create a Password for a User [After using the below command you will have to provide the passwd for mike user]

# "sudo passwd mike" 



6. userdel  -> This is used to Delete a Specific User

# "sudo userdel mike"



7. groupadd  -> This is used to create a Group

# "sudo groupadd devops"  [To check the groups use below command]

# cat /etc/group



8. gpasswd -a , -M  -> This is Used to Add Users to Group 

# "sudo gpasswd -a mike devops"    [Use this if you want to add Single User]

# cat /etc/group  [To check if the user is added to the group or not]


# sudo gpasswd -M carl,monty,micheal tester   [Use this if you want to add Multiple User]

# cat /etc/group  [To check if the users is added to the group or not]



9. groupdel  -> This is Used to Delete a Group

# "sudo groupdel tester"





----------------------------------------------------------------





#File Permission Commands - 
============================


1. Umask  -> 



2. ls -l  -> This is Used to List Directory Content "-l" Use a Long List Format



3. chmod  -> The "chmod" command in Linux is used to change the access permissions of files and directories. It allows you to control who can read, write, or execute a file or directory. chmod is short for "change mode". 



4. chown command  -> This is Used to Change Owner of a File or Directory

# "sudo chown mike demofile.txt"  [By using this command mike will become owner of the demofile.txt]



# Example - [If we do "ls -l" It will show us that demo_file.txt is Owned by Mike]

ubuntu@ip-172-31-1-139:~$ ls -l
total 108
drwxrwxr-x 7 ubuntu ubuntu 4096 Jul 12 10:43 Shell-Scripting-For-DevOps
drwxrwxr-x 3 ubuntu ubuntu 4096 Jul 10 11:43 TWS
-rwxr--r-- 1 ubuntu ubuntu   65 Jul 11 19:17 billi.sh
-rwxr--r-- 1 ubuntu ubuntu   67 Jul 11 19:13 billu.sh
-rwxr--r-- 1 ubuntu ubuntu  260 Jul 11 16:24 check-if-jetha-loyal.sh
drwxrwxr-x 4 ubuntu ubuntu 4096 Jul 12 11:30 day03
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 12 10:29 demo
-rw-rw-r-- 1 mike   devops 3614 Jul 17 12:02 demo_file.txt




5. chgrp command  -> This is Used to Change Group of a File or Directory

# sudo chgrp devops demofile.txt   [By using this command demofile.txt will be owned by devops group]




# Example - [If we do "ls -l" It will show us that demo_file.txt is in devops group]

ubuntu@ip-172-31-1-139:~$ ls -l
total 108
drwxrwxr-x 7 ubuntu ubuntu 4096 Jul 12 10:43 Shell-Scripting-For-DevOps
drwxrwxr-x 3 ubuntu ubuntu 4096 Jul 10 11:43 TWS
-rwxr--r-- 1 ubuntu ubuntu   65 Jul 11 19:17 billi.sh
-rwxr--r-- 1 ubuntu ubuntu   67 Jul 11 19:13 billu.sh
-rwxr--r-- 1 ubuntu ubuntu  260 Jul 11 16:24 check-if-jetha-loyal.sh
drwxrwxr-x 4 ubuntu ubuntu 4096 Jul 12 11:30 day03
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 12 10:29 demo
-rw-rw-r-- 1 mike   devops 3614 Jul 17 12:02 demo_file.txt





----------------------------------------------------------------



#Compression Command - 
========================


1. Zip, gunzip, and gzip commands  -> The zip command in Linux is used to create compressed archives in the .zip format. It combines multiple files and directories into a single archive file, reducing file sizes and simplifying storage and transfer. 

[gunzip and gzip are tools which we cna use to compress/zip and unzip files and folders]

# zip -r kgf.zip linux_for_devops



# Example - 

ubuntu@ip-172-31-1-139:~$ zip -r kgf.zip linux_for_devops/
  adding: linux_for_devops/ (stored 0%)
  adding: linux_for_devops/dummy_file.txt (stored 0%)
  adding: linux_for_devops/demo_file.txt (deflated 81%)
  
  
  


------------------------

# UNZIP Example - 

# mkdir coco               [New folder banaye humne coco naam se]

# cp kgf.zip coco         [kgf.zip file ko humne coco folder me copy kiye]

# cd coco                 [Hum coco folder me gye and file ko unzip kiye]

# unzip kgf.zip 



# Example - [If we run "unzip kgf.zip" command humari file unzip ho jayegi niche proof h]


ubuntu@ip-172-31-1-139:~/coco$ unzip kgf.zip
Archive:  kgf.zip
   creating: linux_for_devops/
 extracting: linux_for_devops/dummy_file.txt
  inflating: linux_for_devops/demo_file.txt
  
  

# ls [If we do "ls" kgf.zip jo file h wo unzip ho gyi h]


ubuntu@ip-172-31-1-139:~/coco$ ls
kgf.zip  linux_for_devops




2. tar, untar command  -> Tar is a Utility to Compress a file 


# tar -cvzf cloud.tar.gz cloud     [Ye command se cloud naam ki jo Directory h wo "cloud.tar.gz" name ki ek Compressed file bun jayegi]


# tar -xvzf cloud.tar.gz     [Ye command se cloud naam ki jo Directory h wo "cloud.tar.gz" name ki ek Compressed file bun jayegi]


-c = Creates an archive by bundling files and directories together.


-v =Displays verbose information, providing detailed output during the archiving or extraction process.


-z = Uses gzip compression when creating a tar file, resulting in a compressed archive with the '.tar.gz' extension.


-f = Specifies the filename of the archive to be created or extracted.


-x = Extracts files and directories from an existing archive.




----------------------------------------------------------------



#File Transfer Command - 
==========================


1. SCP command (copy files)  -> The scp command in Linux is used for securely copying files and directories between a local and remote system, or between two remote systems, using the SSH protocol. It's a command-line utility that enables secure and encrypted file transfers over a network. 


# Example 1 - 
[Here we have Copied test.sh file from our Local Machine to VM by using the below Command]

# scp -i Downloads/nv.cer test.sh ubuntu@3.109.124.17:/home/ubuntu




# Example 2 -

[Yaha humne Humare VM se linux_for_devops k Directory ko humare Local Machine pe Copy kiye]

# scp -i Downloads/nv.cer -r ubuntu@3.109.124.17:/home/ubuntu/linux_for_devops .

dummy_file.txt                                                                                                 100%   21     1.4KB/s   00:00
demo_file.txt






2. rsync command  -> Rsync is a versatile command-line utility in Linux used for synchronizing and transferring files and directories, both locally and remotely. It's known for its efficiency, particularly in transferring only the changed portions of files using a delta-transfer algorithm. This makes it a powerful tool for backups, mirroring, and general file management. 




