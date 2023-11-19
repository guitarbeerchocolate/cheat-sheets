# GNU/Linux notes

## List files

`ls` Lists all files and directories in the present working directory.

`ls -R` Lists files in sub-directories as well.

`ls -a` Lists hidden files as well.

`ls -al` Lists files and directories with detailed information like permissions,size, owner, etc.

## Working with files and directories

'cat > <filename>' Creates a new file.

`cat <filename>` Displays the file content.

`cat <file1> <file2> > <file3>` Joins two files (file1, file2) and stores the output in a new file (file3).

`mv <file> <new_file_path>` Moves the files/directories to the new location.

`mv <filename> <new_file_name>` Renames the file/directory to a new filename.

`rm <filename>` Deletes a file.

`mkdir <directoryname>` Creates a new directory in the present working directory or a at the specified path.

`rmdir <directoryname>` Deletes a directory.

`pr -n <filename>` Denotes the file with Line Numbers.

`cp <filename> <new filename>` copy - Make a copy of a file.

`cp -R <directory> <new directory>` Make a copy of a directory.

`grep -r "jimmy"` Search recursively for pattern in directory.

`find . -name 'templates'` Find files or directories from current location.

`tail -20 <file_name>` Show the last x lines of a file, 10 by default.

`diff <file1> <file2>` Compare 2 files.

## File Permissions:

`chmod u+x <filename>` Change permission of the named file to executable.

`chown <username> <filename>` Change the ownership of a file.

`chown <user>:<group> <filename>` Change the owner and group ownership of a file.

`chown -R <user>:<group> <dirname>` Change the owner and group ownership of the directory and all sub-directories.

## Environment Variables

`env` Displays all environment variables.

`echo $VARIABLE` To display value of a variable.

`unset $VARIABLE` Remove a variable.

`export $VARIABLE=<value>` To set value of an environment variable.

## Commands

`history` Gives a list of all past commands typed in the current terminal session.

`|` Pipe (redirect) output.

`<command> &` run < command> and send task to background.

`>> <fileA>` append to fileA, preserving existing contents.

`> <fileA>` output to fileA, overwriting contents.

`1>2&` Redirect stdout to stderr.

`pwd` Path of working directory - tells you what directory you are in.

`tar -zcvf  <filename> <directory>` Create gzipped tar archive of <directory>.

`tar -xvzf  <filename>` Extract tarred, gzipped <filename> in current directory.

`file <filename>` View the type of any file.

`rsync -avz <directory1> <directory2>` Synchronize the changes of one directory to another.

`whoami` See which user you are currently logged in as.

`reboot` Reboot the system.

`poweroff` Shut down the system.

`tree` View the directory structure for a path.

`uname -a` Output detailed information about your kernel version and architecture.

`uptime` Show uptime.

## User management

`sudo adduser <username>` To add a new user.

`sudo passwd -l '<username>'` To change the password of a user.

`sudo userdel -r '<username>'` To remove a newly created user.

`sudo usermod -a -G <groupname> <username>` To add a user to a group.

`sudo deluser <username> <groupname>` To remove a user from a group.

`finger` Shows information of all the users logged in.

`finger <username>` Gives information of a particular user.

## Networking

`SSH <username>@<ip-address> or <hostname>` Log into a remote Linux machine using SSH.

`ping <hostname>` To ping and Analyzing network and host connections.

`netstat -r -v` print network information, routing and connections.

`put <file>` Upload ‘file’ from local to remote computer.

`get <file>` Download ‘file’ from remote to local computer.

`quit` Logout.

`ip a` Show IP address and other information for all active interfaces.

`ip r` Show IP address of default gateway.

`cat /etc/resolv.conf`See what DNS servers your system is configured to use.

`traceroute` Trace the network path taken to a device.

## Process commands

`bg <PID>` To send a process to the background.

`fg <PID>` To run a stopped process in the foreground.

`top` Details on all Active Processes.

`ps` Give the status of processes running for a user.

`ps <PID>` Gives the status of a particular process.

`pidof <PID>` Gives the Process ID (PID) of a process.

`kill <PID>` Kills a process.

`df` Gives free hard disk space on your system.

`free -m` Gives free RAM on your system.

## Storage

`df -h` See the current storage usage of mounted partitions.

`sudo fdisk -l` See information for all attached storage devices.

`du` See disk usage of a directory’s contents.

## Hardware

`lspci` See general information about host bridge, VGA controller, ethernet controller, USB controller, SATA controller, etc.

`dmidecode` See some information about BIOS, motherboard, chassis, etc.

`lshw` List all hardware components and see their configuration details.

`hwinfo` List details for all hardware, including their device files and configuration options.

`biosdecode` Get some general information about your system’s BIOS.

`lsusb` Get a list of USB devices plugged into your system.

## Editors

vi, pico, emacs
