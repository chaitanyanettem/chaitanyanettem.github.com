---
layout: post
title: Passwordless SSH
date: 2014-02-24 09:23
permalink: passwordless-ssh
summary: A tutorial on ssh-keygen
categories: tutorial ssh
---

If you're anything like me then you constantly have to SSH into other machines to do various things ranging from website maintenance to development to homework submission. Mostly you're SSHing into the same 3-4 machines. Entering passwords again and again is a pain when you are doing that.

Enter ssh-keygen to the rescue. ssh-keygen 'generates, manages and converts authentication keys for ssh'. For the standard usecase of generating a key and using it for sshing into all machines, this is the workflow:

- You enter ssh-keygen at a prompt and then hit enter for all prompts. 

- If ssh-keygen prompts you to confirm overwriting a previously created key then you can go ahead and overwrite it (as long as you know the consequences of overwriting: you will have to enter the passwords again for all the machines that you configured the previous key with). 

- If you do overwrite a previously existing key then you might have to run ssh-add to link the key with your user.

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/chaitanya/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/chaitanya/.ssh/id_rsa.
Your public key has been saved in /home/chaitanya/.ssh/id_rsa.pub.
```

Next you will copy the generated key to each remote machine like so:

```
$ ssh-copy-id <username>@<remote machine's address>
```

And you're done. You can now logon to the remote machine without entering a password so long as the key remains unchanged in your home system. 

You should read the following resources for more information:

- [ssh-keygen man page](http://linux.die.net/man/1/ssh-keygen)
- [Common error resolved using ssh-add] (https://help.github.com/articles/error-agent-admitted-failure-to-sign)