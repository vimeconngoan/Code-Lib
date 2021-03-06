# Basic Network Commands
===========================  
1. `$/usr/sbin/arp -a`    # Print out ARP table  
2. Check IP or Domain info
   ```
   $dig stcloudstate.edu     # get IP address (UDP)
   $dig -x 199.17.59.234     # get domain related to IP
   $nslookup  199.17.59.234  # the same to previous
   $whois stcloudstate.edu   # print out info related to the IP or domain
   ```
3. Check netstat  
   ```
   $netstat -an                        # print litsening and established ports
   $netstat -i                         # like $ifconfig
   $netstat -r                         # routing table and check zones
   $sudo netstat -apeen | grep java    # all protocols ethernet number format for java
   $netstat -pave | more
   ```
4. Trace IP or Domain hops
   ```
   $mtr -n www.google.com       # how many hops to get the IP
   $traceroute www.google.com
   ```
5. Communicate to a host with TCP/UDP
   ```
   $telnet 127.0.0.1         # communicate with a host (TCP)
   $lynx www.google.com      # browser info for World Wide Web (TCP)
   ```
6. Check processes
   ```
   $ps -aux | grep sshd      # find sshd pid
      D --uninterruptible sleep
      R --Running or runnable (on run queue)
      S --Interrutible sleep (waiting for an event to complete)
      T --Stopped, either by a job control signal or because it is being traced
      W --paging (not valid since kernel 2.6)
      X --dead (should never be seen)
      Z --Defunct ("zombie") process, terminated but not reaped by its parent
   $ps -ALF | grep python    # list all python related lwps
   $ps -ely
   $ps -jHax | grep 1135200103 (tty of sshd)
   $ps -ejH
   $ps -eHx
   $ps -axZ
   ```
7. List stuff
   ```
   $ls -las  # list all in current folder with permission and block number
   $ls -al   # list all file with metadata and total
   $lsmod    # list modules
   $lsof     # list open files
   $lsof -t ~/keyfile.txt  #find pid related to a given file
   $lsof -p 481            #check the file related pid
   $lsblk    # list block
   $sudo lshw -short -C disk
   $sudo lshw -class disk -class storage
   ```
8. Info command
   ```
   $whereis rpcinfo                   # find where is the rpcinfo  
   $/usr/sbin/rpcinfo   -p 10.10.3.18 # rpc call to rpc server, show all registered services on rpcbind
   $modinfo nfs                       # print out module info
   $ps -fe | grep rpc                 # 
   $file /usr/bin/rpcgen              # easy to generate RPC programs in C using rpcgen
   ```

9. Check inportant info
   ```
   $vmstat        # VM stat
   $mpstat -P ALL # Multiprocessing stat for all CPU (if 0, for CPU 0)
   $mpstat -A     # all CPU stat (R-running,D-Uninterruptible Sleep,S-sleep,T-stopped,W-pagging,X-dead,Z-zombie)
   $uname -a      # info of Linux
   ```
10. `mount | grep nfs`   # find location of nfs
   ```
   Common mount options:
   rw     --Mounts the FS for reading and writing
   ro     --reading only
   noexec --limits execution of dangerous code
   nosuid --Limits inheritance of super-user rights
   nouser --Disallows an ordinary user to mount or unmount FS
   user   --allows ...
   auto   --Allows FS to be mounted automatically using mount -a command
   noauto --Default behavior disallows ...
   async  --All I/O to FS should be done asynchronously
   noatime--Do not update inode access times on this FS
   nodev  --Do not interpret character or block special devices on the FS
   defaults-Provides an alias for async, auto,dev,exec,nouser,rw,suid
   remount--Remounts the FS in case it is already mounted
   ```
11. Check file metadata
   ```
   $file <filename>      # check file type format
   $stat --format "%F" <filename> #the same to $file
   $cat  <filename>      # show file content if ASCII
   $stat <filename>      # show file detail metadata, "%y" --last modification, "%o" --number of blocks
   $xxd  <filename>      # check file primary data if ASCII
   $xxd -E ebcdic.txt    #if EBCDIC type
   Note: output of stat, the link number shows the hard links.
   ```
12. Kill  
   ```
   1) $kill -9 <pid#>           # kill process anyway  
   2) $kill -s <signal> <pid#>  # kill can send signal to a process, default TERM
   	  $kill -SIGTSTP 1126   #stop pid
   	  $kill -SIGCONT 1126   #restart pid
   ```
