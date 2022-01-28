---
title: "The structure of the M2 Cluster"
questions:
- "What is the structure of the M2 Cluster?"
teaching: 15
exercises: 0
objectives:
- compute and login nodes, hardware table
keypoints:
- "M2 contains more than 400 interconnected compute nodes"
- "a specialized login node runs the SSH server"
---
Structure of M1 and the updated M2:

![image](https://user-images.githubusercontent.com/43855029/151623191-d2732bf2-7eda-4ed3-a155-bda7010ff083.png)



The computers that make up the M2 cluster are called *nodes*. Most of the nodes on M2 are *compute nodes*, 
that can perform fast calculations on large amounts of data. There are also several special nodes called the *login nodes*; they run the server, 
which works like the interface between the cluster and the outside world. 

The people with M2 accounts can log into the server by running a client (such as `ssh`) on their local machines. 
Our client program passes our login credentials to this server, and if we are allowed to log in, the server runs a shell for us. 
Any commands that we enter into this shell are executed not by our own machines, but by the login node.

![image](https://user-images.githubusercontent.com/43855029/151622253-e177426a-9957-4c65-a4f4-618289e35b4e.png)

Another special node is the *scheduler*; M2 users can get from the
login node to the compute nodes by submitting a request to the scheduler, and the scheduler will assign them to the most appropriate compute node.
M2 also has a few so-called "service" nodes, which serve special purposes like transferring code and data to and from the cluster, and hosting web applications.

To see which nodes are available at the moment, you can type 

~~~
cat /hpc/motd/m2_queue_status
~~~
{: .bash}

You will see something like this:

~~~
======================================================================================
|M2 SLURM queue status. Last reported at TimeStamp:  Fri January 28 2022  03:00PM      |
======================================================================================
|Queues                       Jobs Running         Jobs Waiting           Idle Nodes  |
======================================================================================
|standard-mem-s                        404                    4                    0  |
|debug                                   0                    0                    1  |
|idl-test                                0                    0                    0  |
|standard-mem-m                         30                    4                    0  |
|standard-mem-l                         17                    1                    1  |
|htc                                   402                 8486                    0  |
|development                             0                    2                    4  |
|medium-mem-1-s                        103                    1                    1  |
|medium-mem-1-m                         11                    1                    0  |
|medium-mem-1-l                          5                    0                    0  |
|medium-mem-2                            0                    0                    3  |
|high-mem-1                              5                    1                    1  |
|high-mem-2                              2                    0                    4  |
|gpgpu-1                                32                   15                    1  |
|desktop                                11                    0                    7  |
|admin                                   0                    0                    1  |
|desktop-vdi                             0                    0                    0  |
|desktop-vdi-dev                         0                    0                    0  |
|mic                                    54                    7                    0  |
|dtn                                     1                    0                    1  |
|fp-gpgpu-3                              0                   16                    0  |
|fp-gpgpu-4                              0                    0                    1  |
|fp-gpgpu-2                              0                    0                    1  |
|v100x8                                  5                    2                    0  |
|amd                                     0                    0                    1  |
======================================================================================
| Updated every 20 minutes. To get updated stats type # cat /hpc/motd/m2_queue_status |
~~~

This table shows the amount of different queues, number of running jobs, waiing jobs and idle nodes. The number of *idle nodes* per each queue are completely free node: a node which has, for example, 8 cores, but only 4 of them are used, would not be counted as "free". So this table is a conservative estimate. This picture can change pretty drastically depending on the time of the day and the day of the week.

