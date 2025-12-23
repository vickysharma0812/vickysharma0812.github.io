---
title: 'Simple Secure Shell (SSH)'
author: Vikas Sharma, Ph.D.
date: 30 Oct 2021
tags: [SSH, linux-server]
summary: This note explains how to establish the SSH connection between a server and client.
---

SSH stands for simple secured shell. The ssh command contains of 3-parts

OpenSSH provides a server daemon and client tools to facilitate secure remote control and file transfer operation.

Install openssh by using 

```bash
sudo apt install openssh-client openssh-server
```

## OpenSSH Client-Side

OpenSSH provides several client tools to facilitate secure remote control and file transfer operation. Install `openssh` using following command.

```bash
sudo apt install openssh-client
```

OpenSSH has a client side component, it is called `ssh`, which will connect a client to the server.

```bash
ssh {user}@{host}
```

Here `user` is the name of the account that you want to access and `host` is the `IP address` or the `Domain name` of the server.

We want to access the server by using the ssh-key.

**Generating RSA key pair** on client.

Use the `ssh-keygen` CLT for creating RSA key pair on the **client** machine (your local computer).

```bash
ssh-keygen -t rsa
```

Just follow the instruction given in the terminal.

> The key will be stored at `~/.ssh`

If you overwrite the previously generated RSA key, then the applications which use that key will not work properly. Therefore, I always name the RSA key according to the purpose of generating it.

```text
|-- config
|-- config_bk
|-- easifem_dev_rsa
|-- easifem_dev_rsa.pub
|-- github_easifem_rsa
|-- github_easifem_rsa.pub
|-- id_rsa
|-- id_rsa.pub
|-- known_hosts
```

Every time we generate RSA key, we get two files named `XXX_rsa` and `XXX_rsa.pub`. The former is a private key, and the latter is a public key.

**Placing public key to hosting server**

The easiest way to copy your public key from client the hosting server is to use a CLT called `ssh-copy-id`.

In this method, we need to specify the remote server that we would like to connect to.  Therefore, in this method we should have the credentials to access the server. The syntax is

```bash
ssh-copy-id username@remote_host
```

Subsequently, follow the instruction on the screen. This process will copy the content of `id_rsa.pub` to the remote server at `~/.ssh/authorized_keys`.  After this step you will be able to access the remote server using

```bash
ssh username@remote_host -p PORT_NUMBER
```

If you do not `ssh-copy-id` then use the following process to copy the content of `id_rsa.pub` from local machine (client) to the remote server's `~/.ssh/authorized_keys`.

```bash
cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Lastly, if you do not have access to remote, then you have to manually copy the content of `id_rsa.pub` from client to `authorized_keys` of remote server.

Make sure that on the server side `~/.ssh` and `authorized_keys` have correct permission set:

```bash
chmod -R go ~/.ssh
```

**ssh-configuration**

In `~/.ssh` directory you will see a file named `config`, if this file is not present then create it. Then open it in a text editor and add following lines to it.

```bash
# connecting to my ubuntu-server
Host linux
  HostName 192.168.1.15
  User vikassharma
  Port 2222
  IdentityFile ~/.ssh/easifem_linux_rsa
```

Now we can connect to the server using `ssh linux`.

There are several ways to define IP in hostname

- `192.168.1.*` matches `192.168.1.0` to `192.168.1.24`
- `192.168.1.?` matches excatly one character, i.e. `192.168.1.0` to `192.168.1.9`.

## OpenSSH Server-side

OpenSSH provides a server daemon and client tools to facilitate secure remote control and file transfer operation. The server component is called `sshd` (d for daemon) which listens continuously for client connections from any of the client tools.

To **install** `sshd` we need to install `openssh-server` on the server.

```bash
sudo apt install openssh-server
```

**CONFIGURATION** file is located `/etc/ssh/sshd_config`. Note that there are many directives in the `sshd_config` file. Before editing this file make a copy of `sshd_config`.


```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bk
sudo chmod a-w /etc/ssh/sshd_config.bk
```

Now check the configuration file before restarting ssh.

```
sudo sshd -t -f /etc/ssh/sshd_config
```

**LISTEN TO THE PORT** `sshd` by default listens to the TCP port 22. To change this default setting search for `PORT` in `sshd_config` file. 

```
Port 2222
```


**Banner**

```
Banner /etc/issue.net
```

Read more about banner [here](https://www.tecmint.com/ssh-warning-banner-linux/).


**Activating modifications**

```
sudo systemclt status ssh
sudo systemclt restart sshd.service
sudo ufw allow ssh
sudo systemclt enable ssh
```

**Stop and disable ssh**

```
sudo systemctl stop ssh
```

This will stop the service until you restart it or until the system rebooted. To restart it you can type

```
sudo systemctl start ssh
```

If you want to disable it from starting during system boot, use

```
sudo systemctl disable ssh
```

This will not stop the service from running during the current session, just from loading during startup. If you want to start again during system boot, type:

```
sudo systemctl enable ssh
```

**Getting IP address**

```
ip address
```

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp3s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 2c:d4:44:ae:a1:3a brd ff:ff:ff:ff:ff:ff
3: wlp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether c0:d9:62:0b:c2:02 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.15/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp4s0
       valid_lft 64284sec preferred_lft 64284sec
    inet6 fe80::f53a:7745:52fc:1573/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

The ip-address of my system is inet `192.168.1.15`. In this way, from the client side we will use `ssh vikassharma@192.168.1.15` to connect to the remote server.