13. Fuser  --find which process is using a file or directory or a socket
   ```
   1) nc -l -p 1234   #create a port listening
   2) fuser -v -n tcp 1234
   3) fuser -k 1234/tcp   #kill process which created the port
   ```
14. `$history | grep nc`    #list all about nc command
15. `$klist`                #list ticket cache of Kerberos **Hacker like this**
16. `$w` OR `$who -uH`      #**Hacker like IDLE**
17. sha512sum **the xxx and sha512xxx should be in the same folder**
   ```
   $sha512sum xxx > sha512xxx
   $sha512sum -c sha512xxx        #check it
   $cat sha512xxx | sha512sum -c  #echo check
   ```
18. `$top -d 0.00001`             #most severe denial of service **Hacker like it**
19. Redirection  **ctl + d** to end of file
   ```
   1) $ls > /tmp/tmp_ls  #create new file containing the output of ls
   2) $echo 'Another line' >> /tmp/tmp_ls  #append a new line
   3) $find '' 2> stderr_log.txt   #standard error
   4) $wc '' 2>> stderr_log.txt    #append error
   3) < for input, << for input append  
   ```
20. Multiple commands
   ```
   1) $ls -l ; cat /etc/passwd
   2) $date && ls -l
   ```
21. Backticks:
   ```
   $kill `cat /var/run/named/named.pid`
   ```
22. Find
   ```
   $find . -atime 7
   $find . -name core -exec rm {} \; #find all named core file and delete them
   $find . -size -100k               #find all size less than 100k files
   ```
23. Compression
   ```
   1) $gzip myfile.txt          #myfile.txt.gz
      $gzip -d myfile.txt.gz    #decompress
     `$gzip -9 *.html`         #compress multiple files
      $cat b1 b2 b3 | gzip > allb.gz
      $gzip -l allb.gz
   2) bzip2    #same to the previous
   3) $tar -cf archive.tar foo bar  # Create archive.tar from files foo and bar.
      $tar -tvf archive.tar         # List all files in archive.tar verbosely.
      $tar -xf archive.tar          # Extract all files from archive.tar.
   ```
24. Filters for pipe (find, grep, wc, tee, and tr)
   ```
   $wc /etc/magic | tee magic_count.txt  #create a new file or overwrite the file
   `$ls ~ | grep *tar | tr e E >> ls_log.txt`  #find and replace e to E
   ```
25. Check if your linux using UUID (using it to manage hard drives easily)
   ```
   $cat /proc/cmdline
   $cat /etc/fstab
   $findfs UUID=a98fee64-4820-4802-8fe5-2e6e07208980
   ```
26. Getfacl
   ```
   $getfacl ~/www2/bios # permission show
   $nfs4_getfacl ~/www2/bios
   $nfs4_getfacl -H  #<type>:<flags>:<principal>:<permission>
   ```
27. ss --display more socket and state information, like `$netstat`
   ```
   $ss -itoea | grep 5000  #internal TCP info, TCP,FIN-wait-1,Detail,All
   ```
28. Watch --execute a program periodically, showing output fullscreen
   ```
   $watch -n 1 ls -l xxxx
   $chmod 777 xxxx
   ```
29. Links (**Cannot make a across partition hard link**)
   ```
   $ln -s sourceFile newSymbolicLink  #create a symbolic link
   $ln sourceFile newHardLink         #create a hard link
   $rm newSymbolicLink
   $rm newHardLink
   ```
30. Check hardware, like cache and buffer speed, specs
   ```
   $sudo hdparm -tT /dev/sda1    #cache faster than buffer
   $sudo hdparm -t /dev/mem
   $sudo hdparm -I /dev/sda      #show hardware specs
   $cat /proc/cpuinfo
   $cat /proc/meminfo
   $cat /proc/diskstats
   $sudo fdisk -l                #display disk parameters
   $sudo dmidecode | more        #include bus size
   $iostat -x 1
   ```
31. `$cal -j`   #days of year
32. Check out file physical size
   ```
   $ls -las data.txt   #block # check out 41
   $sudo blockdev --getbsz /dev/sda1  #block size
   #block size * # of blocks = physical size
   ```
