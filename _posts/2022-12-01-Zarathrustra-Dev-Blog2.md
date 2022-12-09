---
layout: post
title:  "DEV x1: Zarathrustra; 
System Design & The Abstract Concept Of Time."
date:   2022-11-30 13:37:00 -0700
categories: Cyber-Security
author: Archer B
---
WIP Post
---
## Catch Up
30 days of thinking:
- More Kernel Fears (link to the blog)
- Choose to use machine-learning; inspired by dark trace and their work with JA3
- Looking ahead to potential solutions and system-design
- Digging into the problem.

## Machine-Learning

# Why Machine-learning? 
# Machine-learning should use classification? or regression? 
# Does an anomaly inherently mean a threat & The issue of supervision.

### System Design?
Introduce some inital thinking regarding system design:
# Seperation approach
Create a data-collector which collects process runtime information (Diagnostics System)
Machine-Learning Model that processes the runtime diagnostics.
Implement a process wrapper than kills/alert the process depending on machine-learning model baseline. 
# Contious Adaptation Approach
Instead of a three seperate model approach you combine them both, Each different component still exists but they run concurrently.
- Continuously gather data through run-time execution;
- Generating a "moving" baseline based on the baseline
- Contious evaluation of the proccesses's "threat-level"

For reasons that I can't exactly pinpoint, I envision the contious adapation to use a regression model Whereas the three seperate component approach to be classification. I don't truly know enough about the implementation of different machine learning models to pinpoint exact reasoning but I will add a few ideas here for my future self to evaluate:
# Reasoning For & Against Seperation & Classification
## For
- Easier to develop, each model can be made independly only relying on the output of one-another.
- Classification models are commonly used with unsupervised learning
- Allows for a more general approach, less specific quantifiable variables needed which in theory should make it more effective as approach to all types of processing.
## Against
- Relying on a pre-made dataset. The dataset that the process is running against may not reflect the current baseline.
- As the approach is less-specific, more effective options could be taken for specific processes. The impact of this needs to be evaluated; e.g how "much" of an improvement is a contious/regression system design?
# Reasoning For & Against Contious & Regression
## For
- Therotically infinitely scaling; you can train the data for as long as the process is running, can get as close as possible to a "baseline" (An idea expanded upon in the bottom)
- Doesn't rely on old-data, the training data in the seperation model could become outdated and not reflect the current workings of the process.
- Regression allows a more specific reading on a process, having a quantifiable reading of "anomalous activity" means you can both directly classify (Reading over let's say 0.7 = anomlous activity) 
## Against
- Difficult to code effectively, multi-threading as well as a combination of high-level and low-level languages work in tandem.  
- Not sure how possible a regression model would be to implement for processes; so assuming a high potential for a kernel fear
- Really hard to pinpoint what's an anomaly and what's just a feature that hasn't had recorded usage, this problem sticks out to me as the biggest issue.
# Potential Future Problems 
Adverisal Prepbutation:
If a process is known to be using a contious baseline could they then slowly change the baseline through minutest of changes to therefore allow for future changes? The proverbially: Frog in the Pan problem.

# Fighting against the Future: The Problem Of Predicitability

Processes are volitale. Think about a common command-line tool, how many people really use every single feature? Keeping this is mind; How do we differicate anomlies? What identifies a previously unused feature and an actual threat? 

I conceptualize a *Perfect* baseline. This baseline includes every convincible method, feature or parameter, input that a process is capable of doing. A universal set of safe process activity. This *perfect* baseline would be infalliable. Anything that doesn't fit within the baseline would be considered anomalious. Unfortnutely, this perfect baseline is unobtainable.

For example, picture a small IT blog. Not exactly the most visited website on the internet. One day however, a post goes viral: thousands of different people all visit this blog to check it out. How would a machine-model identify the difference between a Ddos and heavy load?

Would the universal set of correct process activity include high cpu execution time? Would It keep track of different IPs? Distrubted attacks using different ip-ranges?

I'm confident there are lot of edge cases which demostrate the issue of **possibility**. The future is pretty hard to predict. 

An potential way would be if we could classify types of processes. These classifications would include hard-coded logic on what to expect the future to "look like" this could be implemented through certain biases in the ML model. A part of me is hesitant to include any hard-coded logic from a cyber-security pov. 

- ML Biases are different that just "biases"
- Machine-learning learnt bias might be acceptable but my own biases aren't acceptable; the biases should be fine tuned by the machine not me.

## Random off the hinge idea:

Large cloud neural networking --> connects to all usages of zarathrusta --> uses this input data as classification --> then relies this information to the zarathrustra client and provides it with a general outline baseline which is then re-defined using local anomalous data. This therefore allows for a global standardise definition of different expected loads, for example the config passed to the zarathrusta client would didicate some global assumptions like "low-high-extreme" cpu and load variables.
This would also need to take system variables and other parameters as well as a networking component.

However I did managed to get this to work, I would be a millionaire, famous, well loved and successful in every socieitally convicable way.

# Issue of classification 

--> insert the spiel about hard-coded logic being a bad answer. and link to a future potential blog 

What can we use to classify between a threat and a anomaly?
- Time is a potential idea as a a feature


## Time as a feature:

How relevant is Time?
What differs between each cup of tea? The type? The temperature? The Mug? The amount? But once you add time as a dimenson you can increase these questions further: - How long has the tea been brewed? The time since your last cup of tea? How long did it take to drink? What day/second/minute etc etc. 

So can you not take this principle to anomaly detection?

# The Possiblity?

Christmas day is the https://www.makeuseof.com/why-cyberattacks-surge-during-holiday-season/ is one of the most popular days for cyber-attacks. Taking this into account, in the example of a regression model given earlier it might be sensible to reduce the threat-level needed to classify a anomaly.

Another potential idea would be an admin login. On it's own, its not too unusual but a admin login at 3 in the morning? Might be normal traffic within a global company but in a small office that could be deemed as suspicious. 

I currently can't see a way to solve the issue of prediciabiltiy but it does add a lot more dimesonality in how to differiticate 
between anomalies and threats.

# The Problem?

- curse of dimensionality

- How significant of an impact should it have? Why not use patterns in different parts of processes?

- 