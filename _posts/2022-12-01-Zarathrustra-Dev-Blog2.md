---
layout: post
title:  "DEV x1: Zarathrustra; 
System Design & The Abstract Concept Of Time."
date:   2022-11-30 13:37:00 -0700
categories: Cyber-Security
author: Archer B
---
In the last 30ish days, I've had time to reflect upon my previous blog and the ideas presented it. I've discovered a few [more Kernel Fears](https://visceral-sec.github.io/cyber-security/2022/11/02/Zarathrustra-Dev-Blog1.html) as well as began to delve into the different way utilisation of machine-learning in cyber-security. I first came to seriously address machine-learning [after reading about JA3's TLS Fingerprinting & Dark-Traces applications](https://darktrace.com/blog/beyond-the-hash-how-unsupervised-machine-learning-unlocks-the-true-power-of-ja3). JA3 fingerprints are unique hashes based off initial TLS handshakes which in-turn can uniquely identify types encrypted traffic. 
This method of identifying a previously thought of "Information-less" method of transport (Encrypted Traffic) to a point where you can uniquely identify source applications such as slack having the JA3 encryption identifier of "a5aa6e939e4770e3b8ac38ce414fd0d5." is ground-breaking. Although, JA3 is not related to machine-learning, Dark trace's utilisation of JA3 within their own anomalous IDS gives me inspiration that potential kernel fears can be overcome.
# Why Machine-learning? 
Machine-learning in anomalous based detection can more effectively solve some of the major issues within anomaly detection. Machine-learning models can more effectively find patterns within datasets that we might struggle ourselves to identify through classification models. Using loss-functions to refine biases is much more likely to be accurate compared to our own biases. Additionally, machine-learning models can refine their judgements and evolving over time which is incredibly powerful for anomaly detection.
# Machine-learning: Supervised or not?
Supervision, in the context of IDS, is not inherently bad but does come with a few drawbacks. One potential disadvantage is that labelling the data is time-consuming especially with how large anomalous IDS datasets are. Therefore, trained supervised models are difficult to maintain. For example, if the model began to become obsolete due to changing threat-landscapes it would be expensive and time-consuming to re-train the dataset on the new landscape. Another potential problem is the reliance of accuracy. When labelling the data (supervision) inherit biases can unknowingly affect the baseline, this can lead to many false positives and false negatives. These disadvantages if not addressed can greatly reduce the overall effectiveness of an intrusion detection system.

In comparison, classification models don't require labelled data which therefore can handle much larger data-sets as well as adapt quickly to different threat landscapes. On average, unsupervised models are much more suited to anomaly detection but they still come with their own problems such as overfitting and incorrect tuning.

### System Design?
Taking a step back into Zarathustra, I've begun to think out potential system designs. Some initial thinking led me to two potential approaches: Separation and continuous. The separation method separates the problem into three distinct and separated components: A data Collector, the machine-learning model, and the IDS system itself whereas the continuous method would combine all three functions into one large infinitely running system.
# Separation approach
The Separation approach, as briefly described aims to separate all functionality into separate components. These components would be:
- A data-collector which collects process runtime information (Diagnostics System)
- Machine-Learning Model that processes the runtime diagnostics.
- Implement a process wrapper than kills/alert the process depending on machine-learning model baseline.

#### For

- Easier to develop, each model can be made independently only relying on the output of one-another.
- Classification models are commonly used with unsupervised learning
- Allows for a more general approach. The machine-learning model can be separated making the process much easier to run.

#### Against

- Relying on a pre-made dataset. The dataset that the process is running against may not reflect the current baseline.
- As the approach is less-specific, more effective options could be taken for specific processes. The impact of this needs to be evaluated; e.g how "much" of an improvement is a continuous/regression system design?

# Continuous Adaptation Approach
Instead of a three separate model approach you combine them both, each different component still exists but they run concurrently.
- Continuously gather data through run-time execution.
- A machine-learning model evolving the baseline based on the new gathered data.
- Continuous evaluation of the processes’ "threat-level"

### For
- Theoretically infinitely scaling; you can train the data for as long as the process is running, can get as close as possible to a "baseline" (An idea expanded upon in the bottom)
- Doesn't rely on old-data, the training data in the separation model could become outdated and not reflect the current workings of the process.
- Regression allows a more specific reading on a process, having a quantifiable reading of "anomalous activity" means you can also directly classify (Reading over let's say 0.7 = anomalous activity) 
### Against
- Difficult to code effectively, multi-threading as well as a combination of high-level and low-level languages work in tandem.  
- Not sure how possible a regression model would be to implement for processes, so assuming a high potential for a kernel fear
- Really hard to pinpoint what's an anomaly and what's just a feature that hasn't had recorded usage.

# Potential Future Problems 

## The Frog in The Pan
If a process is known to be using a continuous baseline, could they then slowly change the baseline through minutest of changes to therefore allow for future changes? 
The proverbially: Frog in the Pan problem.
This issue would affect both system models but would easier to pull off using the continuous adaptation model. As that approach utilises current processing to change and alter the baseline during run-time, an adversary could slightly and slowly alter the baseline to eventually allow malicious activity to become undetected. Although this problem still exists in mere speculation as well as seeming similar to [adversarial perturbation](https://www.youtube.com/watch?v=yd4j8ue521g)

## Fighting against the Future: The Problem Of Predictability

Processes are volatile: think about a common command-line tool, how many people really use every single feature? Keeping this is mind; How do we differentiate between anomalies and threats? An interesting problem in this domain, is how unsupervised models differentiate between anomalies and threats.
Potentially there exists some method that can effectively differentiate them.

For example, picture a small IT blog. Not exactly the most visited website on the internet. One day however, a post goes viral: thousands of different people all visit this blog to check it out. How would a machine-model identify the difference between a DDos and heavy load?

As a thought experiment, I conceptualized a *Perfect* baseline. This baseline includes every convincible method, feature or parameter, input that a process can do. A universal set of safe process activity. This *perfect* baseline would be infallible. Anything that doesn't fit within the baseline would be considered anomalous. Going back to the previous example; would the "Perfect Baseline" know the difference? Would it simultaneously include both high and low CPU execution time? Would It keep track of different IPs? Then what about distributed attacks using different ips? It seems that the unfortunately, this perfect baseline is unobtainable. I'm confident there are lot of different edge cases which all demonstrate the issue of **possibility**. The future is hard to predict. 

There are a few different ways we can address this problem, one potentially method is hard coding the answer: supervision. Using a supervision model could allow us to avoid this problem all together. Although, as previously mentioned, supervision creates other problems that we previously avoided. Classifying the process further could allow us to implement some hard-coded rules on how a process should operate. Another option could be to include a machine-learning feature that reduces the problem space. (Reduces the number of unknown "anomalies")

# Classifying Processes
A potential way would be if we could classify types of processes. These classifications would include hard-coded logic on what to expect the future to "look like" this could be implemented through certain biases in the ML model. A part of me is hesitant to include any hard-coded logic from a cyber-security point of view, hard-coded logic is a commonly exploit flaw in most systems. As mentioned earlier, the "Frog in the Pan" problem could be easily applied here for example. 

# Time as a feature:
One potential feature that could be used is Time.

What differs between each cup of tea? The type? The temperature? The Mug? The amount? But once you add time as a dimension you can increase these questions further: - How long has the tea been brewed? The time since your last cup of tea? How long did it take to drink? What day/second/minute etc etc. 
So, can you not take this principle to anomaly detection?
# The Possibility?

[Christmas day is one of the most popular days for cyber-attacks.](https://www.makeuseof.com/why-cyberattacks-surge-during-holiday-season)

Picture an Admin portal login. On its own, it’s not too unusual but a admin login at 3 in the morning? Might be normal traffic within a global company but in a small office that could be deemed as suspicious. Time seems like an effective method of adding more dimensions to data, which can help reduce the problem space of differentiating between anomalies and threats.

# The Problem?

However, time could potentially create too much data. Within machine-learning and Ai in general there is a term called "curse of dimensionality". The curse of dimensionality refers to how introducing too features can make the data increasingly difficult to analyse and interpret. Adding too many data-points can lead to over-fitting where new data is unable to generalized. 

Taking this into account, how would you represent the importance of Christmas in a ML model? In a regression/supervised model you could quite easily specify certain criteria for Christmas but what about classification models? But what about classification? Time itself can be easily identified but how do we represent the importance of more societally/abstract importance of time such as a national holiday? 

How reliable is the time reading during operation? Going back to our frog in the pan problem, could time be manipulated on a system to make certain actions be acceptable during a window of time? For example, a adversary could potentially could train the model to allow some specific malicious traffic at an arbitrary time. 