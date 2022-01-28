---
title: "Storage on M2"
questions:
- "How and where can I store my files?"
teaching: 15
exercises: 0
objectives:
- home directory, scratch space
keypoints:
- "users get 200 Gb of backed-up storage in their home directories"
- "they also have access to more than 2 Pb of scratch storage"
- "scratch storage is not backed up"
---

Every M2 user gets 200 Gb of storage space; this storage is backed up at the end of every day. So if you accidentally delete a file that was created more than a day ago, we might be able to restore it. This storage is called *home directory*, used to store your installed program and data

In addition, users are given 8TB work storage (long term storage) and unlimited scratch storage

To see how much space you have left in your home directory, please type:

~~~
cat /hpc/motd/m2_queue_status
~~~
{: .bash}

Since most of you are new users of M2, you should be using very little storage at the moment.

When you log into M2, you end up in your home directory. To see which directory you are in, type 

~~~
pwd
~~~
{: .bash}

...which stands for "print working directory". It should give you something like

~~~
/home/<your username>
~~~
{: .output}

200 Gb might be enough for some, but for people dealing with extensive amounts of data that would not be enough. We also offer the access to *scratch space*, which is about 2.8+ Petabytes in total. Scratch space running in Lustre system and is not backed up. The reading/writing speed is 70.8/56.4 GB/s when used in parallel. We strongly encourage people to use scratch space, but please be aware of its temporary nature. When you get anything that is worth keeping, please back it up, either in your home directory, work directory or on your local machine.

To go to a scratch directory, or to any directory on M2, use the `cd` ("change directory") command:

~~~
cd /scratch/users/<your M2 username>
~~~
{: .bash}
 
To go to your home directory, you can do

~~~
cd /home/<your M2 username>
~~~
{: .bash}

There is also a shortcut; to go to your home directory, you can simply type

~~~
cd
~~~
{: .bash}
