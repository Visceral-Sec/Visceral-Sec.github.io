---
layout: post
title:  "DEV x1: Zarathrustra; 
System Design & the concept of Time."
date:   2022-11-30 13:37:00 -0700
categories: Cyber-Security
author: Archer B
---
## Catch Up
30 days of thinking:
- More Kernel Fears (link to the blog)
- Choose to use machine-learning; inspired by dark trace and their work with JA3
- Looking ahead to potential solutions and system-design
### System Design?
Introduce some inital thinking regarding system design:
# Three pronked approach
- Create a data-collector which collects process runtime information (Diagnostics System)
- Machine-Learning Model that processes the runtime diagnostics.
- Implement a process wrapper than kills/alert the process depending on machine-learning model baseline. 
# Contious Adaptation Approach
- Instead of a three seperate model approach you combine them both,
- Each different component still exists but they run concurrently.
- Contious model evolution through out runtime.

# Potential Future Problems 
Adverisal Prepbutation & bias problems
#Data Collection Design?
# Different issues thought about:
- Different Sources of Process meta-data:
-- System Calls (STRACE)
-- Proc Virtual File System
-- BLKTRACE/DTRACE
-- NICSTAT 
-- PERF
-- SAR
## Machine-Learning

# Why Machine-learning? 
# Machine-learning should use classification? or regression? 
# Does an anomaly inherently mean a threat & The issue of supervision.


## Time as a feature?
# The Possiblity?
# The Problem?
# Inspired by previous work in anomaly detetction. (A.Hood)