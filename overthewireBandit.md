# [Overthewire/Bandit Walkthru](https://overthewire.org/wargames/bandit/)

I feel that OTW/Bandit is one of the best places to start to learn linux and some basic hacking tactics. You learn
- accessing files
- directory navigation
- file searching
- basic decryption
- decompression
- remote access
- network scanning
- permissions
- reverse shell
- setuid
- cronjobs
- basic brute forcing
- github basics

### Bandit0  
 cat readme -- cat is short for concatenate - Concatenate files and print standard output to the screen  
boJ9jbbUNNfktd78OOpsqOltutMc3MY1   
   
### Bandit1  
 cat ./-   -- ./ is used to tell the shell to read the dash as text instead of a parameter  
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9  
   
### Bandit2  
 cat spaces\ in\ this\ filename -- use ./to read spaces as part of the filename  
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK  
   
### Bandit3  
 cd inhere        #opening directory  
 cat .hidden        #print output to screen  
pIwrPrtPN36QITSp3EQaw936yaFoFgAB  
   
### Bandit4  
 find . -type f | xargs file  
= find(find) in current directory(.) with file type (type) f(f) and pipe that output into xargs that executes file command  
   
Also works  
 file ./-*  
koReBOKuIDDepwhWk7jZC0RTdopnAYKh  
   
### Bandit5  
 find . -type f -size 1033c ! -executable | xargs file  
= find(find) in this directory(.) a file (type) f(f) with the size 1033(1033c) bytes not (!) executable(-) and send input to xargs that executes the file command  
DXjZPULLxYr17uwoI01bNLQbtFemEgo7  
   
Also works  
 find . -type f -exec du -b {} \; | grep 1033  
{} are a placeholder for the file path  
escaping ; and passing it to find command so your shell won't interpret it  
   
Or  
 find -size 1033c  
   
   
### Bandit6  
 find / -user bandit7 -group bandit6 -size 33c   
 find(find) on this system (/) a file owner by user bandit7 (-user bandit7) and group bandit6 (-group bandit6) and 33 bytes in size (-ize 33c)  
   
Also add 2>/dev/null to filter out all 'Permission denied' off the screen  
   
