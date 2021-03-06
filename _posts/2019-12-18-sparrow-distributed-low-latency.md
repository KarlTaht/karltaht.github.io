---
layout: posts
title: "Sparrow: Distributed, Low Latency Scheduling"
date: '2019-12-18T09:15:00.002-08:00'
author: Karl Taht
categories: [research-papers, research]
tags:
- cluster scheduling
- spark
- ec2
- scheduling
- cluster computing
- latency
- tpc
modified_time: '2019-12-18T09:15:38.025-08:00'
blogger_id: tag:blogger.com,1999:blog-2670908301789336410.post-5685745132789555116
custom_excerpt: "This work presents Sparrow, a stateless, decentralized scheduler for cluster scheduling. The scheduling component uses two key ideas: batch sampling and late binding."
blogger_orig_url: https://researchdoneright.blogspot.com/2019/12/sparrow-distributed-low-latency.html
---

Authors: Kay Ousterhout, Patrick Wendell, Matei Zaharia, Ion Stoica
Venue:    SOSP 2013

This work presents Sparrow, a stateless, decentralized scheduler for cluster scheduling. The scheduling component uses two key ideas: batch sampling and late binding. Batch sampling is an extension of the power of two choices [1], which shows that the "tail" can quickly be cut off by simply sampling between two machines versus randomly selecting one. Batch sampling generalizes this by sampling dm machines, and placing the m tasks on the machine with the lowest load. Late binding delays the actual task transfer until the machine is ready to process the request. This can be thought of as having a place holder in the worker's queue, and when the worker is finally ready to process it, the actual task is transferred from the scheduler to the worker. This avoids having to rely on inaccurate metrics such as queue depth. Each worker maintains its "instance" of Sparrow, which uses multiple queues to enforce global policies. Additionally, Sparrow is orthogonal to straggler mitigation techniques, and they could be applied in conjunction.

Sparrow does have the following limitations:
* Limitations of placement constraints: "my job should not be run on machine where User X's jobs are run"
* No bin-packing (for performance, I assume)
* No gang scheduling
* No preemption, so by extension, struggles with (highly) heterogeneous tasks
* Despite the limitations, the end result is extremely impressive -- within 12% of an optimal scheduler. And the optimal scheduler is very idealistic (assumes no transfer time). 


[1]: Mitzenmacher, Michael. "The power of two choices in randomized load balancing." IEEE Transactions on Parallel and Distributed Systems 12.10 (2001): 1094-1104.