---
layout: post
title:  Mastering the Hydra
date:  2024-02-02
categories:  [PENTESTING]
tags:  [Penetration Testing, Endpoint Security, Encryption, Cloud Security, Incident Response]
author: Ox1df
image:
 path: assets/img/masteringhydra.png
 alt: Network pentesting
---
## Introuction
Hi there mates Myself 0x1df! i am just a Nerd trying to learn Cyber security stuff
This blog simplifies Hydra, exploring its applications, nuances, and ethical considerations. Whether you're a pro or a newcomer, join us to understand how this tool can enhance your cybersecurity defenses responsibly.
## Table of Contents

1. [Introduction to Hydra](#1-introduction-to-hydra)
2. [Installation](#2-installation)
3. [Basic Syntax](#3-basic-syntax)
    - 3.1 [Single Username/Password Attacks](#31-single-usernamepassword-attacks)
    - 3.2 [Password Spraying](#32-password-spraying)
    - 3.3 [Dictionary Attacks](#33-dictionary-attacks)
4. [Advanced Options](#4-advanced-options)
    - 4.1 [Customizing Hydra Commands](#41-customizing-hydra-commands)
    - 4.2 [Specifying Protocols](#42-specifying-protocols)
    - 4.3 [Parallelized Attacks](#43-parallelized-attacks)
5. [Ethical Considerations](#5-ethical-considerations)
6. [Conclusion](#6-conclusion)

## 1. Introduction to Hydra

Hydra is a tool that cracks login credentials by testing multiple protocols simultaneously. It's fast, flexible, and easily customizable with the ability to add new modules effortlessly.

This tool is commonly used by researchers and security consultants to demonstrate the potential ease of gaining unauthorized remote access to a system.

Hydra supports various protocols such as Cisco AAA, FTP, HTTP(S) forms, ICQ, LDAP, MySQL, SSH, Telnet, and many more. Its versatility makes it a valuable resource for testing and highlighting potential vulnerabilities in systems.

## 2-Installation
Installing Hydra is a straightforward process, especially if you are using Kali Linux or Parrot OS, as Hydra comes pre-installed with these operating systems. For Ubuntu users, the installation can be done using the apt package manager with the following command
```bash
$ apt install hydra
 ```

If you are using Windows, my suggestion would be to utilize a virtual box and install a Linux distribution. Personally, I do not recommend relying on Windows if you aspire to become a professional penetration tester
If you're as stubborn as I am and insist on having Kali on Windows for simpler tasks, you can opt for the Windows Subsystem for Linux `WSL` 
 if you find yourself needing to use Kali on Windows, WSL can be an option, though it may not provide the same level of performance or compatibility as running Kali on dedicated hardware or a virtual machine. After installation, you can check if Hydra is properly installed by typing 
 ```bash
 hydra -h
 ```
 in the terminal. This command will display the help menu for Hydra, confirming its presence and functionality.
 ![image](/assets/img/hydra-help.png)

## 3. Basic Syntax
 
Exploring the functionalities of Hydra involves understanding its various formats and options for brute-forcing usernames and passwords. This encompasses single username/password attacks, password spraying, and dictionary attacks.

Working with Hydra involves utilizing various formats and options for brute-forcing usernames and passwords. Here's a brief overview of common scenarios:
### 3.1 Single Username/Password Attacks
For a single username and password, you can use the following format:

```bash
$ hydra -l <username> -p <password> <target>
```

**To guess Password for specific username**

**hydra -l -P**

If you have a correct username but want to login without knowing the password, so you can

use a list of passwords and brute force on passwords on the host for ftp service.
```bash
hydra -l ox1df -P pass.txt 192.168.1.141 ftp
```

Here -l option is for username -P for password lists and host ip address for ftp service.

**To guess username for specific password**

**hydra -L -p**

You may have a valid password but no idea what username to use. Assume you have a password for specific ftp login. You can brute force the field with correct username wordlists to find the correct. You can use the `-L` option to specify user wordlists and the `-p` option to

specify a specific password.
```shell
hydra -L users.txt -p 123 192.168.1.141 ftp
```
Here, our wordlist is users.txt for which -L option is used, and password is 123 and for that -

p option is used over ftp.

### 3.2 Password Spraying

Password spraying is a technique where a few passwords are tested against multiple usernames to avoid account lockouts. The syntax is as follows:

```bash
$ hydra -L <userlist.txt> -P <passwordlist.txt> <target>

```
Use `<userlist.txt>` and `<passwordlist.txt>` as placeholders for your username and password lists there
you can use `crewl` to make wordlist from exisitng webstie 
`CeWL (Custom Word List generator) is a ruby app which spiders a given URL, up to a specified depth, and returns a list of words which can then be used for password crackers`

or else you can use `rockyou` defalut worldlist

# 3.3 Dictionary Attacks

To execute dictionary attacks, follow these steps:

```bash
$ hydra -l <username> -P <passwordlist.txt> <target>
```

**hydra -L -P**

if you lack either a username or password, you can start to a brute force attack on both parameters by utilizing a wordlist for both.Use the `-U` and `-P` parameters to execute this approach.
```python
hydra -L users.txt -P pass.txt 192.168.1.141 ftp
```
Users.txt is wordlist for username and pass.txt is wordlist for password and it will display the valid credentials for the host after when it `200 status code`

# 4. Advanced Options

## 4.1 Customizing Hydra Commands

Hydra offers numerous customization options. Experiment with flags such as `-t` for threads and `-vV` for verbosity.-V option is used for verbose mode, where it will show the login+pass combination for each attempt. Here, I have two wordlists users.txt and pass.txt so the brute force attack was makingvcombinations of each login+password and verbose mode showed all the attempts.

**To Resume Brute Force Attack**

**hydra -R**

It may happen sometimes, that attack gets halted/paused accidentally due to some unexpected behaviour by hydra. So, hydra has solved this problem by including the -R option so that you
```bash
hydra -R
```

**hydra -l -P -d**

Now is the `-d` option used to enable debug mode. It shows the complete detail of the attack with wait time, conwait, socket, PID, RECV
```bash
hydra -l user.txt -P pass.txt 192.168.1.141 ftp -d
```
-d option enabled debug mode which, as shown displayed complete detail of the attack.

**NULL/Same as Login or Reverse login Attempt**

**hydra -L -P -e**

Hydra has an option -e which will check 3 more passwords while brute-forcing.[n]for null,[s] for same i.e., as same as the username and [r] for reverse i.e., the reverse of username.while brute-forcing the password field, it will first check with the
```bash
hydra -L users.txt -P pass.txt 192.168.1.141 ftp -V -e nsr
```
I have enabled verbose mode also so that we can get detailed information about the attempts made while brute-forcing

## 4.2 Specifying Protocols

Hydra supports various protocols. Utilize the `-s` option to specify the service, e.g., `-s 80` for HTTP.

**hydra -L -P -s**
Network admins sometimes change the default port number of some services for security
reasons. In the previous commands hydra was making brute force attack on ftp service by just
mentioning the service name rather than port, but as mentioned earlier default port gets
changed at this time hydra will help you with the -s option. If the service is on a different
default port, define it using the `-s` option.
```bash
nmap -sV 127.0.0.1
```
```bash
hydra -L users.txt -P pass.txt 192.168.1.141 ssh -s 2222
```
So to perform, first I tried running a nmap scan at the host ports where ssh is at the 2222 port. So post that I tried executing the hydra command with `-s` parameter and port number.


**HTTP Login Form Brute Force**

**hydra -l -P http-post-form**

The hydra form can be used to carry out a brute force attack on simple web-based login forms that requires username and password variables either by GET or POST request. For testing Iused dvwa (damn vulnerable web application) which has login page. This page uses POST method as I am sending some data.
```bash
hydra -l admin -P pass.txt 192.168.1.150 http-post-form “/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed”
```

Here I have given the username admin and provided file for passwords and used http-post-form module to perform brute force attack on host. So, for password: password it gave success and bypassed the login page. Now I had performed brute force on username and password field mentioned having security level as “low”.
```bash
hydra 192.168.1.150 -l admin -P ‘pass.txt’ http-get-form “/dvwa/vulnerabilities/brute/:username=^USER^&password=^PASS^Login=Login:F=User
```
**Password generating using various set of characters**

**hydra -l -x**

To generate passwords using various set of characters, you can use -x option. It is used as -`x min:max:charset` where,
`Min:` specifies minimum number of characters in a password.
`Max:` specifies the maximum number of characters in password.
`Charset:` charset can contain 1 for numbers, a for lowercase and A for uppercase characters.
Any other character which is added is put to the list.Let’s consider as example: 1:2:a1%.
The generated passwords will be of length 1 to 2 and contain lowercase letters, numbers, `%` or `.`
```bash
hydra -l 0x1df -x 1:3:1 ftp://127.0.0.1
```
So, here minimum length of password is 1 and the max length is 3 which will contain numbers and for password 123 it showed success.

## 4.3 Parallelized Attacks

**Attacking Multiple Hosts**

**hydra -L -P -M**

As earlier I performed a brute force attack using password file pass.txt and username file users.txt on a single host i.e., 191.168.1.141. But if there are multiple hosts, for that you can use -M with the help of which brute force is happening at multiple hosts.hydra -L users.txt -P pass.txt -M hosts.txt ftp First, I have created a new file hosts.txt which contains all the hosts. Then the result is showing 2 valid hosts, username and password with success.

```bash
$ hydra -L <userlist.txt> -P <passwordlist.txt> -M targets.txt <target>
```
it is very time-consuming to display all the attempts taking place while the attack, for that we can use provided `-F` option such that the attack will exit after the first found login/password pair for any host.

**Using Combo Entries**

**hydra -C**

This tool gives you a unique parameter `-C` for using combo entries. First, you need to create a file which has data in the colon-separated “login:pass” format, and then you can use `-C` option mentioning the file name and perform a brute force attack instead of using `-L/-P` options separately. In this way, the attack can be faster and gives you desired result in lesser time.

**Authenticated Proxy**

**proxychains hydra**

I got the desired password 123 for the host. In the above attack, there was not any

authentication enabled. Now I tried on a proxy that has 

**authentication enabled.**

**Proxychains**

I tried to brute force the target using proxychains but it was denied because authentication was enabled on the proxy.
proxychains 

So, I added the username and password in `/etc/proxychains4.conf` file `cat /etc/proxychains4.conf`started attacking using the below command
```bash
proxychains hydra -l ignite -P pass.txt 192.168.1.141 ftp
```

Hence, after execution of this command, a valid password was found for the host having proxy enabled.

# 5. Ethical Considerations

Always ensure proper authorization before using Hydra. Unauthorized access attempts can have legal consequences. Use Hydra responsibly, adhering to ethical guidelines and applicable laws.

# 6. conclusion

Mastering Hydra opens the door to effective password testing, a crucial aspect of cybersecurity. Explore its features, experiment responsibly, and enhance your skills in securing systems against potential threats.

This guide provides a foundation for understanding Hydra's capabilities, but it's essential to continue exploring and staying updated in the dynamic field of cybersecurity.