### Bandit7  
 strings data.txt | grep millionth  
 = strings(prints strings of printable characters in files) data.txt(the file) | and sends input to grep(prints lines matching a pattern) millionth(the pattern we are looking for.  
cvX2JJa4CFALtqS87jk27qwqGhBM9plV  
   
### Bandit8  
 sort data.txt | uniq -c  
 = sort(sorts lines of text files) data.txt(the file) | sends input to uniq(finds or omits uniq strings)  
 -c (counts them)  
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR  
   
Sort data.txt | uniq -u  
= sort(sorts lines of text files) data.txt(the file) | sends input to uniq(finds or omits uniq strings)  
 -u (find only unique line)  
   
   
### Bandit9  
 strings data.txt | grep "=="  
 = strings(prints strings of printable characters in files) data.txt(the file) | sending input to grep(prints lines matching pattern) "=="  
truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk  
   
### Bandit10  
 cat data.txt | base64 -d  
 = cat(concatenate/print file) data.txt(file) | send input to base64(base64 encryption) -d(decode)  
IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR  
   
### Bandit11 - no linux based rot13 cipher  
 cat data.txt  
= concatenate data.txt  
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh  
Google rot13 decode  
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu  
   
Or script a quick rot13 cypher where for aach a-z it would rotate to n-z then a-m  
cat data.txt | tr a-zA-Z n-za-mN-ZA-M  
  
   
### Bandit12 -  
 gzip, bzip2, tar, xxd  
 mkdir /tmp/theo  
 cp data.txt /tmp/theo  
 cd tmp/theo  
 xxd -r data.txt > data  
 mv data file.gz  
 gzip -d file.gz  
 mv file file.bz2  
 bzip -d fileb.bz2  
 mv file file.gz  
 gzip - d file.gz  
 mv file file.tar  
 tar xf file.tar  
 rm file.tar  
 rm data.txt  
 mv data5.bin data.tar  
 tar xf data.tar  
 mv data6.bin data.bz2  
 bzip2 -d data.bz2  
 mv data data.tar  
 tar xf data.tar  
 mv data8.bin data.gz  
 gzip -d data.gz  
keep unzipping and changing extensions to match what the file uncompresses into  
ends at data8  
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL  
   
### Bandit 13  
 use ssh key located on bandit13 to access bandit14 as bandit14 and locate key at  
**/etc/bandit_pass/bandit14**  
 ssh -i sshkey.private bandit14@localhost  
=ssh(remote login client) -i(identity file) sshkey.private(rsa key file) bandit14@localhost(user@host ip)  
 cat /etc/bandit_pass/bandit14  
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e  
   
### Bandit14  
Use password 13-14 on port 30000 on localhost  
 nc localhost 30000  
=nc(netcat) localhost(host ip) 30000(port)  
 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e (current level password)  
BfMYroe26WYalil77FoDi9qh59eK5xNr  
   
### Bandit15  
Use password 14-15 on port 30001 on locahost using ssl encryption  
 ncat --ssl localhost 30001  
=ncat(netcat) --ssl(use ssl encryption) localhost(ip address) 30001(port addr)  
BfMYroe26WYalil77FoDi9qh59eK5xNr(current level password)  
Also works  
 openssl s_client -connect localhost:30001  
 openssl(openssl command)  
cluFn7wTiGryunymYOu4RcffSxQluehd  
   
### Bandit16  
 nmap localhost -p 31000-32000  
=nmap(invoke nmap) localhost(on this host ip) -p(port scan) 31000-32000(these ports)  
   
 nmap -sV -p 31000-32000 localhost  
=nmap(invoke nmap) -sV(parameter for service) -p(port scan) 31000-32000(these ports) localhost(on this ip)  
   
 ncat --ssl localhost 31790  
=ncat(netcat) --ssl(use ssl encryption) localhost(ip addr) 31790(port)  
=ncat(netcat) --ssl(search for port speaking ssl) localhost(on this host ip) 31790(this port)  
   
 nmap -sV -p 31000-32000 localhost  
=nmap(invoke nmap) -sV(parameter for service) -p(port scan) 31000-32000(these ports) localhost(on this ip)  
   
 copy rsa private -BEGIN to END- , save to /tmp on bandit16 by using  
 touch key2.txt  
 echo "copied rsa private key, beginning to end" > key2.txt  
   
 chmod key2.txt 600  
=chmod(change permissions) key2.txt(identity/key file) 600(user=read, write, group/other=none)  
[https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x9543.htm](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x9543.htm)  
   
 ssh -i key2.txt bandit17@localhost  
=ssh(remote login client) -i(identity file) key2.txt(rsa key file) bandit17@localhost(user@host ip)  
   
or  
 copy rsa private -BEGIN to END- , save to desktop as key17  
 ssh -i key17 bandit17@bandit.labs.overthewire.org -p 2220  
 =ssh(remote login client) -i(identity file) key17(file where rsa key located) bandit17@bandit.labs.overthewire.org(username@ip addr) -p(port) 2220(port #)  
   
### Bandit17  
 diff -y passwords.new passwords.old  
 =diff(command that compares files line by line) -y(output in 2 columns) passwords.new(file1) passwords.old(file2)  
Or diff passwords.new passwords.old  
kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd  
   
### Bandit18  
Exit bandit17  
Exit bandit16  
 man ssh | grep terminal  
 -t Force pseudo-terminal allocation  
  ssh -t bandit18@bandit.labs.overthewire.org -p 2220 /bin/sh  
 or  
 ssh -t bandit18@localhost /bin/sh  
 =ssh(remote login client) -t(force pseudo terminal) bandit18@bandit.labs.overthewire.org(user@host ip) -p(port) 2220(port #) /bin/sh(?)  
 shell access  
 ls  
 cat readme  
[https://www.akashtrehan.com/writeups/OverTheWire/Bandit/level18/](https://www.akashtrehan.com/writeups/OverTheWire/Bandit/level18/)  
OR  
ssh -t bandit18@bandit.labs.overthewire.org -p 2220 "cat ~/readme"  
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x  
   
OR  
 ssh bandit18@localhost /bin/sh  
   
### Bandit19  
 ./bandit20-do --> use this file to run commands as bandit20  
=set relative path to local directory with ./  
 ./bandit20-do cat /etc/bandit_pass/bandit20  
 =./(set relative path to local directory with)bandit20-do(setuid binary) cat(print to screen) /etc/bandit_pass/bandit20(filename)  
GbKksEFF4yrVs6il55v6gwY5aVje5f0j  
   
### Bandit20 - [https://www.jonyschats.nl/writeups/bandit-level-20-to-21/](https://www.jonyschats.nl/writeups/bandit-level-20-to-21/)  
You need 2 ssh sessions open - $ssh bandit20@bandit.labs.overthewire.org -p 2220  
#1 to nc into a specific port  
#2 to run ./suconnect on the specific port  
   
#2 ssh  
 echo GbKksEFF4yrVs6il55v6gwY5aVje5f0j | nc -l localhost -p 54321  
   
#1  
 ./suconnect 54321  
   
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr  
   
### Bandit21 -   
 cd/etc/cron.d  
 cat cronjob_bandit22  
 cat /usr/bin/cronjob_bandit22.sh  
 cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv  
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI  
   
### Bandit22 -  
 cd /etc/cron.d  
 cat cronjoib_bandit23  
 cat /usr/bin/cronjob_bandit23.sh  
   
'''  
#!/bin/bash  
   
myname=$(whoami)  
=bandit22  
   
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)  
=  
   
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"  
'''  
   
 whoami = bandit22  
 echo I am user bandit23 |md5sum  
  8ca319486bfbbc3663ea0fbe81326349  
 cat /tmp/8ca319486bfbbc3663ea0fbe81326349  
   
     
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n  
   
### Bandit23  
*cronjob runs as bandit24, enumerates through files in /var/spool/bandit24, if the file owner is bandit23 (created by your current user), it will run it*
 mkdir /tmp/theo  
Make directory /tmp/theo  
 cd /tmp/theo  
Change into directory /tmp/theo  
 nano bandit24  
Create file bandit24  
 --save the below into bandit24  
'''  
#!/bin/bash  
cat /etc/bandit_pass/$myname > /tmp/theo/bandit24.txt  
'''  
 chmod 777 bandit24.sh  
Change permissions of the file bandit24.sh to 777 (rwx for all)  
 chmod 777 /tmp/theo  
Change permissions of the directory /tmp/theo to 777 (rwx for all)  
 cp bandit24.sh /var/spool  
Check level24 file for  password  
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ  
   
### Bandit 24  
   
Create script to  
Declare bandit24 Password as UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ  
iterate through 0000-9999 pins  
And echo  UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ + pins  
   
#!/bin/bash  
pass24="UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"  
for p in {0000..5000}  
do  
echo $pass24' '$p  
done  
   
$ ./brute | nc localhost 30002  
   
 uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG  
   
### Bandit 25  
   
ssh bandit26@localhost -I bandit26.sshkey  
Gets us booted upon entry  
 cd /etc  
 cat passwd  
/home/bandit26:/usr/bin/showtext -- Funny looking file ending in showtext  
 cat  /usr/bin/showtext  
   
#!/bin/sh  
   
export TERM=linux  
   
more ~/text.txt  
exit 0  
   
 ssh bandit26@localhost -I bandit26.sshkey  
Shrink terminal to 4 lines  
 enter  
 v -- to enter vi interface  
 enter  
 :set shell=/bin/bash -- to set bash shell?  
 enter  
 :sh -- to enter shell  
 enter  
 now in Bandit26  
   
### Bandit 26  
   
Grab bandit27 password from etc with bandit27 setuid  
   
 ./bandit27-do cat /etc/bandit_pass/bandit27  
   
 3ba3118a22e93127a4ed485be72ef5ea  
   
### Bandit 27  
   
 cd /tmp  
 git clone ssh://bandit27-git@localhost/home/bandit27-git/repo  
 cat README  
   
 0ef186ac70e04ea33b4c1853d2526fa2  
   
### Bandit28  
   
 git clone ssh://bandit28-git@localhost/home/bandit28-git/repo  
--> Clone git repo  
 cd repo  
 cat README.md  
 git log  
--> view logs  
 git show edd935d60906b33f0619605abd1689808ccdd5ee  
--> show specific log  
   
 bbc96594b4e001778eee9975372716b2  
   
### Bandit 29  
   
 git clone ssh://bandit29-git@localhost/home/bandit29-git/repo  
--> Clone git repo  
 cd repo  
 cat README.md  
 git log  
--> view logs  
 git show 208f463b5b3992906eabf23c562eda3277fea912  
--> show commit for specific log  
 git branch -a  
--> show branch from a  
 git checkout dev  
--> show dev branch  
 cat README.md  
   
 5b90576bedb2cc04c86a9e924ce42faf  
   
### Bandit 30  
   
 git clone ssh://bandit30-git@localhost/home/bandit30-git/repo  
--> Clone git repo  
 cd repo  
 cat README.md  
 git tag  
Show tags created in repository history  
 git show secret  
Show contents of git tag  
   
 47e603bb428404d265f59c42920d81e5  
   
### Bandit 31  
   
 git clone ssh://bandit31-git@localhost/home/bandit31-git/repo  
--> Clone git repo  
 cd repo  
 cat README.md  
Directions to push a file to the remote repository called key.txt with 'May I come in?' text  
 nano key.txt  
 May I come in? --> save in file  
   
 git add -f key.txt  
Add the text file to the repository  
 git commit -m "."  
Commit the entry  
 git push origin  
Push it into the Origin branch  
   
 56a9bf19c63d650ce78e6ec0354ee45e  
   
### Bandit 32  
   
Escape the uppercase shell  
 $0  
Escapes uppercase shell using an escape character ‘$0’  
   
 ls -al  
Shows all files in directory  
 cat /etc/bandit_pass/bandit33  
   
 c9c3199ddf4121b10cf581a98d51caee  
   
Bandit33
