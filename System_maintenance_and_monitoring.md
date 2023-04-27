## getting cpu information in proc directory

=>cd /proc
=> ls -p | grep -v / |column

<!-- this grep -v will exclude everything that starts with / and we piping through column that will show in column -->

=> cat cpuinfo

<!-- cpu info is a file that contains every information about the cpu
you can get how many core the cpu had 
cpu model,model name etc
 -->

=> cat cpuinfo| grep "processor"
=> cat cpuinfo| grep "model name"

<!-- you can filter information about the cpu info -->

=> uptime

<!-- uptime command give you two information 
	first it shows you the time
	second this will show how much time 
	it is on 
-->

=>cat meminfo

<!-- it will give you all the infrmation about 
	your memory or ram
 -->

=>cat meminfo | grep "MemTotal"
=>cat meminfo | grep "MemFree"

<!-- get the total memory size in KB -->
<!-- get the total free memory in KB  -->

<!-- there is a easy way to do that
	getting memory info in human redable form
 -->

 => free -h
<!-- this will show the memory used shared swap in human readable format -->

<!-- how many processor does your cpu has? -->
<!-- ans -->
=> cat cpuinfo | grep "processor"

## Storage and Network Bandwidth

=>df
<!--df command will show all the file system and where it is mounted

but there is a problem 
when you install any package with snap it will create a separate filesystem/partition for that
to see the filesystem without that the command is bellow
-->

<!-- we exclude the snap with grep -v command -->

=> df -h | grep -v snap
or
=> lsblk | grep -v snap

## Network and band width

<!-- if you need to monitor traffic in a network interface in your device you need a 
tool called iftop 
you might need to install it with your package manager
-->

<!-- first you choose your network interface
then copy the ip address then give this command -->

=>iftop -i <interface_name>


## System monitoring tools

<!-- install cockpit for System GUI monitoring -->
=> sudo yum update -y
=> sudo yum install cockpit -y 

=> sudo apt update -y
=> sudo apt install cockpit -y

<!-- after installing cockpit you start the service -->
=> systemctl start cockpit
=> systemctl status cockpit

<!-- remember cockpit starts at port 9090 -->
<!-- so go to the localhost:9090 -->
<!-- it will show storafe management,
service management
user management
network status management etcc
 -->

 ## controlling system resource

<!-- lets thin the current process is a cockpit -->
<!-- and it is taking a huge resource and we need to stop it down and 
disable so it wont start on the startup -->
<!-- get the ststus of a current status -->

=> systemctl status cockpit
=> systemctl stop cockpit
=> systemctl status cockpit
=> systemctl disable cockpit 


<!-- you can kill the process using kill and killl command  -->
<!-- you need the PID or name of the processs to kill it -->

<!-- suppose making 3 background ptocess -->
=>ping 8.8.8.8 &
=>ping 8.8.8.8 &
=>ping 8.8.8.8 &


<!-- kill the process  -->
=> sudo kill <PID>
=> sudo killall ping


## Maintaining System Hardware Intergity And Information

<!-- monitoring the CPU and RAm and Other hardware -->

<!-- find the linux kernel that you are using commmand -->
=>uname -a

<!-- it will show the machine name kernel with version and OS namae etc -->

<!-- getting the hardware information  -->

=>sudo dmidecode

<!-- this will give you a lot of information -->
<!-- you can filter the information to get the CPU Speed,Mother Board,Processor Memory Storage hardware information -->

➜  ~ sudo dmidecode -s chassis-type
Notebook
➜  ~ sudo dmidecode -s baseboard-product-name
81E5
➜  ~ 
➜  ~ sudo dmidecode -s processor-frequency   
1800 MHz


<!-- dmi decode will give a messy information to geta  clean structure information
we use the lshw command
 -->

 => sudo lshw -short


 ## Disk Check Monitoring
 <!--  first you need a package name smartmontools -->
 =>sudo apt install smartmontools -y
 =>sudo yum install smartmontools -y


 <!-- then applt lsblk to find the storage name you want to test -->

 =>lsblk

<!--  now we need to check if the storafe is compatable with the package -->
<!-- because not all system is compatable with the system -->

=>sudo smartctl -i /dev/sda


<!-- is support is enables then start the test -->

=> sudo smartctl -t short /dev/sda

<!-- it will tell you to wait 2/3 munites while it work in the background -->

<!-- how the output with this command  -->
=> sudo smartctl -l selftest /dev/sda
