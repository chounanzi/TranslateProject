How to use lftp to accelerate ftp/https download speed on Linux/UNIX
====================================================================

lftp is a file transfer program. It allows sophisticated FTP, HTTP/HTTPS, and other connections. If the site URL is specified, then lftp will connect to that site otherwise a connection has to be established with the open command. It is an essential tool for all a Linux/Unix command line users. I have already written about [Linux ultra fast command line download accelerator](www.cyberciti.biz//www.cyberciti.biz/tips/download-accelerator-for-linux-command-line-tools.html) such as Axel and prozilla. lftp is another tool for the same job with more features. lftp can handle seven file access methods:

1.  ftp
2.  ftps
3.  http
4.  https
5.  hftp
6.  fish
7.  sftp
8.  file

So what is unique about lftp?
-----------------------------

*   Every operation in lftp is reliable, that is any not fatal error is ignored, and the operation is repeated. So if downloading breaks, it will be restarted from the point automatically. Even if FTP server does not support REST command, lftp will try to retrieve the file from the very beginning until the file is transferred completely.
*   lftp has shell-like command syntax allowing you to launch several commands in parallel in the background.
*   lftp has a builtin mirror which can download or update a whole directory tree. There is also a reverse mirror (mirror -R) which uploads or updates a directory tree on the server. The mirror can also synchronize directories between two remote servers, using FXP if available.

How to use lftp as download accelerator
---------------------------------------

lftp has pget command. It allows you download files in parallel. The syntax is `lftp -e 'pget -n NUM -c url; exit'` For example, download http://kernel.org/pub/linux/kernel/v2.6/linux-2.6.22.2.tar.bz2 file using pget in 5 parts: `$ cd /tmp $ lftp -e 'pget -n 5 -c http://kernel.org/pub/linux/kernel/v2.6/linux-2.6.22.2.tar.bz2'` Sample outputs:

```
45108964 bytes transferred in 57 seconds (775.3K/s)
lftp :~>quit
```

Where,

1.  `pget` – Download files in parallel
2.  `-n 5` – Set maximum number of connections to 5
3.  `-c` – Continue broken transfer if lfile.lftp-pget-status exists in the current directory

How to use lftp to accelerate ftp/https download on Linux/Unix
--------------------------------------------------------------

Another try with added exit command: `$ lftp -e 'pget -n 10 -c https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.15.tar.xz; exit'`

_Sorry, your browser doesn’t support HTML5 video._ HTML 5 Video 01: lftp command in action

A note about parallel downloading
---------------------------------

Please note that by using download accelerator you are going to put a load on remote host. Also note that lftp may not work with sites that do not support multi-source downloads or blocks such requests at firewall level.

NA command offers many other features. Refer to [lftp](https://lftp.yar.ru/) man page for more information: `man lftp`

Posted by: Vivek Gite
---------------------

The author is the creator of nixCraft and a seasoned sysadmin and a trainer for the Linux operating system/Unix shell scripting. He has worked with global clients and in various industries, including IT, education, defense and space research, and the nonprofit sector. Follow him on [Twitter](https://twitter.com/nixcraft), [Facebook](https://facebook.com/nixcraft), [Google+](https://plus.google.com/+CybercitiBiz). Get the **latest tutorials on SysAdmin, Linux/Unix and open source topics via [my RSS/XML feed](https://www.cyberciti.biz/atom/atom.xml)**.

[GOT FEEDBACK? CLICK HERE TO JOIN THE DISCUSSION](https://www.nixcraft.com/)