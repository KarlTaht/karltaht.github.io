---
layout: posts
title: Multi-Resource Packing for Cluster Schedulers (Tetris)
date: '2020-01-08T08:57:00.001-08:00'
author: Karl Taht
categories: [research-papers, research]
tags:
- cluster scheduling
- spark
- resource allocation
- tetris
- cluster computing
- map-reduce
- resource-aware scheduling
- resource management
custom_excerpt: This work presents a resource-aware cluster scheduling scheme which maximizes performance and includes additional parameters to balance fairness requirements.
except_sepator: <!--more-->
---

Authors: Robert Grandl, Ganesh Anathanarayanan, Srikanth Kandula, Sriram Rao, Aditya Akella

Venue: SIGCOMM 2014

Cluster level scheduling is a complex topic in which performance, fairness, and hard constraints must all be considered. Fundamentally, a perfectly fair solution sacrifices performance. This work presents a resource-aware cluster scheduling scheme which maximizes performance and includes additional parameters to balance fairness requirements. <!--more--> For simplicity, I will divide the discussion into two sections: the central idea and additional heuristics.

Tetris performs scheduling by analyzing jobs resource requirements in terms of CPUs, memory, disk I/O, and network usage. Each job, task (a subset of a job), and machine is assigned a resource vector. To determine the optimal positioning of a task, a heuristic is used which takes the dot product of the job's resource requirements vs a candidates available resources. The machine with the maximum dot product is selected to place the job. To incorporate fairness into the approach, the number of candidate jobs can be adjusted. Maximizing fairness will only place jobs in the global queue order, while maximizing performance will consider all jobs in the queue.

In addition to the basic setup, Tetris also includes additional heuristic properties to ensure no low-hanging fruit is left on the table. Firstly, shortest remaining time first (SRFT) algorithm is incorporated into the scheduling calculations, such that dot products are weighted to favor jobs nearly completions. The next optimization comes from the nature of map-reduce and DAG dependencies. Again, when a job is nearing the end of a stage, it's tasks a favored so that it can begin the next stage sooner. The last significant optimization is regarding the "remote penalty". When a job is scheduled away from data locality, it's network requirements will increase. Thus, jobs which cause this are assigned a penalty (note this part is a bit vague in the details from my reading).

Overall, exceptional gains are achieved of a 40% improvement in job completion time and 41% improvement in job makespan (the total time for all jobs to complete). This occurs with a minimal impact in fairness, where about 6% jobs are delayed more than 10%. It would have been nice to see an S-curve of job improvements to illustrate the details more clearly, but nevertheless fairness seems to suffer marginally.