*   [Home][1]
*   [Disclaimer][2]
*   [Contact][3]
*   [Archives][4]
*   [About][5]
*   [Subscribe][6]
*   [Support][7]
*   [Advertise][8]
*    
    

[Kernel Talks][9]

Unix, Linux & scripts.

 

*   [How-to guides][10]
    *   [Howto][11]
    *   [Disk management][12]
    *   [Configurations][13]
*   [OS][14]
    *   [HPUX][15]
    *   [Linux][16]
*   [Commands & tools][17]
    *   [Commands][18]
    *   [Software & Tools][19]
    *   [System services][20]
*   [Cloud computing][21]
    *   [AWS CSA associate quiz][22]
    *   [AWS CSA preparation guide!][23]
    *   [Cloud Services][24]
*   [Tips & Tricks][25]
*   [Linux commands][26]

You are here: [Home][27] / [Tips & Tricks][28]

How to configure login banners in Linux (RedHat, Ubuntu, CentOS, Fedora)
========================================================================

Published: November 10, 2017 | Modified: November 10, 2017 | 1062 views

*   [0][31]

*   [0][35]
*   [0][36]
*   shares

---

_Learn how to create login banners in Linux to display different warning or information messages to user who is about to log in or after he logs in._

![Login banners in Linux](https://a3.kerneltalks.com/wp-content/uploads/2017/11/login-banner-message-in-linux.png)

Login banner messages in Linux

---

Whenever you login to some production systems of firm, you get to see some login messages, warnings or info about server you are about to login or already logged in like below. Those are the login banners.

![Login welcome messages in Linux](https://a3.kerneltalks.com/wp-content/uploads/2017/11/Login-message-in-linux.png)

Login welcome messages in Linux

In this article we will walk you through how to configure them.

There are two types of banners you can configure.

1.  Banner message to display before user log in (configure in file of your choice eg. `/etc/login.warn`)
2.  Banner message to display after user successfully logged in (configure in `/etc/motd`)

---

### How to display message when user connects to system before login

This message will be displayed to user when he connects to server and before he logged in. Means when he enter the username, this message will be displayed before password prompt.

You can use any filename and enter your message within. Here we used `/etc/login.warn` file and put our messages inside.

Shell

\# cat /etc/login.warn !!!! Welcome to KernelTalks test server !!!! This server is meant for testing Linux commands and tools. If you are not associated with kerneltalks.com and not authorized please dis-connect immediately.

1

2

3

4

5

6

7

\# cat /etc/login.warn

!!!!  Welcome to  KernelTalks test  server  !!!!

This  server is  meant for  testing Linux commands and  tools.  If  you are

not  associated with kerneltalks.com  and  not  authorized please dis-connect

immediately.

Now, you need to supply this file and path to `sshd` daemon so that it can fetch this banner for each user login request. For that open `/etc/sshd/sshd_config` file and search for line `#Banner none`

Here you have to edit file and write your filename and remove hash mark. It should look like : `Banner /etc/login.warn`

Save file and restart `sshd` daemon. To avoid disconnecting existing connected users, use HUP signal to restart sshd.

Shell

root@kerneltalks # ps -ef |grep -i sshd root 14255 1 0 18:42 ? 00:00:00 /usr/sbin/sshd -D root 19074 14255 0 18:46 ? 00:00:00 sshd: ec2-user \[priv\] root 19177 19127 0 18:54 pts/0 00:00:00 grep -i sshd root@kerneltalks # kill -HUP 14255

1

2

3

4

5

6

7

8

root@kerneltalks  \# ps -ef |grep -i sshd

root 14255 10  18:42  ?00:00:00  /usr/sbin/sshd  -D

root 19074  142550  18:46  ?00:00:00  sshd:  ec2-user  \[priv\]

root 19177  191270  18:54  pts/000:00:00  grep  -i  sshd

root@kerneltalks  \# kill -HUP 14255

Thats it! Open new session and try login. You will be greeted with the message you configured in above steps .

![Login banner in Linux](https://a1.kerneltalks.com/wp-content/uploads/2017/11/login-banner.png)

Login banner in Linux

You can see message is displayed before user enter his password and log in to system.

---

### How to display message after user logs in

Message user sees after he logs into system successfully is **M**essage **O**f **T**he **D**ay & is controlled by `/etc/motd` file. Edit this file and enter message you want to greet user with once he successfully logged in.

Shell

root@kerneltalks # cat /etc/motd W E L C O M E Welcome to the testing environment of kerneltalks. Feel free to use this system for testing your Linux skills. In case of any issues reach out to admin at info@kerneltalks.com. Thank you.

1

2

3

4

5

6

7

8

root@kerneltalks  \# cat /etc/motd

 W  E  L  C  O  M  E

Welcome to  the testing environment of kerneltalks.

Feel free to  use  this  system for  testing your Linux

skills.  In  case  of any issues reach out to  admin at

info@kerneltalks.com.  Thank you.

You dont need to restart `sshd` daemon to take this change effect. As soon as you save the file, its content will be read and displayed by sshd daemon from very next login request it serves.

![motd in linux](https://a3.kerneltalks.com/wp-content/uploads/2017/11/motd-message-in-linux.png)

Message Of The Day

You can see in above screenshot : Yellow box is MOTD controlled by `/etc/motd` and green box is what we saw earlier [login banner][37].

You can use tools like [cowsay][38], [banner][39], [figlet][40], [lolcat ][41]to create fancy, eye-catching messages to display at login. This method works on almost all Linux distros like RedHat, CentOs, Ubuntu, Fedora etc.

---

*   [0][44]

*   [0][48]
*   [0][49]
*   shares

⇠ Previous article [All you need to know about sosreport tool][50]

Next article ⇢ [How to change timezone in Linux server (RedHat, CentOS, Ubuntu)][51]

### Related stuff:

*   [Hollywood movie MATRIX like desktop in Linux terminal][52]
*   [How to list open ports on Linux/Unix server][53]
*   [Run command on multiple linux servers from windows][54]
*   [How to get directory size in Linux][55]
*   [How to save PuTTY session output automatically][56]
*   [How to test internet speed in Linux terminal][57]
*   [3 tricks to get multiple commands output in same row][58]
*   [Cowsay : Fun in Linux terminal][59]
*   [8 ways to generate random password in Linux][60]
*   [Create beautiful ASCII text banners in Linux][61]
*   [4 tools to download any file using command line in Linux][62]

Filed Under: [Tips & Tricks][63] Tagged With: [login banners][64], [login banners in linux][65], [ssh login banners][66]

#### If you like my tutorials and if they helped you in any way, then

*   Consider buying me [a cup of coffee via paypal][67]!
*   Subscribe to our newsletter [here][68]!
*   Like KernelTalks [Facebook page][69].
*   Follow us on [Twitter][70].
*   Follow our [Google+ page][71].
*   Add our [RSS feed][72] to your feed reader.

### Share Your Comments & Feedback: [Cancel reply][73]

Comment

Name * 

Email * 

Website 

  

Join group of 8,909 Talkers!

*   [
    
    6.4kFans
    
    ][74]
*   [
    
    1.9kFollowers
    
    ][75]
*   [
    
    45Followers
    
    ][76]
*   [
    
    154Followers
    
    ][77]
*   [
    
    323Subscribers
    
    ][78]
*   [
    
    46Subscribers
    
    ][79]

#### Popular posts

*   [How to resolve mount.nfs: Stale file handle error][80]
*   [mount.nfs: requested NFS version or transport protocol is not supported][81]
*   [How to check if package is installed on Linux][82]
*   [Process states in Linux][83]
*   [4 ways to check size of physical memory (RAM) in Linux][84]
*   [How to configure NTP client in Linux][85]
*   [How to establish passwordless ssh between two servers][86]
*   [How to resolve aclocal: not found error in Ubuntu][87]
*   [pvcreate error: Device /dev/xyz not found (or ignored by filtering).][88]
*   [How to open file in read only mode under vi or vim][89]

### Get Linux & Unix stuff right into your mailbox

Join with other **308** subscribers to get our weekly newsletter in your inbox. Its FREE and you can unsubscribe at anytime!

This work is licensed under a [CC-BY-NC][90] license. © Copyright 2016-2017 [KernelTalks][91] · All Rights Reserved. The content is copyrighted to Shrikant Lavhate & can not be reproduced either online or offline without prior permission.

*   [How to check and test APA in HPUX][92]
*   [Highest size files in mount point][93]
*   [Auto port aggregation APA configuration in HPUX][94]
*   [LVM cheatsheet][95]
*   [Difference between tmpfs and swap][96]
*   [xsos : a tool to read sosreport in RHEL/CentOS][97]
*   [AWS CloudFront, SNS, SQS revision before CSA exam][98]
*   [Hyperthreading in HPUX][99]
*   [Difference between LVM and LVM2 : Linux interview question explained][100]
*   [How to create RAM disk in Linux][101]

Send this to a friend

Your emailRecipient email

SendCancel

---

via: [https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/][102]

作者: [null][103] 选题者: [@chounanzi][104] 译者: [译者ID][105] 校对: [校对者ID][106]

本文由 [LCTT][107] 原创编译，[Linux中国][108] 荣誉推出

[1]: https://kerneltalks.com/
[2]: https://kerneltalks.com/disclaimer/
[3]: https://kerneltalks.com/contact/
[4]: https://kerneltalks.com/archives/
[5]: https://kerneltalks.com/about/
[6]: https://kerneltalks.com/subscribe/
[7]: https://kerneltalks.com/buy-me-coffee/
[8]: https://kerneltalks.com/advertise/
[9]: https://kerneltalks.com/
[10]: https://kerneltalks.com/#
[11]: https://kerneltalks.com/category/howto/
[12]: https://kerneltalks.com/category/disk-management/
[13]: https://kerneltalks.com/category/config/
[14]: https://kerneltalks.com/#
[15]: https://kerneltalks.com/category/hpux/
[16]: https://kerneltalks.com/category/linux/
[17]: https://kerneltalks.com/#
[18]: https://kerneltalks.com/category/commands/
[19]: https://kerneltalks.com/category/tools/
[20]: https://kerneltalks.com/category/services/
[21]: https://kerneltalks.com/#
[22]: https://kerneltalks.com/cloud-services/aws-csa-associate-quiz/
[23]: https://kerneltalks.com/virtualization/complete-aws-csa-associate-preparation-guide/
[24]: https://kerneltalks.com/category/cloud-services/
[25]: https://kerneltalks.com/category/tips-tricks/
[26]: https://kerneltalks.com/useful-linux-commands-for-beginners/
[27]: https://kerneltalks.com/
[28]: https://kerneltalks.com/category/tips-tricks/
[29]: https://www.facebook.com/sharer/sharer.php?u=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/&t=How+to+configure+login+banners+in+Linux+%28RedHat%2C+Ubuntu%2C+CentOS%2C+Fedora%29&redirect_uri=https://kerneltalks.com?sharing-thankyou=yes
[30]: https://kerneltalks.com/#
[31]: https://plus.google.com/share?url=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[32]: https://kerneltalks.com/#
[33]: https://www.linkedin.com/shareArticle?mini=true&ro=true&trk=EasySocialShareButtons&title=How+to+configure+login+banners+in+Linux+%28RedHat%2C+Ubuntu%2C+CentOS%2C+Fedora%29&url=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[34]: http://www.stumbleupon.com/badge/?url=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[35]: https://kerneltalks.com/#
[36]: https://kerneltalks.com/#
[37]: https://kerneltalks.com/#banner
[38]: https://kerneltalks.com/tips-tricks/cowsay-fun-in-linux-terminal/
[39]: https://kerneltalks.com/howto/create-nice-text-banner-hpux/
[40]: https://kerneltalks.com/tips-tricks/create-beautiful-ascii-text-banners-linux/
[41]: https://kerneltalks.com/linux/lolcat-tool-to-rainbow-color-linux-terminal/
[42]: https://www.facebook.com/sharer/sharer.php?u=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/&t=How+to+configure+login+banners+in+Linux+%28RedHat%2C+Ubuntu%2C+CentOS%2C+Fedora%29&redirect_uri=https://kerneltalks.com?sharing-thankyou=yes
[43]: https://kerneltalks.com/#
[44]: https://plus.google.com/share?url=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[45]: https://kerneltalks.com/#
[46]: https://www.linkedin.com/shareArticle?mini=true&ro=true&trk=EasySocialShareButtons&title=How+to+configure+login+banners+in+Linux+%28RedHat%2C+Ubuntu%2C+CentOS%2C+Fedora%29&url=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[47]: http://www.stumbleupon.com/badge/?url=https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[48]: https://kerneltalks.com/#
[49]: https://kerneltalks.com/#
[50]: https://kerneltalks.com/tools/all-you-need-to-know-about-sosreport/
[51]: https://kerneltalks.com/howto/how-to-change-timezone-in-linux-server/
[52]: https://kerneltalks.com/tips-tricks/hollywood-movie-matrix-like-desktop-linux-terminal/ "Link to Hollywood movie MATRIX like desktop in Linux terminal"
[53]: https://kerneltalks.com/tips-tricks/list-open-ports-linux-server/ "Link to How to list open ports on Linux/Unix server"
[54]: https://kerneltalks.com/howto/run-command-on-multiple-linux-servers-from-windows/ "Link to Run command on multiple linux servers from windows"
[55]: https://kerneltalks.com/howto/howto-get-directory-size-linux/ "Link to How to get directory size in Linux"
[56]: https://kerneltalks.com/tips-tricks/how-to-save-putty-session-output-automatically/ "Link to How to save PuTTY session output automatically"
[57]: https://kerneltalks.com/tips-tricks/how-to-test-internet-speed-in-linux-terminal/ "Link to How to test internet speed in Linux terminal"
[58]: https://kerneltalks.com/scripts/3-ways-get-multiple-commands-output-row/ "Link to 3 tricks to get multiple commands output in same row"
[59]: https://kerneltalks.com/tips-tricks/cowsay-fun-in-linux-terminal/ "Link to Cowsay : Fun in Linux terminal"
[60]: https://kerneltalks.com/tips-tricks/8-ways-to-generate-random-password-in-linux/ "Link to 8 ways to generate random password in Linux"
[61]: https://kerneltalks.com/tips-tricks/create-beautiful-ascii-text-banners-linux/ "Link to Create beautiful ASCII text banners in Linux"
[62]: https://kerneltalks.com/tips-tricks/4-tools-download-file-using-command-line-linux/ "Link to 4 tools to download any file using command line in Linux"
[63]: https://kerneltalks.com/category/tips-tricks/
[64]: https://kerneltalks.com/tag/login-banners/
[65]: https://kerneltalks.com/tag/login-banners-in-linux/
[66]: https://kerneltalks.com/tag/ssh-login-banners/
[67]: https://kerneltalks.com/buy-me-coffee/
[68]: https://eepurl.com/cDSMhj
[69]: https://www.facebook.com/kerneltalks
[70]: https://twitter.com/@kerneltalks
[71]: https://plus.google.com/b/115086199909589647244/115086199909589647244
[72]: https://feeds.feedburner.com/kerneltalks
[73]: https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/#respond
[74]: https://www.facebook.com/kerneltalks
[75]: https://www.twitter.com/kerneltalks
[76]: https://plus.google.com/+KernelTalks
[77]: https://www.pinterest.com/lensedin
[78]: https://eepurl.com/cDSMhj
[79]: https://feeds.feedburner.com/kerneltalks
[80]: https://kerneltalks.com/troubleshooting/resolve-mount-nfs-stale-file-handle-error/
[81]: https://kerneltalks.com/troubleshooting/mount-nfs-requested-nfs-version-or-transport-protocol-is-not-supported/
[82]: https://kerneltalks.com/tools/check-package-installed-linux/
[83]: https://kerneltalks.com/linux/process-states-in-linux/
[84]: https://kerneltalks.com/linux/4-ways-to-check-size-of-physical-memory-in-linux/
[85]: https://kerneltalks.com/config/how-to-configure-ntp-client-linux/
[86]: https://kerneltalks.com/howto/establish-passwordless-ssh-between-two-servers/
[87]: https://kerneltalks.com/troubleshooting/how-to-resolve-aclocal-not-found-error-in-ubuntu/
[88]: https://kerneltalks.com/troubleshooting/pvcreate-error-device-not-found-or-ignored-by-filtering/
[89]: https://kerneltalks.com/howto/open-file-read-only-mode-vi-vim/
[90]: https://creativecommons.org/licenses/by-nc/4.0/
[91]: https://kerneltalks.com/
[92]: https://kerneltalks.com/howto/check-and-test-apa-in-hpux/
[93]: https://kerneltalks.com/linux/highest-size-files-in-mount-point/
[94]: https://kerneltalks.com/hpux/auto-port-aggregation-apa-configuration-hpux/
[95]: https://kerneltalks.com/disk-management/lvm-cheatsheet/
[96]: https://kerneltalks.com/linux/difference-between-tmpfs-and-swap/
[97]: https://kerneltalks.com/tools/xsos-a-tool-to-read-sosreport/
[98]: https://kerneltalks.com/virtualization/aws-cloudfront-sns-sqs-revision-before-csa-exam/
[99]: https://kerneltalks.com/hardware-config/hyperthreading-in-hpux/
[100]: https://kerneltalks.com/linux/difference-lvm-and-lvm2-linux-interview/
[101]: https://kerneltalks.com/linux/how-to-create-ram-disk-in-linux/
[102]: https://kerneltalks.com/tips-tricks/how-to-configure-login-banners-in-linux/
[103]: undefined
[104]: https://github.com/chounanzi
[105]: https://github.com/译者ID
[106]: https://github.com/校对者ID
[107]: https://github.com/LCTT/TranslateProject
[108]: https://linux.cn/