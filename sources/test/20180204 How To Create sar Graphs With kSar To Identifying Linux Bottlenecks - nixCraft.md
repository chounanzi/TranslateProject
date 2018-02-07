How To Create sar Graphs With kSar To Identifying Linux Bottlenecks
===================================================================

[![](https://www.cyberciti.biz/media/new/category/old/sysadmin-logo.jpg)](www.cyberciti.biz//www.cyberciti.biz/tips/category/sys-admin &quot;See all UNIX/Linux SysAdmin related news/tips&quot;)

The sar command collects, report, or save UNIX / Linux system activity information. It will save selected counters in the operating system to the /var/log/sa/sadd file. From the collected data, you get lots of information about your server:

1.  CPU utilization
2.  Memory paging and its utilization
3.  Network I/O, and transfer statistics
4.  Process creation activity
5.  All block devices activity
6.  Interrupts/sec etc.

The sar command output can be used for identifying server bottlenecks. However, analyzing information provided by sar can be difficult, so use kSar tool. kSar takes sar command output and plots a nice easy to understand graph over a period of time.

sysstat Package
---------------

The sar, sa1, and sa2 commands are part of sysstat package. Collection of performance monitoring tools for Linux includes

1.  sar : Displays the data.
2.  sa1 and sa2: Collect and store the data for later analysis. The _sa2 shell script_ write a daily report in the /var/log/sa directory. The sa1 shell script collect and store binary data in the system activity daily data file.
3.  sadc &ndash; System activity data collector. You can configure various options by modifying sa1 and sa2 scripts. They are located at the following location:
    *   /usr/lib64/sa/sa1 (64bit) or /usr/lib/sa/sa1 (32bit) &ndash; This calls sadc to log reports to/var/log/sa/sadX format.
    *   /usr/lib64/sa/sa2 (64bit) or /usr/lib/sa/sa2 (32bit) &ndash; This calls sar to log reports to /var/log/sa/sarX format.

### How do I install sar on my system?

Type the following [yum command](www.cyberciti.biz//www.cyberciti.biz/faq/rhel-centos-fedora-linux-yum-command-howto/ &quot;See Linux/Unix yum command examples for more info&quot;) to install sysstat on a CentOS/RHEL based system: `# yum install sysstat` Sample outputs:

```
Loaded plugins: downloadonly, fastestmirror, priorities,
              : protectbase, security
Loading mirror speeds from cached hostfile
 * addons: mirror.cs.vt.edu
 * base: mirror.ash.fastserv.com
 * epel: serverbeach1.fedoraproject.org
 * extras: mirror.cogentco.com
 * updates: centos.mirror.nac.net
0 packages excluded due to repository protections
Setting up Install Process
Resolving Dependencies
--&amp;gt; Running transaction check
---&amp;gt; Package sysstat.x86_64 0:7.0.2-3.el5 set to be updated
--&amp;gt; Finished Dependency Resolution
&nbsp;
Dependencies Resolved
&nbsp;
====================================================================
 Package        Arch          Version             Repository   Size
====================================================================
Installing:
 sysstat        x86_64        7.0.2-3.el5         base        173 k
&nbsp;
Transaction Summary
====================================================================
Install      1 Package(s)
Update       0 Package(s)
Remove       0 Package(s)
&nbsp;
Total download size: 173 k
Is this ok [y/N]: y
Downloading Packages:
sysstat-7.0.2-3.el5.x86_64.rpm               | 173 kB     00:00
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing     : sysstat                                      1/1
&nbsp;
Installed:
  sysstat.x86_64 0:7.0.2-3.el5
&nbsp;
Complete!
```

Loaded plugins: downloadonly, fastestmirror, priorities, : protectbase, security Loading mirror speeds from cached hostfile * addons: mirror.cs.vt.edu * base: mirror.ash.fastserv.com * epel: serverbeach1.fedoraproject.org * extras: mirror.cogentco.com * updates: centos.mirror.nac.net 0 packages excluded due to repository protections Setting up Install Process Resolving Dependencies --&amp;gt; Running transaction check ---&amp;gt; Package sysstat.x86\_64 0:7.0.2-3.el5 set to be updated --&amp;gt; Finished Dependency Resolution Dependencies Resolved ==================================================================== Package Arch Version Repository Size ==================================================================== Installing: sysstat x86\_64 7.0.2-3.el5 base 173 k Transaction Summary ==================================================================== Install 1 Package(s) Update 0 Package(s) Remove 0 Package(s) Total download size: 173 k Is this ok \[y/N\]: y Downloading Packages: sysstat-7.0.2-3.el5.x86\_64.rpm | 173 kB 00:00 Running rpm\_check\_debug Running Transaction Test Finished Transaction Test Transaction Test Succeeded Running Transaction Installing : sysstat 1/1 Installed: sysstat.x86\_64 0:7.0.2-3.el5 Complete!

### Configuration files for sysstat

Edit /etc/sysconfig/sysstat file specify how long to keep log files in days, maximum is a month: `# vi /etc/sysconfig/sysstat` Sample outputs:

```
# keep log for 28 days
# the default is 7
HISTORY=28
```

Save and close the file.

### Find the default cron job for sar

[The default cron job is located](https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/) at /etc/cron.d/sysstat: `# cat /etc/cron.d/sysstat` Sample outputs:

```
# run system activity accounting tool every 10 minutes
*/10 * * * * root /usr/lib64/sa/sa1 1 1
# generate a daily summary of process accounting at 23:53
53 23 * * * root /usr/lib64/sa/sa2 -A
```

### Tell sadc to report statistics for disks

Edit the /etc/cron.d/sysstat file using a text editor such as NA command or vim command, enter: `# vi /etc/cron.d/sysstat` Update it as follows to log all disk stats (the -d option force to log stats for each block device and the -I option force report statistics for all system interrupts):

```
# run system activity accounting tool every 10 minutes
*/10 * * * * root /usr/lib64/sa/sa1 -I -d 1 1
# generate a daily summary of process accounting at 23:53
53 23 * * * root /usr/lib64/sa/sa2 -A 
```

On a CentOS/RHEL 7.x you need to pass the `-S DISK` option to collect data for block devices. Pass the `-S XALL` to collect data about:

1.  Disk
2.  Partition
3.  System interrupts
4.  SNMP
5.  IPv6

```
# Run system activity accounting tool every 10 minutes
*/10 * * * * root /usr/lib64/sa/sa1 -S DISK 1 1
# 0 * * * * root /usr/lib64/sa/sa1 600 6 &amp;
# Generate a daily summary of process accounting at 23:53
53 23 * * * root /usr/lib64/sa/sa2 -A
```

Save and close the file. Turn on the service for a CentOS/RHEL version 5.x/6.x, enter: `# chkconfig sysstat on # service sysstat start` Sample outputs:

```
Calling the system activity data collector (sadc): 
```

For a CentOS/RHEL 7.x, run the following commands: `# systemctl enable sysstat # systemctl start sysstat.service # systemctl status sysstat.service` Sample outputs:

```
● sysstat.service - Resets System Activity Logs
   Loaded: loaded (/usr/lib/systemd/system/sysstat.service; enabled; vendor preset: enabled)
   Active: active (exited) since Sat 2018-01-06 16:33:19 IST; 3s ago
  Process: 28297 ExecStart=/usr/lib64/sa/sa1 --boot (code=exited, status=0/SUCCESS)
 Main PID: 28297 (code=exited, status=0/SUCCESS)
&nbsp;
Jan 06 16:33:19 centos7-box systemd[1]: Starting Resets System Activity Logs...
Jan 06 16:33:19 centos7-box systemd[1]: Started Resets System Activity Logs.
```

● sysstat.service - Resets System Activity Logs Loaded: loaded (/usr/lib/systemd/system/sysstat.service; enabled; vendor preset: enabled) Active: active (exited) since Sat 2018-01-06 16:33:19 IST; 3s ago Process: 28297 ExecStart=/usr/lib64/sa/sa1 --boot (code=exited, status=0/SUCCESS) Main PID: 28297 (code=exited, status=0/SUCCESS) Jan 06 16:33:19 centos7-box systemd\[1\]: Starting Resets System Activity Logs... Jan 06 16:33:19 centos7-box systemd\[1\]: Started Resets System Activity Logs.

How Do I Use sar? How do I View Stats?
--------------------------------------

Use the sar command to display output the contents of selected cumulative activity counters in the operating system. In this example, sar is run to get real-time reporting from the command line about CPU utilization: `# sar -u 3 10` Sample outputs:

```
Linux 2.6.18-164.2.1.el5 (www-03.nixcraft.in) &Tab;12/14/2009

09:49:47 PM       CPU     %user     %nice   %system   %iowait    %steal     %idle
09:49:50 PM       all      5.66      0.00      1.22      0.04      0.00     93.08
09:49:53 PM       all     12.29      0.00      1.93      0.04      0.00     85.74
09:49:56 PM       all      9.30      0.00      1.61      0.00      0.00     89.10
09:49:59 PM       all     10.86      0.00      1.51      0.04      0.00     87.58
09:50:02 PM       all     14.21      0.00      3.27      0.04      0.00     82.47
09:50:05 PM       all     13.98      0.00      4.04      0.04      0.00     81.93
09:50:08 PM       all      6.60      6.89      1.26      0.00      0.00     85.25
09:50:11 PM       all      7.25      0.00      1.55      0.04      0.00     91.15
09:50:14 PM       all      6.61      0.00      1.09      0.00      0.00     92.31
09:50:17 PM       all      5.71      0.00      0.96      0.00      0.00     93.33
Average:          all      9.24      0.69      1.84      0.03      0.00     88.20
```

Where,

*   3 = interval
*   10 = count

To view process creation statistics, enter: `# sar -c 3 10` To view I/O and transfer rate statistics, enter: `# sar -b 3 10` To view paging statistics, enter: `# sar -B 3 10` To view block device statistics, enter: `# sar -d 3 10` To view statistics for all interrupt statistics, enter: `# sar -I XALL 3 10` To view device specific network statistics, enter: `# sar -n DEV 3 10 # sar -n EDEV 3 10` To view CPU specific statistics, enter: `# sar -P ALL # Only 1st CPU stats # sar -P 1 3 10` To view queue length and load averages statistics, enter: `# sar -q 3 10` To view memory and swap space utilization statistics, enter: `# sar -r 3 10 # sar -R 3 10` To view status of inode, file and other kernel tables statistics, enter: `# sar -v 3 10` To view system switching activity statistics, enter: `# sar -w 3 10` To view swapping statistics, enter: `# sar -W 3 10` To view statistics for a given process called Apache with PID # 3256, enter: `# sar -x 3256 3 10`

Say Hello To kSar
-----------------

sar and sadf provides CLI based output. The output may confuse all new users / sys admin. So you need to use kSar which is a java application that graph your sar data. It also permit to export data to PDF/JPG/PNG/CSV. You can load data from three method : local file, local command execution, and remote command execution via SSH. kSar supports the sar output of the following OS:

1.  Solaris 8, 9 and 10
2.  Mac OS/X 10.4+
3.  Linux (Systat Version &gt;= 5.0.5)
4.  AIX (4.3 &amp; 5.3)
5.  HPUX 11.00+

### Download And Install kSar

Visit the [official](https://github.com/vlsi/ksar) website and grab the latest source code. Use [wget to](www.cyberciti.biz//www.cyberciti.biz/tips/linux-wget-your-ultimate-command-line-downloader.html) download the source code, enter: `$ wget https://github.com/vlsi/ksar/releases/download/v5.2.4-snapshot-652bf16/ksar-5.2.4-SNAPSHOT-all.jar`

#### How Do I Run kSar?

Make sure [JAVA jdk](www.cyberciti.biz//www.cyberciti.biz/faq/howto-ubuntu-linux-install-configure-jdk-jre/) is installed and working correctly. Type the following command to start kSar, run: `$ java -jar ksar-5.2.4-SNAPSHOT-all.jar`

![Fig.01: kSar welcome screen](https://www.cyberciti.biz/media/new/tips/2009/12/sar-welcome.png &quot;kSar welcome screen&quot;)

Fig.01: kSar welcome screen

Next you will see main kSar window, and menus with two panels.

![Fig.02: kSar - the main window](https://www.cyberciti.biz/media/new/tips/2009/12/screenshot-kSar-a-sar-grapher-01.png &quot;kSar - the main window&quot;)

Fig.02: kSar - the main window

The left one will have a list of graphs available depending on the data kSar has parsed. The right window will show you the graph you have selected.

How Do I Generate sar Graphs Using kSar?
----------------------------------------

First, you need to grab sar command statistics from the server named server1. Type the following command to get stats, run: `[**server1** ]# LC_ALL=C sar -A &gt; /tmp/sar.data.txt` Next copy file to local desktop from a remote box using the scp command: `[**desktop** ]$ scp user@server1.nixcraft.com:/tmp/sar.data.txt /tmp/` Switch to kSar Windows. Click on **Data** &gt; **Load data from text file** \&gt; Select sar.data.txt from /tmp/ &gt; Click the **Open** button. Now, the graph type tree is deployed in left pane and a graph has been selected:

![Fig.03: Processes for server1](https://www.cyberciti.biz/media/new/tips/2009/12/cpu-ksar.png &quot;Linux kSar Processes for server1 &quot;)

Fig.03: Processes for server1

![Fig.03: Disk stats (blok device) stats for server1](https://www.cyberciti.biz/media/new/tips/2009/12/disk-stats-ksar.png &quot;Linux Disk I/O Stats Using kSar&quot;)

Fig.04: Disk stats (blok device) stats for server1

![Fig.05: Memory stats for server1](https://www.cyberciti.biz/media/new/tips/2009/12/memory-ksar.png &quot;Linux Memory paging and its utilization stats&quot;)

Fig.05: Memory stats for server1

#### Zoom in and out

Using the move, you can interactively zoom onto up a part of a graph. To select a zone to zoom, click on the upper left conner and while still holding the mouse but on move to the lower-right of the zone you want to zoom. To come back to unzoomed view click and drag the mouse to any corner location except a lower-right one. You can also right click and select zoom options

#### Understanding kSar Graphs And sar Data

I strongly recommend reading sar and sadf command man page: `$ man sar $ man sadf`

Case Study: Identifying Linux Server CPU Bottlenecks
----------------------------------------------------

With sar command and kSar tool, one can get the detailed snapshot of memory, CPU, and other subsystems. For example, if CPU utilization is more than 80% for a long period, a CPU bottleneck is most likely occurring. Using **sar -x ALL** you can find out CPU eating process. The output of [mpstat command](www.cyberciti.biz//www.cyberciti.biz/tips/how-do-i-find-out-linux-cpu-utilization.html) (part of sysstat package itself) will also help you understand the cpu utilization. You can easily analyze this information with kSar.

### I Found CPU Bottlenecks&hellip;

Performance tuning options for the CPU are as follows:

1.  Make sure that no unnecessary programs are running in the background. Turn off [all unnecessary services on Linux](www.cyberciti.biz//www.cyberciti.biz/faq/check-running-services-in-rhel-redhat-fedora-centoslinux/).
2.  Use [cron to schedule](www.cyberciti.biz//www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/) jobs (e.g., backup) to run at off-peak hours.
3.  Use [top and ps command](www.cyberciti.biz//www.cyberciti.biz/faq/show-all-running-processes-in-linux/) to find out all non-critical background jobs / services. Make sure you lower their priority using [renice command](www.cyberciti.biz//www.cyberciti.biz/faq/howto-change-unix-linux-process-priority/).
4.  Use [taskset command to set a processes&rsquo;s](www.cyberciti.biz//www.cyberciti.biz/faq/taskset-cpu-affinity-command/) CPU affinity (offload cpu) i.e. bind processes to different CPUs. For example, run MySQL database on cpu #2 and Apache on cpu # 3.
5.  Make sure you are using latest drivers and firmware for your server.
6.  If possible add additional CPUs to the system.
7.  Use faster CPUs for a single-threaded application (e.g. Lighttpd web server app).
8.  Use more CPUs for a multi-threaded application (e.g. MySQL database server app).
9.  Use more computer nodes and set up a [load balancer](www.cyberciti.biz//www.cyberciti.biz/tips/load-balancer-open-source-software.html) for a web app.

isag &ndash; Interactive System Activity Grapher (alternate tool)
-----------------------------------------------------------

The isag command graphically displays the system activity data stored in a binary data file by a previous sar run. The isag command invokes sar to extract the data to be plotted. isag has limited set of options as compare to kSar.

![Fig.06: isag CPU utilization graphs](https://www.cyberciti.biz/media/new/tips/2009/12/isag.cpu_.png &quot;Fig.06: isag CPU utilization graphs&quot;)

Fig.06: isag CPU utilization graphs

#### References:

*   [How do I Find Out Linux CPU Utilization?](www.cyberciti.biz//www.cyberciti.biz/tips/how-do-i-find-out-linux-cpu-utilization.html)
*   [kSar](https://github.com/vlsi/ksar) home page.
*   [isag](http://mujweb.cz/linux_monitor/isag/) home page.

Posted by: Vivek Gite
---------------------

The author is the creator of nixCraft and a seasoned sysadmin and a trainer for the Linux operating system/Unix shell scripting. He has worked with global clients and in various industries, including IT, education, defense and space research, and the nonprofit sector. Follow him on [Twitter](https://twitter.com/nixcraft), [Facebook](https://facebook.com/nixcraft), [Google+](https://plus.google.com/+CybercitiBiz). Get the **latest tutorials on SysAdmin, Linux/Unix and open source topics via [my RSS/XML feed](https://www.cyberciti.biz/atom/atom.xml)**.

[GOT FEEDBACK? CLICK HERE TO JOIN THE DISCUSSION](https://www.nixcraft.com/)