How to print filename with awk on Linux / Unix
==============================================

[![](https://www.cyberciti.biz/media/new/category/old/unix-logo.gif)](www.cyberciti.biz//www.cyberciti.biz/faq/category/unix/ "See all UNIX related articles/faq")

I would like to print filename with awk on Linux / Unix-like system. How do I print filename in BEGIN section of awk? Can I print the name of the current input file using gawk/awk? The name of the current input file set in FILENAME variable. You can use FILENAME to display or print current input file name If no files are specified on the command line, the value of FILENAME is “-” (stdin). However, FILENAME is undefined inside the BEGIN rule unless set by getline.

How to print filename with awk
------------------------------

The syntax is: `awk '{ print FILENAME }' fileNameHere awk '{ print FILENAME }' /etc/hosts` You might see file name multiple times as awk read file line-by-line. To avoid this problem update your awk/gawk syntax as follows: `awk 'FNR == 1{ print FILENAME } ' /etc/passwd awk 'FNR == 1{ print FILENAME } ' /etc/hosts` [![How to print filename using awk on Linux or Unix](https://www.cyberciti.biz/media/new/faq/2018/02/How-to-print-filename-using-awk-on-Linux-or-Unix.jpg)](https://www.cyberciti.biz/media/new/faq/2018/02/How-to-print-filename-using-awk-on-Linux-or-Unix.jpg)

How to print filename in BEGIN section of awk
---------------------------------------------

Use the following syntax: `awk 'BEGIN{print ARGV[1]}' fileNameHere awk 'BEGIN{print ARGV[1]}{ print "someting or do something on data" }END{}' fileNameHere awk 'BEGIN{print ARGV[1]}' /etc/hosts` Sample outputs:

```
/etc/hosts
```

However, ARGV\[1\] might not always work. For example: `ls -l /etc/hosts | awk 'BEGIN{print ARGV[1]} { print }'` So you need to modify it as follows (assuming that ls -l only produced a single line of output): `ls -l /etc/hosts | awk '{ print "File: " $9 ", Owner:" $3 ", Group: " $4 }'` Sample outputs:

```
File: /etc/hosts, Owner:root, Group: roo
```

How to deal with multiple filenames specified by a wild card
------------------------------------------------------------

Use the following simple syntax: `awk '{ print FILENAME; nextfile } ' *.c awk 'BEGIN{ print "Starting..."} { print FILENAME; nextfile }END{ print "....DONE"} ' *.conf` Sample outputs:

```
Starting...
blkid.conf
cryptconfig.conf
dhclient6.conf
dhclient.conf
dracut.conf
gai.conf
gnome_defaults.conf
host.conf
idmapd.conf
idnalias.conf
idn.conf
insserv.conf
iscsid.conf
krb5.conf
ld.so.conf
logrotate.conf
mke2fs.conf
mtools.conf
netscsid.conf
nfsmount.conf
nscd.conf
nsswitch.conf
openct.conf
opensc.conf
request-key.conf
resolv.conf
rsyncd.conf
sensors3.conf
slp.conf
smartd.conf
sysctl.conf
vconsole.conf
warnquota.conf
wodim.conf
xattr.conf
xinetd.conf
yp.conf
....DONE

```

nextfile tells awk to stop processing the current input file. The next input record read comes from the next input file. For more information see awk/[gawk](https://www.gnu.org/software/gawk/manual/) command man page: `man awk man gawk`

Posted by: Vivek Gite
---------------------

The author is the creator of nixCraft and a seasoned sysadmin and a trainer for the Linux operating system/Unix shell scripting. He has worked with global clients and in various industries, including IT, education, defense and space research, and the nonprofit sector. Follow him on [Twitter](https://twitter.com/nixcraft), [Facebook](https://facebook.com/nixcraft), [Google+](https://plus.google.com/+CybercitiBiz). Get the **latest tutorials on SysAdmin, Linux/Unix and open source topics via [my RSS/XML feed](https://www.cyberciti.biz/atom/atom.xml)**.