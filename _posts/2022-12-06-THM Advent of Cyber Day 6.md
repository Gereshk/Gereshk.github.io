---
title: Advent Of Cyber 2022 Day 6
date: 2022-12-06 10.16.00 +/-TTTT
categories: [Try Hack Me, Advent OF Cyber 2022]
tags: [tryhackme,try hack me, hacking, advent of cyber, advent of cyber 2022, advent of cyber day 6]     # TAG names should always be lowercase
author: me
---

# **It"s beginning to Look A Lot Like Phishing**

![d6](/assets/AOCD6/day6.png)

## Overall Thoughts
This was a great intruduction to looking for imformation in a malicous email.  Most people unless in that role would actually know how to do this.  I think it is great we are getting all sorts of different views on different skills to build for ourselves.  Overall had at all if you follow the instructions or the video walk through provided by Cyberseurity Meg

## Getting Started 
There are more questions today than on previous days but we should be able to power through them quickly

In this room the box automatically spawns with an image with everything you need to include the email file.  So following the instructions we open up sublime text editor and open the email file 

My Sublime automatically opened it in the correct format but the instructions are there if you need to change the format to email header

### Lets start answering questions

#### Question 1

![q1](/assets/AOCD6/q1.png)

Looking at the information in sublime we can see the From field which gives us the answer to Question 1

![sender](/assets/AOCD6/sender.png)

#### Question 2

![q2](/assets/AOCD6/q2.png)

Again looking at the information in sublime we can see the retun-path which gives us the answer to number 2

![return](/assets/AOCD6/Return.png)

#### Question 3

![q3](/assets/AOCD6/q3.png)

This one was answered with the information we gathered from question one so lets look there again

![sender](/assets/AOCD6/sender.png)

#### Question 4

![q4](/assets/AOCD6/q4.png)

Question four has us looking for the X-spam source which again we can find in the information in Sublime 

![xs](/assets/AOCD6/xs.png)

#### Question 5

![q5](/assets/AOCD6/q5.png)

This one we will find the hash in the informaiton in sublime we just have to decode it.  I personally like Cyberchef.io but you can easily just google a base64 decoder and get the answer.

![cyber](/assets/AOCD6/cyber.png)

#### Question 6

![Q6](/assets/AOCD6/q6.png)

Now we are going to have to visit the website emailrep.io to check the senders email rep

![risk](/assets/AOCD6/risky.png)
That was easy

#### Question 7

![q7](/assets/AOCD6/q7.png)

This one is found in the information in sublime again 

![attach](/assets/AOCD6/attach.png)

#### Question 8

This one we will have to use a few command line tools to get the hash

Open up terminal and make sure we Change directory, CD, into the desktop folder.  First we will have to run the email anylizer to extract all the information the command will be.

```console
emlAnalyer -i Urgent\:eml --header --html -u --text --extrat-all
```

Now if we check our directory we have the eml_attachment folder we can cd into that and run the get the hash value by running this command

```console
sha256sum Name_of_email_attachment
```

and there is our hash

![hash](/assets/AOCD6/sha.png)

#### Question 9

Now we have to visit the virus total website with the hash and see what it says for the hash.

![def](/assets/AOCD6/defense.png)

#### Question 10

![q10](/assets/AOCD6/q10.png)

This question has has using another website to check the hash

Looking it up we can see the subcategory for the hash

![macro](/assets/AOCD6/macro.png)

## Conclusion 
That brings us to the end of day 6 of Advent of Cyber.  I am really excited for tomorrow and the end of the first week.
