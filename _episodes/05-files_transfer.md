---
title: "Transferring files to and from M3"
teaching: 15
exercises: 0
questions:
- "How can I transfer data between M3 and my local machine?"
objectives:
 - WinSCP, FileZilla
keypoints:
- Windows users can use WinSCP for file transfer
- Mac users can use FileZilla
- In terminal, use scp (secure copy via ssh)
---

## command line (via terminal)

Another option for advanced Mac and Linux users is to use the `scp` command from the terminal. Open a new terminal, but **don't connect to M3**. The `scp` command works like this:

~~~
scp <path_to_source> username@m3.smu.edu:<path_to_destination>
~~~
{: .bash}

For example, here is the `scp` command to copy a file from the current directory on my local machine to my home directory on M3 (`tuev` is my M3 username:) 

~~~
scp myfile.txt tuev@m3.smu.edu:/home/tuev/
~~~
{: .bash}

... and to do the same in reverse, i.e., copy from M3 to my local machine:

~~~
scp tuev@m3.smu.edu:/home/tuev/myfile.txt .
~~~
{: .bash}

The . represents the working directory on the local machine.

To copy entire folders, include the -r flag:

~~~
scp -r myfolder tuev@m2.smu.edu:/home/tuev/
~~~
{: .bash}

## Transfer file via hpc.smu.edu

