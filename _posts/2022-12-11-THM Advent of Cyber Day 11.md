---
title: Advent Of Cyber 2022 Day 11
date: 2022-12-11 09.33.00 +/-TTTT
categories: [Try Hack Me, Advent OF Cyber 2022]
tags: [tryhackme,try hack me, hacking, advent of cyber, advent of cyber 2022, advent of cyber day 11]     # TAG names should always be lowercase
author: me
---

![day11](/assets/AOCD11/day11.png)

#  Not all Gifts are Nice

## Overall thoughts

	This was a good introduction to the volatility tool and its uses.  The Room was very follow the leader.  Stick to the instructions and you wont get lost.

### Getting started

We just need to lauch the attack box.  I did have some connection errors during this room but the seemed to resolve themselves after some time.

### Step one

	First we need to get our terminal to the right place.  Everything that we need will live in the volatility3 folder so lets change directory into that

```console
cd volatility3
```

There are a lot of commands you can run and if you are interested their website has great resources.

The first command we are going to run is this one

```console
python3 vol.py -f workstation.vmem windows.info
```
This will get the image info so that we can answer question 1

#### Question 1

![q1](/assets/AOCD11/q1.png)

Looking at the information we can find the answer

![answer1](/assets/AOCD11/Results.png)

## Step two 

Following along we now need to get the gift left by santa we can do that by listing out all the processes that were running when the image was take with this command

```console
python3 vol.py -f workstation.vmem windows.pslist
```

That will get us the answer to question 2 and 3

#### Question 2 and 3

![q2](/assets/AOCD11/q2.png)

![q3](/assets/AOCD11/q3.png)

![santa](/assets/AOCD11/santa.png)

### Step Three

Now we have to dump the contents of the binary and to do that we will use this command

```console
python3 vol.py -f workstation.vmem windows.dumpfiles --pid <processID>
```

#### Question 4

![q4](/assets/AOCD11/q4.png)

and with that we get the files dumped onto our screen.  we can just count them and get the answer

![pid](/assets/AOCD11/piddump.png)

# Conclusion

Very quick room. This just scratches the surface of what volatility3 can do.  I encourage you to look into it more as it is very powerful.
