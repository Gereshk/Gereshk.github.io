---
title: Advent Of Cyber 2022 Day 4
date: 2022-12-04 14.44.00 +/-TTTT
categories: [Try Hack Me, Advent OF Cyber 2022]
tags: [tryhackme,try hack me, hacking, advent of cyber, advent of cyber 2022, advent of cyber day 4]     # TAG names should always be lowercase
author: me
---
# **Scanning Through The Snow**

## Overall Thoughts
Today with Try Hack Me's Advent Of Cyber 2022 event we are looking at NMAP scanning.  Overall I feel like this was a good introduction to NMAP and some of its tools.  It barely scratched the surface of what I know NMAP is capable of.  Although I did feel this was well positioned for the target audience THM was after.  Beginners, the people who have never ran an NMAP scan, and thoughs who are starting out.

I really liked how they built off of day 3 and the credientals found during OSINT were incorperated into the challenge.

## The Steps
First we need to start the machine we will be scanning and for convience sake I will be using the AttackBox provided by THM.

The first thing I like to do is just a ping to make sure the box you are "attacking" with has connection to the target box

![Ping](/assets/Advent_of_Cyber_day_4/ping.png)

Once I verified that a ping was successfully I followed along in the instructions.  The first instruciton I read and completed was a SYN scan. To complete a SYN Scan the -sS flag must be in the command.  Please note the IP address should be of your target machine.

```bash
nmap -sS Ipaddressfortargetmachine
```

The results form this were

![nmap_results](/assets/Advent_of_Cyber_day_4/nmap%20results.png)

I found four ports open and they are as follows
- Port 22 
    + Used for SSH
- Port 80
    + Used for Http 
- Port 139
    + Used for Netbios-ssn
- Port 445
    + Used for Microsoft-ds

These are all the default for the services that are running on them.  After awhile you will learn which port number is normally associated with which service.  None of these gave the version or name of the service running on that port so we had to do some more scanning.

This time we will combine some NMAP flags into one command 

```bash
nmap -sS -sV Ipaddressfortargetmachine
```

As we learned with the first scan the -sS has NMAP do a SYN scan,  -sV tells NMAP to try to figure out the versions of the services running on each port that is open. 

![nmapflags](/assets/Advent_of_Cyber_day_4/nmapwithflags.png)

These results will allow us to start answering the questions.

## Quesiton 1

![Q1](/assets/Advent_of_Cyber_day_4/Q1.png)

Form the scan we can see that it is running **Apache** on port 80

## Question 2
![Q2](/assets/Advent_of_Cyber_day_4/q2.png)

From the scan we can see that **SSH** is running on port 22

With the first two questions answered we move on, following the instructions, to accessing the samba service we do that by opening our file explorer and connecting to the address.  We sould know that samba is available because when we ran the NMAP scan with the -sV flag it returned that samba was running on ports 139 and 445 which are the default ports.

```bash
smb://Ipaddressfortargetmachine
```

we get this connection

![samba](/assets/Advent_of_Cyber_day_4/samba.png)

Clicking on the admin folder we get a login prompt.  Using the provided login info.  Which was found from Day 3 of the challenge we are presented with two files.  A flag.txt and userlist.txt

![files](/assets/Advent_of_Cyber_day_4/files.png)

## Question 3

Opening the flags.txt file we are presented with the answer to question 3

![q3](/assets/Advent_of_Cyber_day_4/q3.png)

## Question 4

Opening the userlist.txt we are presented with the answer to question 4

![q4](/assets/Advent_of_Cyber_day_4/q4.png)

That concludes the day 4 challenge of the Advent of Cyber 2022 event.  Lets see what tomorrow brings
