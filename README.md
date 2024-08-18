# linux

This is a testing page
Testing...............................................................................................................................................................................

Administrator is the default user for Windows which is like QSECOFR in as400 similarly root is QSECOFR for Linux.

Administrator and root are the highest level privileged users.

Linux on EC2


Minimum requirements when creating an ec2 instance are similar 2to us buying a laptop

1. Purpose - for example gaming, office. chrome book, mid-range gaming, etc.
2. CPU - for example i9, amd, intel other gens
3. Memory - how much
4. Disk - type SSD or HDD similarly.

Whenever we get a request to create an EC2.
we have to ask the purpose - why they need the instance for (business purpose).
 how much RAM they require. type of OS, what is the CPU and memory they require. what type of disk type they are looking for and also the cost that it will incur to provision that VM. how long it should be provisioned.

The experience of a person also comes from the naming convention of the VMs.
The name of the VM(1) is the first and foremost thing that will be visible to us in the dashboard. so by just seeing the VM name we should know the purpose and version in it.
Common format is ({environment type(dev, test, prod}:{specific application running in it}:{type and version of the OS running.})
Example: dev_SQL_windows2012

AMI(2): we have to select the AMI (Amazon machine image) - so if we were to install/upgrade a new OS in the server it is going to take at least 4 - 5 hours as per the abacus. but how it is possible to span a new VM with our own choice within a few minutes in cloud. this is the result of AMI.
AMI is basically a disk with the OS of our choice and it is attached to the server. so instead of installing it freshly which takes time. we are directly attaching the boot disk [boot disk is a disk in which OS resides or the server reads the data when booting/starting] to VM. so we are just starting the VM with our choice of OS like starting a PC. 
Including the OS we have to select the no of CPU cores and RAM
after that, we have to select a key pair we can generate a key pair then and there.
We can even import the public key and select it. After which we need to select the memory and the type - SSD and HDD.

so .pem keys are for SSH method and .ppk is for a putty method to connect to a server. where always we load the public key to the server and private key is secured with us.

The default user of the Linux on AWS is ec2-user or root

Billing in AWS:
Cost varying depending upon the services we use and the location they are created/spawned. we can use the Amazon cost calculator to calculate the price
reserved instances will save more money than on-demand instances but we should be ready for commitment as the fee would be paid upfront for the years that we reserve them. Normally On-demand Ec2 instances are used for POC the testing/developing requires less period (Couple of months). But for the production, we know that production should be up and running for a long time. so, in this scenario, it is recommended to use the reserved instances where the 60% bill can be saved compared to the on-demand instances. (example: subscription similar to our SAAS order forms).

Types of instances:
on-demand instances - costly
Reserved - 60% discount when compared to on-demand.
On-spot - 90% discount when compared to on-demand.

Companies mainly go by compute saving plans but not reserved capacities.

AWS can terminate spot instances at any time with or without notice.
we cannot run the spot instances for more than 24 hours.

spot instances can also be used in production using 60-40% and 70-30% (on-demand  + spot). where 60/70% are reserved and 30-40 can be spot instances.

till 2022, there are no options to stop and start a spot instance. but from 2022, we get the option to start/stop the instances. (experience question)

Scope of the EBS (elastic block store is zone) -> Means even if the VM and the block storage is in the same region they wont be compatible if they are not in the same zone.
EBS is only the installable storage in AWS. (the storage can be attached to one VM at a time) but the VM can have multiple block storages attached to it but not vice versa.

whenever we restart an EC2 instance its public IP will change.
We can increase the disk but not shrink it.

Elastic IP address: whenever we stop and start an VM the Public IP of the VM changes so the public IP is not reliable as it would change for every restart. so the concept of elastic IP which is a static IP comes in picture. but this costs us money(expensive) . As of March 28th Public IP is not free anymore (FYI).

By assigning the elastic IP to a VM the public IP of the VM will be the elastic IP no matter how many times we restart.

Linux


Linux connectivity -> when SSH to a Linux server from putty using the username and password for authentication - we have to select the username@systemip(public)
SSH username@publicIP.

Everything in Linux is a File
Linux is case-sensitive including the user profile and file names
The system settings/properties of Linux are modified by the values in a file.
Linux doesn't have the concept of file extension which is one of the reasons it is so secure. even if we give the extension license will consider it as a name.

----> in Windows the file opens the application based on an extension but in Linux application opens the file due to which there will be fewer cybersecurity threats due to human errors.

Least privilege principle.
Root in Linux is the highest privileged user profile in Linux but there's a catch in most of the Linux versions an individual cannot log in as root user. this profile is disabled by default and there is no password. even if we set the password. we may not log in. but there's a workaround to execute commands as a root user that is by using the Sudo (super user do) where temporarily the privileges and access are granted to the user profile to execute commands on specific paths or files that they are restricted for security reasons.

Syntax: Sudo [commands]

the default directory of a user will be /home/<username> -> where all the user created objects by default will be created in /home/<username>/<objects/files>

SED (stream line editor): using this we can see the from a specific line to another specific line. example: sed -n -e ' "starting line number" , "ending line numer" p(print)' filename
example: sed -n -e '8,15 p' /etc/passwd will provide the 8 to 15 lines of the file. we can print a specific line using sed -n -e '8 p' /etc/passwd (only 8th line will be printed)

CUT (filed seperator): using the field seperator we can get some specific data.
Example: [ centos@centos8-machine /etc ]$ cut -d : -f1 /etc/passwd -> here we used the : as the divider/separator to divide the string into fields and later we have selected the fields to print.
root
bin
daemon
adm
lp
so cut -d : -f1-5 /etc/passwd -> will show from 1filed to 5th field 
but cut -d : -f1,2,5 /etc/passwd will show only the 1st,2nd,5th field. we can play like cut -d : -f1-5,7 /etc/passwd [(-) -> from and to] [(,) specific fields] 

VI / VIM - editor in linux -> used to edit/write into file: 
to enter the data in a file using the VIM/VI first esc and then press insert key. after all the data is entered to save the contents and exit the editor esc :wq!(save and quit)
if you dont want to make the changes q!(quit)

Tar and Zip: used for compressing and archiving files also we could say packing the files into a single container.

How to compress/archive a file using a Tar/zip:
Tar: tar -zcvf zips.tar.gz zips: (this is like SAVF incomparsion)  TAR full form is tape archive
1. tar: The command-line utility for archiving files.
2. -z: Compress the archive using gzip alogathim (.gz).
3. -c: Create a new archive.
4. -v: Verbose mode, which displays the files being archived.
5. -f zips.tar.gz: Specifies the filename of the archive (zips.tar.gz in this case).
6. zips: The name of the directory or file that you want to include in the archive. (can be multiple inputs (type can be files directories etc)

Zip: ZIP filename.zip extension files/ directories/ -> used to archive/compress a file

How to uncompress/unarchive a file using a Tar/zip
Tar: tar -xf apache-tomcat-10.1.26.tar.gz
1. tar: The command-line utility for archiving files.
2. -x: Extracts files from an archive.
3. -f apache-tomcat-10.1.26.tar.gz: Specifies the file (apache-tomcat-10.1.26.tar.gz) that you want to extract.

Zip: unzip (zip filename)

How to see the contents of a Zip file without extracting them similar to DSPSAVF
TAR: tar -tf zips.tar.gz (-t(table of contents) = list the contents of the tar file)
Zip: unzip -l zipfilename (-l = list the contents)

The operating system is stored on the hard disk, but to speed up the whole process, the OS is copied into RAM on start-up.

Runlevels in linux: are like windoes boot options

1. 0: Halt (shuts down the system)
2. 1: Single-user mode (for administrative tasks, minimal services)
3. 2: Multi-user mode without networking
4. 3: Multi-user mode with networking (standard for server operations 90% of the server will be in this mode)
5. 4: Undefined (user-definable)
6. 5: Multi-user mode with networking and graphical user interface (GUI)
7. 6: Reboot (restarts the system)

others ways to shutdown and restart:

sudo halt |  sudo shutdown -h now | sudo reboot | sudo shutdown -r now | sudo init 6 (reboot) | sudo init 0 (shutdown).

Process Management:
PS - this shows the processes
Top - this shows the dynamic accurate data of all the process CPU, Mem consumption and everything. (shift + p sort the CPU (highest to lowest)
shift + M (memory consumption (highest to lowest) , (shift + u and type the user to get the stats of that specific user.)

User management:
how to see the users present in the system: by going to /etc/passwd this contains all the user profiles present in the system and there is a parameter known as UID normally 0 is root and there are other inbuild created user profiles/accounts.
all the others that are create afterwards will have a uid(userid) >= 1000.

how to create a new user: 
useradd username but we have to use Sudo to create a user as it require privileges. 
using useradd we just create the user profile but not set the password for it to access. so sudo passwd username + enter whenever we need to do a task that require administrator privileges we need to use sudo. (by default when a user is created a group is created with user name along with group id). | how to delete a user: sudo userdel username

how to switch to a user in the middle of the session: su - username/ su username
to grant the user sudo access. we have to add the user in the /etc/sudoers file as <username ALL=(ALL) ALL > you will know where you need to add. but we cant add every single user in this file as a single thing changed in this file will mess up the system. so the concept of group comes in.

how to create a new group: sudo groupadd groupname |  how to delete a group: sudo groupdel groupname

How to add a user profile to the group: sudo usermod -a -G groupname | [another way sudo gpasswd -a username groupname] username (we can add 1 user at a time) a user can have 1 primary + 15 secondary (supplementary) groups.
```
sudo usermod -a -G groupname username
```
- -a: Append the user to the group (without removing them from other groups).
- -G: Specify the group(s) to which the user should be added.
- groupname: The group you want to add the user to.
- username: The user you want to add to the group. | how to remove a user from a group: if i remove -a and and proceed with this sudo usermod -G groupname username then the user will only be added to the this group and will be removed from other groups or simply use sudo gpasswd -d gperumalla(username) infortech(groupname) (-d=delete the user)

sudo usermod -a -G gperumalla,infortech qsecofr -> we can add a user to multiple group all at once. but there is no command to add a multiple users into a single group all at once. (but we can modify the /etc/group to acheive this)
how to see which users are part of a group -> we can see this in /etc/group 
how to see the paramters of a user: id <username> 

Permission management: 

[-rw-r--r--(permission)] 1(hard-link) root(user) root(group) 1655(size of the file) Jul 26 20:22(last modified) passwd

rwx(4+2+1 = 7) operations on a file
r read: 4
w write: 2
x execute: 1
chgmod is the command to change the permission on a file.
-(file)rwxr-xr-- -> first 3 decides what the owner can do | next 3 decides what a group can do | next 3 decides what nor owner nor group can do. (rwx - owner can read write execute | r-x - group can read and execute | r-- others can only read.)

File Permissions:
	- Read (r): Allows viewing the content of the file.
	- Write (w): Allows modifying the content of the file.
	- Execute (x): Allows executing the file if it is a script or binary.

d(directory)rwxr-xr-- -> first 3 decides what the owner can do | next 3 decides what a group can do | next 3 decides what nor owner nor group can do. (rwx - owner can read write execute | r-x - group can read and execute | r-- others can only read.) but the directory permission will not be copied to the files in the directories.

Directory Permissions:
	- Read (r): Allows listing the contents of the directory.
	- Write (w): Allows creating, deleting, and renaming files in the directory.
	- Execute (x): Allows entering the directory and accessing files within it.

so we can do a recursive chmod -r <permission numbers> directory -> this will edit all the files permissions similar to the directory,
we can use ACLs (access control list for more granule access)
ports - 65535 is max number of the ports where first 1034 are reserved for preserved services like SSH, MAIL , FTP etc.

```
sudo netstat -tupln

```
- -t: Shows TCP connections.
- -u: Shows UDP connections.
- -p: Shows the process ID (PID) and name of the program to which each socket belongs.
- -l: Shows only listening sockets. This is useful for viewing which ports are open and waiting for incoming connections.
- -n: Shows numerical addresses instead of resolving hostnames. This makes the output faster and avoids DNS lookups.

Sample Output and Explanation

Here’s a sample output of the command:
```
bash
Copy code
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1234/sshd
tcp6       0      0 :::80                   :::*                    LISTEN      5678/httpd
udp        0      0 0.0.0.0:68              0.0.0.0:*                           9101/dhclient

```
- Proto: Protocol (TCP or UDP).
- Recv-Q: Number of bytes not copied by the user program connected to this socket.
- Send-Q: Number of bytes not acknowledged by the remote host.
- Local Address: The local IP address and port number on which the process is listening.
- Foreign Address: The remote IP address and port number (for connections). For listening sockets, this is typically shown as * or :::*.
- State: The state of the socket (e.g., LISTEN).
- PID/Program name: The process ID and name of the program that is using the socket.

networking firewall/security group in AWS: A security group controls the traffic that is allowed to reach and leave the resources that it is associated with.
there are 2 type of errors in network to determine what caused the issue
1. Timed out: this is firewall related (the firewall didnt allow the request to go to requested server)
2. connection refused error: this is probably due to the service/app denying the request (not firewall issue)
by remembering the above -> it is easy to troubleshoot the network related issues.

How to allow user only to execute some commands as a root user.
We can achieve this by editing the /etc/sudoers. so we place the user we want/group we want in the same thing without a password section and update the feild with NOPASSWD: (path to the command) [to find the path to the execute command use command type {command name}]


Pack manager:
dnf - upgraded version of yum so in-order to install update remove we use dnf as yum is for older version.

sudo is required to run dnf if not login as root user using sudo su - as workaround for not using sudo.

dnf list installed
dnf list avaible
dnf list - shows available and installed applications/packages.
dnf install 
dnf remove
dnf update

so when we use install, update how the system knows where to check the versions, pre-reqs and other things etc. this concept is called repos(repositries)
so /etc/yum.repos.d is the directory where all the repos are present. when we tell system to install/update it will check these repos for details/packages and install them.
but not repos are configured by default in the system for example jenkins. we have to manually do it by following the instructions in the home page of the jenkins

so search google <application-name> repo it will take us to official page where there are commands to configure the repo.

who - will show all the users who are logged into the system.

dnf history - shows the history what dnf commands are used for what purpose(install, update, remove etc) to what service/application irespective of the user.
if you really like to see which user did the dnf commands we can find the details in [grep 'dnf' /var/log/secure]
this path logs all the entries/commands executed by the user this is similar to dsplog.

another command is just history -> where all the commands executed by a respective user is shown. so instead of asking the user what they have done to resolve a issue we can just switch to that user and type history where all the commands can be seen which are executed by them.

Dnf info <application-name> will show the details like version and everything. if it is installed will show the installed version details if not available details.

how to see all available versions of application: sudo dnf --showduplicates list nginx -> this shows the current installed and available versions of application and from also from which repo the details are being pulled.

output:
Installed Packages
nginx.x86_64                                                                           1:1.20.1-14.el9_2.1                                                                            repos: @rhel-9-appstream-rhui-rpms
Available Packages
nginx.x86_64                                                                           1:1.20.1-10.el9                                                                                rhel-9-appstream-rhui-rpms
nginx.x86_64                                                                           1:1.20.1-13.el9                                                                                rhel-9-appstream-rhui-rpms
nginx.x86_64                                                                           1:1.20.1-14.el9                                                                                rhel-9-appstream-rhui-rpms
nginx.x86_64                                                                           1:1.20.1-14.el9_2.1                                                                            rhel-9

systemctl is a command-line utility used in Linux systems to control the systemd system and service manager. systemd is a system and service manager for Linux that initializes the system and manages services and other system resources.

systemctl list-units --type=service ->  this is used to see all the services in the system. mostly all the services will have .service extension with the application name.
example: nginx (service: nginx.service).

systemctl start <service-name> - will start the service
systemctl stop <service-name> - will stop the service
systemctl restart <service-name> -  will restart the service
systemctl status <service-name> - will show the status like active, enabled/disabled[auto-start of the service upon reboot/start]
systemctl enable <service-name> - auto-start of the service upon reboot [yes]
systemctl disable <service-name> - auto-start of the service upon reboot [No]


Journalctl is very powerful command utility tool that is used to query and view logs from the systemd journal on Linux system.
journalctl -u <service-name> -> this is used to see the logs of a specifc service.

```
journalctl -p err this is used to see the priority level msg from the logs the prioroties are mentioned below i think we mostly use err/warning/emerg

```
Priority levels are: emerg, alert, crit, err, warning, notice, info, debug.

journalctl _MESSAGE_ID=<id> (logs of a specific messaged id)
sudo journalctl _PID=1 (logs from a specific process id)

sudo useradd -r -s /sbin/nologin <username> -> see when free
Configuring Service Files -> see when free.

HTTP status codes and their meaning:

1xx Informational
- 100 Continue: The server has received the request headers, and the client should proceed to send the request body.
- 101 Switching Protocols: The server is switching protocols as requested by the client.

2xx: Success

- 200 OK: The request was successful, and the server has returned the requested data.
- 201 Created: The request was successful, and a new resource was created.
- 202 Accepted: The request has been accepted for processing, but the processing is not complete.
- 203 Non-Authoritative Information: The request was successful, but the returned metadata may be from a local or third-party copy.
- 204 No Content: The request was successful, but there is no content to send in the response.
- 205 Reset Content: The request was successful, and the user agent should reset the document view.
- 206 Partial Content: The server is delivering only part of the resource due to a range header sent by the client.

3xx: Redirection

- 300 Multiple Choices: There are multiple choices for the resource that the client may follow.
- 301 Moved Permanently: The resource has been permanently moved to a new URL.
- 302 Found: The resource resides temporarily under a different URL.
- 303 See Other: The response to the request can be found under a different URL using a GET method.
- 304 Not Modified: The resource has not been modified since the last request.
- 305 Use Proxy: The requested resource must be accessed through a proxy.
- 307 Temporary Redirect: The resource temporarily resides at a different URL, and the client should continue to use the original URL for future requests.
- 308 Permanent Redirect: The resource has been permanently moved to a new URL, and the client should use the new URL for future requests.

4xx: Client Error

- 400 Bad Request: The server could not understand the request due to invalid syntax.
- 401 Unauthorized: The request requires user authentication.
- 402 Payment Required: Reserved for future use, originally intended for digital payment systems.
- 403 Forbidden: The server understands the request but refuses to authorize it.
- 404 Not Found: The server cannot find the requested resource.
- 405 Method Not Allowed: The request method is not allowed for the requested resource.
- 406 Not Acceptable: The resource is not available in a format acceptable to the client.
- 407 Proxy Authentication Required: The client must authenticate with a proxy server.
- 408 Request Timeout: The server timed out waiting for the request.
- 409 Conflict: The request could not be completed due to a conflict with the current state of the resource.
- 410 Gone: The resource is no longer available and will not be available again.
- 411 Length Required: The server requires a Content-Length header field in the request.
- 412 Precondition Failed: One or more preconditions in the request header fields were evaluated to false.
- 413 Payload Too Large: The request entity is larger than the server is willing or able to process.
- 414 URI Too Long: The URI provided was too long for the server to process.
- 415 Unsupported Media Type: The media type of the request data is not supported by the server.
- 416 Range Not Satisfiable: The server cannot provide the requested range of data.
- 417 Expectation Failed: The server cannot meet the expectations specified in the Expect request header field.

5xx: Server Error

- 500 Internal Server Error: The server encountered an unexpected condition that prevented it from fulfilling the request.
- 501 Not Implemented: The server does not support the functionality required to fulfill the request.
- 502 Bad Gateway: The server, while acting as a gateway or proxy, received an invalid response from the upstream server.
- 503 Service Unavailable: The server is currently unable to handle the request due to temporary overloading or maintenance.
- 504 Gateway Timeout: The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server.
- 505 HTTP Version Not Supported: The server does not support the HTTP protocol version that was used in the request.
These status codes are used to indicate the result of an HTTP request and help diagnose and handle various scenarios in web communication.


Commonly used commands:
1. /etc - will have all the configuration data in Linux example: cat /etc/*release will give us the flavor of Linux its version
2. /Proc - contains all the hardware-related data whether it can be processor cpu, modules, disks etc example: cat /proc/cpuinfo - will give hardware level data of the CPU like processor, processor company, and everything. (when taken /proc/cpuinfo - we will have a cache size this parameter value size varies on the processor we have chosen. the cache size also determines the performance of the system) - if there are 2 CPUs then we can see 2 CPU-related information.
3. fdisk -L -> will show the disk and its related information that are attached to the server (hardware related)
4. sudo parted -l -> will show the disk and its related information that are attached to the server (hardware related)
5. df -h -> shows the disk utilization overview of the disks (available memory, occupied extra). where -h stands for human-readable format.
6. Cat -> used to read a file
7. Touch -> used to create a new file
8. how to create a hidden file -> by placing a (.) before the filename it will be hidden. Example: Touch .filename-> this file will be hidden and can only be seen using ls -la
9. how to remove a file -> rm /path to the filename/filename
10. how to rename a file -> mv (source/filename) (destination/renamed filename) example: mv /home/gopi/zomato.txt /home/gopi/swiggy.txt the file will renamed from zomato to swiggy but we have to make sure that swiggy.txt is not present previously if yes then that file will be overwritten.
11. /tmp path files will be deleted/cleared when the system is restarted. it is somewhat similar to QTEMP. but QTEMP data is deleted when the user logoff but for /tmp this will be cleared upon restart of the server.
12. mkdir - to create a dir.
13. cat /etc/passwd - this is a database in the linux where the data of the users are stored. -> if the groupid is 0 it means that user is part of the root group. 
14. cat /etc/group - shows all the group present in the system.
15. tail -> this command is used to see last 10 lines of a file example: tail filename 
16.  how to see last 3 lines or 5 lines of files -> tail -n (number) filepath
17. head -> this command is used to see first 10 lines of a file example: head filename (head or tail by default show 10 lines if we don't specify any paramters)
18.  how to see first 3 lines or 5 lines of files -> tail -n (number) filepath
19. curl is the browser in the linux
20. wget is used to download the browser content
21. uptime gives us the information when the system is up. (load average values are very important to determine the system performance).
22. date -> give us the system date.
23. tar (compresser,decompreser software in linux)
24. zip (compresser decompressor software in linux) 
25. du -h (shows the space occupied by the objects/files in the present working directory and the subtree of the directory)
26. df -h (shows the disk space utilization related information). (-h = human readable format)
27. lsblk - will show the mounted devices
28. type - type gives the location of the application or executable.
29. alias: alias is  command by which we can alias a command to our custom words. example: alias gp="git pull" now gp can be used as aliased command for git pull.
30. Free -m shows the RAM memory availablity: 
free -m
              total        used        free      shared  buff/cache   available
Mem:            767          98         433          11         235         547
Swap:             0           0           0
Adding these together: 98 MB (used)+433 MB (free)+235 MB (buff/cache)=766 MB  (total)
Here's a summary of how each value is calculated:
- total: The sum of all physical RAM.
- used: Memory currently being used by processes.
- free: Memory that is completely unused.
- buff/cache: Memory used for buffers and cache, which can be freed if needed.
- available: An estimate of how much memory is available for new processes, including free memory plus reclaimable memory from buffers and cache.

Swap memory is the virtual memory on the hard disk used by the operating system when the physical RAM is fully utilized or when system requires more memory than the physical RAM.
1. Purpose: Swap memory provides additional virtual memory when physical RAM is fully utilized. It acts as an overflow area for memory that isn't actively being used.
2. Usage: When the system needs more RAM than physically available, it moves inactive pages of memory (those not actively being used) from RAM to the swap space.
3. Performance Impact: Using swap space can significantly slow down the system because accessing data from disk is much slower than from RAM. Hence, excessive swapping (called "thrashing") can degrade system performance.



