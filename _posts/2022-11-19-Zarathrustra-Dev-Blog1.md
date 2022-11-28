---
layout: post
title:  "DEV x0: Zarathrustra; Initial Ideas & Kernel Fears"
date:   2022-11-02 13:37:00 -0700
categories: Cyber-Security
author: Archer B
---
 
# Anomlous Based Detection
[I like anomlous based detection](https://visceral-sec.github.io/psychology,/cyber-security/2022/10/28/The-Untapped-Potential-Of-Sound.html). Cyber-security seems so defined by red and blue team's proverbially cat and mouse game, where blue team always seems to be one step behind. However, certain techniques such as anomlous based detection seems to give blue team the advantage. Although I am hesitant to say that anomlous detection *changes the game* enough to finally stop using the cat and mouse game analogy, I do believe that it changes the game some what; Giving red-teams another obstacle. Not only do Red-Teams need to discover vulnerabilities, they need to do so without alerting the "guards". Unfortnutely, like professional acrobats, red teams always find a way through. However, increasing the difficulty as well as the amount of obstacles red-teams need to face does improve cyber-security posture.

Anomaly based detection, unlike signature-based detection, anomaly detection doesn't rely on a fixed list. (It's important to note that in most modern applications of signature-based detection certain malware behaviour also have signatures.) Anomaly based detection relies on a "baseline" which a is a set of behavioural characterisitics that are considered usual. Mapping current operation to the baseline means we can idenitfy differences between the two behaviours. These differences can be big or small, but usually there is some internal logic in addition to what ought to be considered an anomaly, such as a bias in a machine-learning algorithim or hard-coded logic. 

# Inital Ideas

The most common use of anomlous based detection is within network security. However, the concept isn't limited to just networking. Anomalous based host intrusion detection systems (HIDS) perform the same method but applied to a operating system's behaviour.  One story told in the podcast [darknet diaries](https://darknetdiaries.com/) describes how a penetration tester almost got discovered by loading powershell on receptionisit's machine which hadn't launched a console in 5 years.

Following this line I thought I questioned whenever if I could reduce the scale further? The premise was originally applied to networking, now to just a singular machine.. So why not a individual process? 

If we could apply anomaly based detection to a individual process. Wouldn't it give binary exploitators an obsctale they haven't faced before? If we could create an accurate baseline for processes, then techniques such as ROP chains would become easily be detectable as the process system behaviour would greatly differ from the baseline.

I did some quick inital searches to see if this idea was already well-established and pre-existing solutions were already out there but I couldn't find much. I stumbled across owasp's [App Sensor](https://owasp.org/www-project-appsensor/) which wasn't exactly what I envisoned but was clearly born of the same concept. Some alternatives found were [SELinux](https://www.redhat.com/en/topics/linux/what-is-selinux) and docker security stripping methods. Both of which didn't incorporate anomaly detection methods but were focused on more specific process security such as limitng systemcalls.

--- Cool Sentence about why I decided to puruse the idea myself ---

# Kernel Fears

As with any good idea, you should first start with doubting why it isn't one. 

I'm unsure if it's my own prinicples or my own insecurity that lead to the axiom of "If the idea is good, why hasn't someone already done it before?". Eitherway, that question haunts my thinking. You may of heard of the fermi paradox, which I think is a really accurate description of this type of internal doubt: *["If life is so easy, someone from somewhere must have come calling by now."](https://en.wikipedia.org/wiki/Fermi_paradox)* One of the proposed answers to this paradox is the "great filter" which describes that perhaps there is some large unavoidable event that is incredibly hard or impossible to over-come [Paraphrased](https://en.wikipedia.org/wiki/Fermi_paradox#Great_Filter). Applying this concept to my worries you can derive: "Other people have found the reason why it doesn't work in practice". I've decided to described these reasons as "Kernel Fears". 

Working with process is considered a pretty low level task. (Low level referring to only a small about of abstraction away from hardware, the larger the abstraction) Therefore a lot of common low-level problems could be these great filter. First one that comes to mind is race conditions. Race conditions describe when two procedures need to use the same resource and therefore influence each other, this could a variable value which is correct for one of the procedures but incorrect for another or could cause effiency issues. Race conditions could come up as a problem in all sorts of ways, such as process run-time information being gathered interferes the running of the process.

Another potential kernel fear could be that process behavioural data is just too volitate to create a baseline with. I personally don't think that process behavioural is that too variable but potentially somewhere there is a gap of in my understanding of how processes and operating systems work.

Another potential issue is regarding malware behaviour. Malware is capable of jumping between processes through techniques such as process hollowing and process injection. Creating a process might not be considered an anomaly? So if malware jumps to a process that hasn't got a baseline then no matter how "suspect" the behaviour is the detection system won't pick it up. Obviously, this is quite a specific issue but it goes to show that there is a lot of potential problems that are pretty hard to foresee.

In the next development entries I wish to explore previous research, the potential for machine-learning and what I should consider an anomaly?