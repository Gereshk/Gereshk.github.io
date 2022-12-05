---
title: Advent Of Cyber 2022 Day 5
date: 2022-12-05 10.16.00 +/-TTTT
categories: [Try Hack Me, Advent OF Cyber 2022]
tags: [tryhackme,try hack me, hacking, advent of cyber, advent of cyber 2022, advent of cyber day 5]     # TAG names should always be lowercase
author: me
---

# **He knows when you're awake**

## Overall thoughts on room.

Today we take a quick look into brute forcing passwords.  If you have spent any time in a training platform you will be familiar with the tools discussed and used.  Today the written instructions were geared towards hydra.  Although in the walk through video Phillip Wylie does make a point to show the use of other tools which I appreciate because it shows that their is usually a few ways to do everything

 With that lets get into the steps of todays room.

## Get Connected
 
 I again used the attack box provided by TryHackMe. You can do the challenge from your own machine but I find it convient for these quick challenges since I am not at home with my VMs when I have been doing them.  I started both the AttackBox and the target machine and waited for them to both come up
 
## Brute force the VNC password
 
 We know from the intial scans that VNC is open. After determining that it does not require a username just a password I start the hydra scan with the following syntax
 
 ```console
 hydra -P /user/share/wordlists/rockyou.txt vnc://ipaddressoftargert -V -f -t4
 ```

### Explination of the flags used in the command
 
 As always you can look at the man pages to get an understanding of the flags used but I will explain the ones I used
 - -P 
   + Designate password list
 - -V
   + Verbose 
 - -f
   + Stops the hydra attack after it gets a correct password
 - -t4
   + Desingnates the number of threads to use for the attack
  
## Results of the scan

After we let the hydra scan run for a while we catach a correct password and the scan stops
![hydrascan](/assets/AOCD5/hydra%20scan.png)

### Question 1

The Hydra scan answers question 1 for us
![q1](/assets/AOCD5/q1.png)

## VNC into the machine

Now that we have the password we can VNC in and take a look around.  You can use whatever VNC client you want to use but Remmina is installed on the machine so we will use that.  Once connected it asks for a password and we give the password found from the brute force attack.
![password](/assets/AOCD5/vnc%20password.png)

And we are in. 

![screen](/assets/AOCD5/vnc%20SCREEN.png)

### Question 2

We can see the answer to question 2 on the screen so we grab that and enter it into the answer table and we are done for today
![q2](/assets/AOCD5/q2.png)
