---
published: false
---
I'm writing this post just as a quick note to save somewhere the steps to follow in order to get connected to a remote SSH server without have to enter a user password for each connection. 

I came across this when started using the Remote-SSH extension for Visual Studio Code, then for each modification I was asked to enter a password!  

In the following example, I'm connecting from a Windows 10 as a Client, to Ubuntu as SSH Server:

```
C:\Users\user>ssh-keygen -t rsa
Generating public/private rsa key pair.
```

after the execution of the command above `ssh-keygen` you're asked to choose a file where to save the rsa key (I used the default one by pressing Enter). The same thing for `passphrase`, just tape enter to use empty passphrase if you're using a local environment.

```
Enter file in which to save the key (C:\Users\user/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

If they key is generated successfully, you get something like the following response:

```
Your identification has been saved in C:\Users\user/.ssh/id_rsa.
Your public key has been saved in C:\Users\user/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:wjB7gpc9icYrRV9a8ABZcAcENeKO8/XFoEilne7e838 domain\admin@sshclient
The key's randomart image is:
+---[RSA 2048]----+
|  =OB.. .        |
| ..o+o + +       |
|  +  ++ + o      |
| o.o o++ o       |
| ...+++ S        |
|  . o+ o         |
| + o..  .        |
|o B +. . ..     E|
| +.o... . .o.... |
+----[SHA256]-----+
```

Once the key is generated, we need now to save the public key in Autorized Keys of the remote SSH server. 

Execute the following command to create the folder `.ssh` using SSH: 
```
C:\Users\user>ssh user@sshserver mkdir -p .ssh
user@sshserver's password:
```

now, because I'm using Windows, I just copy past the content of the generated file `c:\users\user\id_rsa.pub` to the remote file `~/.ssh/autorized_keys`  

If you're using Linux as a client, you have just to use the awesome command `cat` to "copy/past" from command line: 

```
user@sshclient:~> cat .ssh/id_rsa.pub | ssh user@sshserver 'cat >> .ssh/authorized_keys'
user@sshserver's password: 
```

now, if all is fine, when you try to connect from SSH command line, you'll not be asked for the password anymore: 

```
C:\Users\user>ssh user@sshserver
Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.4.0-37-generic x86_64)

Last login: Mon Jun 15 07:29:16 2020 from 192.168.1.10
user@sshserver:~$ 
```

That's all! 


