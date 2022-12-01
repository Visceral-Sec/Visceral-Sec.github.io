---
layout: post
title:  "DEV x1: Zarathrustra; 
System Design & The Concept Of Time."
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
- 
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

Adverisal Prepbutation & bias problems
Data Collection Design?
# Fighting against the future --> What is the perfect baseline?

## Time as a feature?
# The Possiblity?
# The Problem?
# Inspired by previous work in anomaly detetction. (A.Hood)