33. `strace -p 18523`   #pid, used to trace process read and write  
    `strace -C /usr/bin/who`  #trace command who<br/>
    strace can trace unnamed pipes and named pipes. **Hacker like that**
34. Random Access
   ```
   $head -$((${RANDOM} % `wc -l < car.csv` + 2)) car.csv | tail -1  #random query, head: first n line, tail: last n lines
   $awk -f ./awkindexlu -v indexes="1 2 3 4 5 6 7 10" indexed.dat | sort -n
   $cat > index.txt    #2 4 6 8
   $awk -f ./awkindexlu -v indexes="`index.txt`" indexed.dat | sort -n
   $awk '{print $1","$2","$3}' < index.txt > index.csv
   $cat > indexneg.txt  #-3 -5 -7
   $awk -f ./awkindexlu -v indexes="`indexneg.txt`" indexed.dat | sort -n
   ```
35. Performance
   ```
   `perf stat -B java class PrimeByVector`  #performance analysis tool  
   `perf stat -B sleep 5`
   $time cat /etc/services
   $time cat /ramdisk/services
   $time cat services
   ```
36. `$uptime`   #how long box is running
37. pmap --report memory map of a process
   ```
   $pmap -x 28961 | grep stack
   ```
38. `$id`   #show detail of current user
39. `$chmod o+t ~/stickeyDir`   #prevent deleting this directory  
    `$chmod 1754 ~/stickydir`   #1 means sticky bit set
40. touch command, used to hide hacker foot print
   ```
   $touch filename                  #change all timestamps
   $touch -m filename               #change modification time
   $touch -c -t 0101011111 filename #change access and modification time
   ```
41. ls -ls file1 vs stat file1 about block number (default block size 1024 vs 512)
   ```
   $ stat xxxx
      File: ‘xxxx’
      Size: 207             Blocks: 8          IO Block: 524288 regular file
   $ ls -las xxxx
      4 -rwxr-xr-x 1 BCRL\zhao.xie BCRL\domain^users 207 Sep 21 00:09 xxxx
   $ du xxxx
      4       xxxx
   $ stat --format=%b xxxx   #show number of blocks
      8
   $ stat --format=%B xxxx   #show block size
      512
   $ ls -lsa --block-size=512 xxxx
      8 -rwxr-xr-x 1 BCRL\zhao.xie BCRL\domain^users 1 Sep 21 00:09 xxxx
   $ ls -lsa xxxx
      4 -rwxr-xr-x 1 BCRL\zhao.xie BCRL\domain^users 207 Sep 21 00:09 xxxx
   ```
42. `$chkconfig` RedHat command to check runlevels for services.
43. VMware command
   ```
   WMwareToolboxCmd.exe    #Windows
   wmware-toolbox-cmd      #Linux
   vmware-tools-cli        #Mac

   wmware-toolbox-cmd stat hosttime       #show date and time
   wmware-toolbox-cmd stat speed          #display cpu speed in MHz
   wmware-toolbox-cmd stat balloon        #amount of memory recliamed from VM
   wmware-toolbox-cmd stat swap           #amount of memory swapped out to the VM
   wmware-toolbox-cmd stat memlimit       #memory limit info
   wmware-toolbox-cmd stat memres         #memory reservation info in MB
   wmware-toolbox-cmd stat cpures         #cpu reservation info
   wmware-toolbox-cmd stat cuplimit       #CPU limit info
   wmware-toolbox-cmd stat sessionid      #current session ID
   ```
44. Logger
   ```
   1) $logger -i Log an event and login `ssh james1@eros`& 
   & --the shell executes the command in the background in a subshell. The shell
   does not wait for the command to finish, and return status is 0.
   2) $cat display
      logger -i -f $1
      echo $PPID
      cat zztop
      $./display zztop
      26533
      I Darren Get paid
   ```
45. Find user ID that owns a daemon `cat /etc/passwd | grep mysql`
46. List all local users: `cut -d: -f1 /etc/passwd`
47. Lost and reset your user password:
   ```
   1) Restart with shift holding press, or esc when restarting
   2) recovery mode, choose root
   3) mount -n -o remount,rw /
      passwd <username>
48. Reset root password (Ubuntu)
   ```
   sudo passwd root
   # remove passwd and lock root
   sudo passwd -dl root
   ```
