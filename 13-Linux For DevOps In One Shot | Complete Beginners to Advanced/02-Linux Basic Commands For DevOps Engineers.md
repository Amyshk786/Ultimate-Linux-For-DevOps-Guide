
# Linux Basic Commands for DevOps Engineer

1) ls -> List Everything in a Directory


2) cd -> Change Directory


3) pwd -> Prints the Present Working Directory


4) mkdir, ->  Make Directory


5) Delete Directory files rm,rmdir -> rm for removing a file,  rmdir to delete a empty dir,  rm-r to delete a dir recursively


6) cat, zcat -> To view File content,  zcat is used to view file content of a zipped file


7) touch -> To create a File


8) Head -> To view first lines of a File [head -n 5 file.txt] first 5 lines show krega


9) Tail, tail -f -> To view last lines of a File,  [tail -n 5 file.txt] last 5 lines show krega,      tail-f is Used to View Logs file by DevOps Engiveers


10) less, more -> Used to view Files but "less" is more useful


11) cp  -> Used to copy a file,   cp -r used to copy a dir recursively


12) mv -> Used to Move & Rename Files and Dir


13) wc -> Used to show Word Count  [We can use "wc" for Multiple File word count]  ["wc" CMD batati h lines kitni h, words kitne h & file kitne bytes ki h]


14)  vi editor in Unix and Linux operating system?


15 ) ln (hard link, soft link) -> ln -s is Used to Create a Softlink, If the Original file is deleted Softlink will also get deleted, it will be of blue color

ln is used to create a Hardlink, If the Original file is deleted Hardlink will not be deleted



# Softlink Example - ln -s /home/ubuntu/devops/cloud/newfile.txt soft-link


-> If we do ls soft-link file bun gyi h [Agar Main File delete ho gyi toh softlink Red ho jati h and Delete ho jati h]

ubuntu@ip-172-31-1-139:~$ ls
Shell-Scripting-For-DevOps  day03             error_handle.sh        loop.sh                 shell-scripting-projects  wloop.sh
TWS                         demo              file                   loyalty.sh              soft-link
billi.sh                    demo_file.txt     firsh-shell-script.sh  myfirstfolder           test.sh
billu.sh                    deploy_django.sh  jethalal-ki-duniya.sh  nodeHealth.sh           ty.sh
check-if-jetha-loyal.sh     devops            list-user.sh           second-shell-script.sh  user-add.sh
ubuntu@ip-172-31-1-139:~$





# Hardlink Example - ln /home/ubuntu/devops/cloud/newfile.txt hard-link


# If we do ls hard-link file bun gyi h [Agar Main File delete ho gyi toh hard-link Delete Nhi Hogi]



ubuntu@ip-172-31-1-139:~$ ls
Shell-Scripting-For-DevOps  day03             error_handle.sh        loop.sh                 shell-scripting-projects  wloop.sh
TWS                         demo              firsh-shell-script.sh  loyalty.sh              soft-link
billi.sh                    demo_file.txt     hard-link              myfirstfolder           test.sh
billu.sh                    deploy_django.sh  jethalal-ki-duniya.sh  nodeHealth.sh           ty.sh
check-if-jetha-loyal.sh     devops            list-user.sh           second-shell-script.sh  user-add.sh







16) cut -> cut -b 1-4 demo_file  [It will cut the 1st to 4 byte from the file and provide the Output]


17) tee -> If we do echo "Hello" | tee file.txt  [tee will print the "Hello" on the screen As well as file.txt bhi create krega & usme bhi Dal dega]

[tee is a Command which is used to take Input or Output and Display the Output on the Screen as well as on the File]


18) sort -> It will sort the File Content Alphabetically


19) clear -> To Clear the Screen


20) diff -> It will provide us the difference between 2 files [diff file1 file2]


21) ssh -> We can use this CMD to Connect to Any Machine at Port 22


22) df -> Shows the Amount of Disk Space Used and Available on the Filesystem [We can use df -h to Display the Content in Human Readable format]


23) du -> Shows us the Disk Space Usage of Files and Directories


24) ps -> It is used to Display Info Abt Running processes [PID, Users, CPU Usage, Memory Usage & More]


25) top -> It will Show Us All the Processes Which are Running, Stopped, Killed, Zoombie


26) fuser -> It is Used to Identify which processes are using a particular file, dir or socket


27) kill -> To Kill any Process


28) nohup -> It is used to Store the Logs into a File like ["nohup free -h"  free -h ka output nohup.out Folder me store krega and badme jab bhi koi dusri CMD fire krege like "nohup df -h" toh uska bhi output niche show krega,  Logs store krne DevOps Eng use krte h]


29) free -> It is Used to Display Memory Usage [WE can use free -h to display the Output in Human Readable format]


30)vmstat -> It is Used to Report Info Abt System processes, Memory, CPU Activity, Block I/O. [It Provides Insights into the Overall Performance of the System Helping Users to Monitor Resources and Identify Bottlenecks]


vmstat -a krege toh Active In-Active batata hai


# vmstat -a 


ubuntu@ip-172-31-1-139:~$ vmstat -a
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 103632 521928 128340    0    0     6     5   19   31  0  0 100  0  0
