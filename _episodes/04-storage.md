---
title: "Storage on M3"
questions:
- "How and where can I store my files?"
teaching: 15
exercises: 0
objectives:
- home directory, scratch space
keypoints:
- "users get 200 Gb of backed-up storage in their home directories"
- "Users get access to Cold Front allocation work storage"
- "scratch storage is not backed up"
---

Every M3 user gets 200 Gb of storage space; this storage is backed up at the end of every day. So if you accidentally delete a file that was created more than a day ago, we might be able to restore it. This storage is called *home directory*, used to store your installed program and data

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

200 Gb might be enough for some, but for people dealing with extensive amounts of data that would not be enough and they are encouraged to use the Cold Front allocation storage

To go to a scratch directory, or to any directory on M3, use the `cd` ("change directory") command:

~~~
cd /scratch/users/<your M3 username>
~~~
{: .bash}
 
To go to your home directory, you can do

~~~
cd /home/<your M3 username>
~~~
{: .bash}

There is also a shortcut; to go to your home directory, you can simply type

~~~
cd
~~~
{: .bash}
