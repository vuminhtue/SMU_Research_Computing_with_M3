---
title: "The structure of the M3 Cluster"
questions:
- "What is the structure of the M3 Cluster?"
teaching: 15
exercises: 0
objectives:
- compute and login nodes, hardware table
keypoints:
- "M3 contains more than 178 interconnected compute nodes"
- "a specialized login node runs the SSH server"
---

The computers that make up the M3 cluster are called *nodes*. Most of the nodes on M3 are *compute nodes*, 
that can perform fast calculations on large amounts of data. There are also several special nodes called the *login nodes*; they run the server, 
which works like the interface between the cluster and the outside world. 

The people with M3 accounts can log into the server by running a client (such as `ssh`) on their local machines. 
Our client program passes our login credentials to this server, and if we are allowed to log in, the server runs a shell for us. 
Any commands that we enter into this shell are executed not by our own machines, but by the login node.

![image](https://user-images.githubusercontent.com/43855029/151622253-e177426a-9957-4c65-a4f4-618289e35b4e.png)

Another special node is the *scheduler*; M3 users can get from the
login node to the compute nodes by submitting a request to the scheduler, and the scheduler will assign them to the most appropriate compute node.
M3 also has a few so-called "service" nodes, which serve special purposes like transferring code and data to and from the cluster, and hosting web applications.

To see the configuration of nodes, max memory and walltime in each of the partition (queue), you can type

~~~
sinfo --Format="PartitionName,Nodes:10,CPUs:8,Memory:12,Time:15,Features:18,Gres:14"
~~~

To see which nodes are available at the moment, you can type 

~~~
cat /hpc/motd/m3_queue_status
~~~
{: .bash}


This table shows the amount of different queues, number of running jobs, waiing jobs and idle nodes. The number of *idle nodes* per each queue are completely free node: a node which has, for example, 8 cores, but only 4 of them are used, would not be counted as "free". So this table is a conservative estimate. This picture can change pretty drastically depending on the time of the day and the day of the week.

In brief:
- 170 standard compute nodes with 128 cores, 512 GB memory and 200 gb/s infiniband
- 8 high memory (2TB) nodes with same bandwidth
- 3 nodes with 8 NVIDIA V100 GPU (gpu-dev queue, 2 hours walltime)
- 5 Virtual Desktop nodes (VDI) for Remote Desktop, can be configured in Linux/Windows OS. 
- All  clusters' nodes are interconnected with high speed infiniband network 200 gb/s
