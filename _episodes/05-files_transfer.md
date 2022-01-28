---
title: "Transferring files to and from M2"
teaching: 15
exercises: 0
questions:
- "How can I transfer data between M2 and my local machine?"
objectives:
 - WinSCP, FileZilla
keypoints:
- Windows users can use WinSCP for file transfer
- Mac users can use FileZilla
---

## CyberDuck

There are many ways to transfer files between your local computer and M2. One piece of software that works for both Mac and Windows machines is called CyberDuck. You can download it [here](https://cyberduck.io/download/).

After installation, click on "Open Connection". A new window will pop out:

Let's configure the connection:
- in the drop-down menu on top, select "SFTP" instead of the default "FTP";
- in the "Server", please specify `m2.smu.edu`;
- make sure that Port is set to 22;
- specify your M2 username and password.

Then, click on "Connect". Another window will pop out asking you to do two-factor verification:

Type "1" (the number one) or the word "push" if you want to get a DUO push notification. After two-factor verification, a yet another new window will pop up, which will contain the contents of your M2 home directory (if this is your first time using M2, it will be empty). You can go to any other folder on Palmetto by changing the path (e.g., `/scratch/users/username`). You can upload files by clicking the "Upload" button, and download files by right-clicking them and selecting "Download".

## MobaXTerm (Windows users only)

For small file transfers, the Windows users can use the built-in function in MobaXTerm. On the left side of the MobaXTerm window, you will see the browser of your M2 directory. By default, it points to your home directory: `/home/<your M2 username>`. You can point it to any other folder that you have access to, for example, to `/scratch/users/<your M2 username>`. To upload files *to* M2, use the UP arrow &uarr;, and to download files *from* M2, use the DOWN arrow &darr;.

![image](https://user-images.githubusercontent.com/43855029/151627971-e6c777b5-a0fa-46c0-b6d7-acf125f813f4.png)

## command line (Mac and Linux users)

Another option for advanced Mac and Linux users is to use the `scp` command from the terminal. Open a new terminal, but **don't connect to M2**. The `scp` command works like this:

~~~
scp <path_to_source> username@m2.smu.edu:<path_to_destination>
~~~
{: .bash}

For example, here is the `scp` command to copy a file from the current directory on my local machine to my home directory on M2 (`tuev` is my M2 username:) 

~~~
scp myfile.txt tuev@m2.smu.edu:/home/tuev/
~~~
{: .bash}

... and to do the same in reverse, i.e., copy from M2 to my local machine:

~~~
scp tuev@m2.smu.edu:/home/tuev/myfile.txt .
~~~
{: .bash}

The . represents the working directory on the local machine.

To copy entire folders, include the -r flag:

~~~
scp -r myfolder tuev@m2.smu.edu:/home/tuev/
~~~
{: .bash}


